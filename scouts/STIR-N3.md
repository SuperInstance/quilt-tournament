# STIR-N3 — Quadruple-Buffered Multi-Stage Commit

**Provenance:** Two external sources consulted (Wikipedia on double/triple buffering; questdb on append-only logs; transaction processing research). The STIR is a novel fusion: use **buffered staged commits** where every effect is not just "committed" atomically, but **validated against a history buffer** before it enters the stable, append-only ledger.

## The core idea

Every cellcore runtime does this today:
1. **Effects queue** (pending ops, not yet committed)
2. **Commit gate** (atomic decision: commit or abort)
3. **Write-ahead log** (append-only ledger for crash recovery)
4. **State materialization** (apply committed effects to runtime state)

This STIR replaces the **single two-phase commit** with a **three-stage buffered pipeline**:

```
Effect → Buffer-1 (writeback) → Buffer-2 (validation) → Append-Only Ledger → State
```

### Stage 0: Buffer-1 (Immediate Writeback)
- When a cell requests an effect (deposit, transfer, reject), it is NOT immediately written to the append-only ledger.
- Instead, it is appended to **Buffer-1** (a cyclic ring of, say, 1024 entries).
- Buffer-1 is **in-memory, mutable**, and survives crashes (stored on heap, not persistent storage).
- Reasoning: early writeback means the cell sees its own state updates instantly — no additional synchronous commit hop.

### Stage 1: Buffer-2 (Staged Validation)
- A background tick or per-effect gate evaluates **Buffer-1** entries:
  - **Consistency check:** Does the proposed effect violate bounded-state invariants?
  - **Balance check:** Does the fisher have a booked debit for the fish entering the hold?
  - **Chain check:** Does this effect extend an existing chain of effects that is still in Buffer-1?
- If **Buffer-2** deems an entry valid, it "advances" — the entry moves from Buffer-1 → Buffer-2.
- If **Buffer-2** deems an entry invalid, it is **promoted to a logged error** and rejected without touching the ledger.
- Buffer-2 is a **bounded buffer** (same size as Buffer-1), so it never overflows — overflowing entries are forced into the ledger immediately with an explicit "overflow" flag.

### Stage 2: Append-Only Ledger (The Truth)
- Only entries that have passed **Buffer-2** are atomically appended to the append-only ledger.
- The ledger never sees:
  - Invalid effects
  - Incomplete chains (effects that depend on a predecessor that is still in Buffer-1)
  - Inconsistent states that violate bounded invariants
- The ledger is the **source of truth** for crash recovery and audit. If a cellcore crashes after writing to Buffer-1 but before Buffer-2, it simply discards Buffer-1 and replays the ledger forward.

### Stage 3: State Materialization (Materialized View)
- After a buffer advances to the ledger, the cell's state is updated with that effect.
- The state is a **materialized view** of the ledger, kept up-to-date by a **single pass over the ledger** each tick.
- No per-effect state update is done directly — only ledger-appended effects trigger state changes.

## Why this matters for the tournament

### For the LEDGER team (batch, audit-first, conservation as primitive)
- **Buffer-1** gives them immediate writeback without sacrificing auditability — the audit trail exists as soon as the entry lands in Buffer-1, not in the ledger.
- **Buffer-2** is a validation gate that enforces bounded-state invariants before anything touches the ledger.
- The append-only ledger remains the source of truth, which aligns with LEDGER's philosophy.

### For the STREAM team (signal, wavefront, FIFO)
- **Buffer-1** is a **FIFO pipeline stage** — a wavefront of effects flowing through the runtime.
- **Buffer-2** is a **validation wavefront** — downstream cells can validate effects before they become permanent.
- The staged pipeline introduces a natural **tick discipline**: effects that haven't passed Buffer-2 are not considered "visible" until the next tick.

### For the ORGANISM team (hebbian, stigmergy, healing)
- **Buffer-1** as a **growth buffer** — cells can propose effects that the runtime "learns" over time.
- **Buffer-2** as a **healing gate** — only effects that survive the validation pass become part of the organism's structure.
- Invalid entries are not rejected outright; they are **logged as adaptive signals** that the organism can "heal" in future ticks by adjusting its hebbian rules.

### For the SHIPWRIGHT team (minimal verbs, joinery, pieces that fit)
- **Buffer-1** is a **temporary staging deck** — effects are staged before they become permanent.
- **Buffer-2** is a **carpenter's inspection** — only effects that are structurally sound are let through.
- The append-only ledger is the **final planking** — once planks are in place, they are never altered.

### For the PROCESSION team (teaching, tutorial-first)
- **Buffer-1** is a **draft buffer** — cells propose effects, and the runtime can show them to the cell for review.
- **Buffer-2** is a **validation tutorial** — the runtime can explain WHY an effect is valid or invalid, teaching the cell's operators.
- The append-only ledger is the **textbook** — once an effect is in the ledger, it's a "recorded fact" that can be referenced and explained.

### For the DEADBAND team (perception-first, audit schedules, drift prefilters)
- **Buffer-1** is a **sensor buffer** — raw effects enter with minimal processing.
- **Buffer-2** is an **audit schedule** — a phased check that detects drift, bias, and noise before effects are committed.
- The append-only ledger is the **calibration baseline** — a stable reference that drift-oversight can compare against.

## How to implement this

### Buffer-1 (Ring Buffer)
```rust
pub struct Buffer1 {
    entries: VecDeque<Entry>,
    capacity: usize,
}

impl Buffer1 {
    pub fn append(&mut self, effect: Effect) -> usize {
        if self.entries.len() == self.capacity {
            self.force_rollover() // or return Err(Overflow)
        }
        self.entries.push_back(effect)
    }
}
```

### Buffer-2 (Validation Stage)
```rust
pub struct Buffer2 {
    entries: VecDeque<Entry>,
    capacity: usize,
    ledger: &mut AppendOnlyLedger,
}

impl Buffer2 {
    pub fn advance_entry(&mut self) -> Option<Entry> {
        let entry = self.entries.pop_front()?;
        // Validate the entry here
        if entry.is_valid() {
            self.ledger.append(entry.clone())?;
            Some(entry)
        } else {
            // Log error, don't advance
            None
        }
    }
}
```

### Ledger Append (Atomic)
```rust
pub struct AppendOnlyLedger {
    entries: Vec<Entry>,
    head_position: usize,
    next_position: usize,
}

impl AppendOnlyLedger {
    pub fn append(&mut self, entry: Entry) -> Result<(), CommitError> {
        // Atomic append — no partial writes allowed
        self.entries.push(entry);
        self.head_position = self.next_position;
        self.next_position += 1;
        Ok(())
    }
}
```

## Trade-offs

### Benefits
1. **Bounded-state integrity:** Buffer-2 can enforce invariants before anything touches the ledger.
2. **Crash recovery simplicity:** If Buffer-1 is lost, the runtime simply replays the ledger — no need to "recover" a partial Buffer-2.
3. **Audit trail from entry:** Buffer-1 is mutable, so you can add audit metadata (who proposed it, when) before validation.
4. **Per-cell validation:** Each cell can have its own Buffer-2 that validates its local invariants before committing globally.

### Risks
1. **Extra memory:** Buffer-1 and Buffer-2 double the memory footprint (though bounded).
2. **Latency:** Effects are not committed until they pass Buffer-2 — adds a tick delay.
3. **Complexity:** Three-stage pipeline vs. single two-phase commit adds a new coordination problem.
4. **Buffer overflow:** If Buffer-2 is slower than Buffer-1, you can overflow. Mitigation: dynamic sizing or forced flush.

## Challenge to teams

Each team must answer this booked question:

> **Can you prove that Buffer-2 does not add any new atomic commitment problem that wasn't already present in the original two-phase commit? If not, where does the atomicity come from?**

- LEDGER: Is the audit trail in Buffer-1 still valid if Buffer-2 fails after Buffer-1 advances?
- STREAM: Is the wavefront discipline preserved if Buffer-2 introduces arbitrary latency?
- ORGANISM: If a cell's hebbian rules depend on seeing an effect in Buffer-1 before Buffer-2, does Buffer-2 break that adaptation?
- SHIPWRIGHT: Is the staged joinery still minimal if Buffer-2 introduces additional verbs?
- PROCESSION: If the tutorial-first interface requires cells to see effects in Buffer-1 before validation, how does Buffer-2 explain the rejection?
- DEADBAND: If Buffer-2 is an audit schedule, does it enforce drift prefilters, or does drift escape into Buffer-1?

## Scout's provocation

> **"You're not adding a third phase. You're hiding the first phase. Buffer-1 is just a delayed commit. The real question is: is the validation gate inside Buffer-2 or outside it? If it's inside, you haven't reduced the atomic commitment problem — you've just split it. If it's outside, you're back to two-phase commit, just with a longer label."**

---

**STIR-N3 provenance:** Wikipedia (double/triple buffering), questdb (append-only logs), transaction processing research (two-phase commit). Scout order: flash+web. Round: R3 RIVAL IDEAS. Booked to all six teams. No rejection without a booked reason the scout can publicly rebut.
