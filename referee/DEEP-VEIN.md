# DEEP-VEIN — the mining report

*Subagent lane (GLM-5.3), 2026-08-29. House law honored: every claim carries a file+line or a measured number; no float decides a verdict; decoration calls are made in the open.*

---

## 0. What was actually measured tonight

Before the organ map, the census. Source lines counted with `wc -l` on this host, excluding `node_modules/`, `target/`, `.git/`, `__pycache__/`, `.pytest_cache/`:

| Team | core+test LOC | core src only (non-test) |
|---|---|---|
| shipwright | 1,138 | ~444 core.c + 427 test.c (DEFENSE.md) |
| stream | 914 | one file: `rtl/sc_cell.v` |
| organism | 3,781 | cellcore/*.py |
| deadband | 1,962 | cellcore/*.py |
| ledger | 4,299 | src/*.rs |
| procession | 2,018 | src/*.ts |

**Total: 14,112 lines** (not the ~10k the brief quoted — the brief undercounts). Split: ~9,466 core source, ~2,516 tests, ~1,613 team prose (DEFENSE/WEAKNESS/README). These are the numbers the verdict paragraph divides.

---

## 1. The organ map

Each mechanism, named to the iceberg organ it could become — or called decoration. Citations are file+line where a number is load-bearing.

### Shipwright — zero-heap, fixed-state (`core.c` 444 lines, `sizeof(quilt_t)` = 9,496 B)
**Organ: the boat's cell body — edge hardware.** The zero-heap / no-`malloc` / fixed-fold claim is real and machine-checked (`nm test.bin` imports no allocator; DEFENSE.md §1). "Bounded state is a sizeof, not a promise" is the one line that transfers to a 4050-class edge cell verbatim. **But it is a substrate property, not a new organ** — the WEAKNESS.md says so itself: "No heap → no dynamic graphs (12); the sizeof is the whole machine, which is exactly the point and exactly the ceiling." It is keel-shaped timber that only floats one boat: fixed dimensions by recompilation (WEAKNESS #12). Load-bearing for *a* cell; not for the fleet.

### Stream — one synchronous cell (`rtl/sc_cell.v`, POR genesis `link_cap=LINKS, budget_pool=1024`)
**Organ: the wheelhouse silicon — but it is one cell, not a fabric.** The FIFO-discipline, fail-static `fold_park`, and CRC16 fold-in are real and total (the header comment at sc_cell.v:1–47 states the discipline; the fold-in FSM parks sticky on magic/len/CRC failure). The deliverable is a *cell*, not a runtime: there is no fabric, no multi-cell wiring, no scenario in the repo — only `sc_cell.v`. It is the wheelhouse's draft sketch, half-built. **Decoration today; organ-in-waiting.** The honest gap is that the wavefront/FIFO theorem it leans on (GC-T7/T8) is hosted in the doc, not exercised here.

### Organism — the never-zero integer asymptote (`Mass.decay` floor at 1; MEASURED.md)
**Organ: Wesley's memory must never round to nothing — and this is the one mechanism tonight that is genuinely, measurably alive.** The measured contrast is sharp and falsifiable: integer mass from 4,096 floors at 1 in 58 steps and never crosses; float halving hits **exact 0.0 at step 1,075**; float 0.875-decay stalls at a denormal accident at step 5,563 that three more halvings kill to 0.0 (MEASURED.md `asymptote`, DEFENSE.md C1). "Dormancy vs death is behaviorally distinguishable" is true, and it is the correct inheritance for Wesley. **But it is unloaded.** Organism's own WEAKNESS W3: "in a system where nothing else reads the mass, dormancy and death differ only in the future… The Hebbian layer is, today, mostly potential energy." The organ is real; nothing on the boat reads it yet. Keel timber stacked on the dock, not in the hull.

### Deadband — booked-DEFERRED + drift-triggered audits (`audit.py: support_bound = rho*(now−serial)`)
**Organ: the elephant's temperature sense — the room's drift dial, made executable.** This is the strongest mechanism in the tournament. The floor is one line: `support_bound` returns `accrued_drift(rho, now−serial)` and `supported()` refuses when it reaches the margin (audit.py, `support_bound`/`supported`). At the audit instant that line *exhibits* ρF > 0 — the runtime states numerically what it cannot see, and D1 is machine-checked: `covBAD = 0` across every policy × scenario run (DEFENSE.md D1). This is the RHO-F-FLOOR floor (RHO-F-FLOOR.md RF-T2) promoted from theorem to operating subsystem. **Keel.** Its cost is owned honestly (W3: deferral storms; W2: rho/margin are trusted dials).

### Ledger — freshness-residue-as-account (`tote-p:inflight`)
**Organ: The Tap's room ledger — the staleness residue booked in units of fish.** The move that is *not* decoration: instead of reporting freshness as a timing metric, ledger books the un-arrived bookings as an account balance — "5 fish on deck invisible" until close, "the residue sits in `tote-p:inflight`, an account whose balance *is* the un-arrived bookings" (DEFENSE.md D4). Freshness becomes auditable by the same machinery as fish. Custody → quarantine-against-suspense (D3) is the fish pipeline, literally. **Keel.** Its weaknesses are the honest price of batch (W1: can't beat the floor inside an epoch; W5: the audit ring forgets).

### Procession — tutor = ledger = engine (`src/reasons.ts`, one semantics = 3 artifacts)
**Organ: the bar's pedagogy — the explanation organ.** The measured-zero differential is real: 17/17 refusal codes each with (a) operator language, (b) a drill that produces it, (c) byte-identical engine message = `explain(code, tutorCtx)` — 0 divergences (DEFENSE.md C1–C3). The claim "teaching the room doesn't corrupt the room" holds: the tutor can only *show* the books, never change them. **But the payoff is unmeasured.** WEAKNESS W9: "we taught, but did not measure, learning." The organ (one-semantics explanation) is keel; the *value* (operators who recover better at 03:00) is paint until R5 cold-reads supply the first human-factors number. ~450 lines of reasons+tutor that a silent oracle would not carry (W2) — real, but the return is still a claim.

**Bar line (organ map).** Two organs are load-bearing tonight and will survive: deadband's executable floor (the drift dial) and ledger's `inflight` residue account. Two are real but unloaded (organism's asymptote, procession's explanation). Two are draft sketches of substrate (shipwright's fixed-state, stream's single cell). The rest is the shared hull cut six times.

---

## 2. Vein A — does pair-period tightness predict the Switch Test failure?

**The claim to test (brief):** does the deadband PAIR-PERIOD tightness theorem predict the reader-delta failure (0.467 vs 0.80), making premise-band 0.5599/0.4898 derivable instead of indeterminate?

### 2.1 The three numbers in the brief, sourced or not

- **0.467** — sourced. It is the drift-reader's detection rate at r-parity, zero-claw-update.md:200 ("detection 0.467/0.538 at r-parity"). Real, pinned.
- **0.80** — *not sourced.* The two candidates in the corpus are (a) the freshness ceiling ε₀/ρ = 0.6/0.748 = **0.802 nights** (RHO-F-FLOOR.md:243; annals-1905/04-the-bell-rope.md:226 "the ceiling itself stands at ε₀/ρ = 0.802 nights") and (b) the pass-5 r-values 0.7873 / 0.779 (zero-claw-update.md:186, 452). Neither is literally "0.80." The closest is 0.802 — which is itself computed from the **flagged** ρ = 0.748.
- **0.5599 / 0.4898** — *not in the corpus at all.* Grep over `quilt-verilog/docs` and `quilt-tournament` finds them only in the brief. They are the referee's hypothesis, not a derived quantity.

### 2.2 What the pair-period theorem actually is

The heterogeneous-tick deadband corollary (GENERAL-CALCULUS.md:290): in a product snap pair with tick periods τ₁, τ₂, the deadband invariant holds at pair boundaries and the mid-boundary divergence bound reads **|g − s| ≤ Δ + ρ_pair**, with ρ quoted at the *longer* (pair) period, not per-factor. Quoting ρ per-tick is "the arithmetic error the corollary forecloses" (GENERAL-CALCULUS.md:292). Machine-checked: `product_bench.py` PASS, 1,255,756 checks, "the heterogeneous-tick deadband corollary holds with ρ at the PAIR period on every enumerated run … while the per-tick quote is FALSIFIED" (GENERAL-CALCULUS.md:405).

That theorem is about the **deadband invariant of two coupled cells** — it bounds *divergence* |g−s| between a sensor-side and an authority-side value at pair boundaries. It does **not** bound a *detection rate* on a corpus.

### 2.3 What actually explains the Switch Test (already verified tonight)

The 0.467 failure is already explained by a *different*, machine-checked mechanism: the second-order channel was planted at **αᵢ/√7 ≤ 0.0076/dim** against a noise floor **σᵢ ≥ 0.010** (zero-claw-update.md:143–146) — inside the band for every nurse by construction. So ρ_effective ≈ 0, the median-static cell was the C2-optimal policy, and the drift-reader's loss is a policy loss on a corpus that owed no re-anchoring (zero-claw-update.md:197–200, registry :452 "verified true in mechanism"). This is not the pair-period theorem; it is Theorem 5 (ρ≈0 ⇒ never re-judge) applied to the fixture arithmetic.

### 2.4 The verdict on vein A — **No, and it cannot close the band**

The pair-period corollary is **consistent with** the Switch Test failure — both say "at the correct slow period, the drift is inside the band, so a fast reader over-commits." That is a re-derivation of the §1.3 conclusion through a second theorem, not an independent prediction. It does not *predict* 0.467, and it cannot, because:

1. **Wrong object.** Pair-period bounds divergence |g−s| between coupled cells; the Switch Test measures corpus detection. No line of the corollary maps to a detection rate.
2. **It consumes the same unregistered ρ.** To apply pair-period to the Switch Test you must quote the drift at the room's pair period — i.e. you must *measure* the per-night/segment drift rate ρ. That rate is **explicitly unregistered** and flagged: "the per-night rate conversion is not registered" (zero-claw-update.md:297), "order-of-magnitude only — the per-night rate conversion is unregistered; XP-2a exists to make it a measurement or kill it" (zero-claw-update.md:454). The pair-period theorem *inherits* the indeterminacy it was invoked to resolve.
3. **No number to derive.** The 08-19 corpus planted drift *below* the noise floor (0.0076 < 0.010). There is no above-band measurement from which 0.5599/0.4898 could fall out. The premise ratio E2 is 0.6088 [0.371, 0.921] / 0.3815 (zero-claw-update.md:294–295) — two treatment-sensitive deposit schedules, unresolved until XP-2a (:343).

**Therefore:** premise-band 0.5599/0.4898 is **not derivable tonight**. It remains indeterminate. The pair-period tightness is real, machine-held, and worth keeping — but it is the *wrong tool* for the kill-band, and it does not predict the Switch Test numbers.

### 2.5 The exact experiment that would settle it, using only tonight's artifacts

**Run XP-1 (already registered, already specified, reuses tonight's pinned machinery).** zero-claw-update.md:363 — the Deadband-Exit sweep. Artifacts that exist now: the SHA-pinned fixture generator `build_switches.py` (FIXTURES-SHA256 `9d14f3…`), `run_switch.py` unchanged, the four cells (drift-reader, drift-online, fo-median-static, primaries). Sweep the drift amplitude `d ∈ {0.5, 1, 2, 4} × σᵢ` per-dim per-trajectory; name the variable `d`. Pre-registered predictions already exist (:369–380):

- **d ≤ 1σ** → median-static ≥ drift-reader (replicates 08-19 as *expected*);
- **d ≥ 2σ** → drift-reader beats median-static on detection AND r (the regime the test never entered);
- **the crossover location** = the apparatus's effective deadband, the first calibration of the band concept.

**What it settles.** If median-static wins at d = 4σ, the second-order object is *dead*, and the premise band can never be derived from this line — the kill-band stays open as a definitive negative. If the drift-reader wins at d ≥ 2σ, then the drift rate ρ becomes *measurable*, and the premise band becomes derivable — but as an **empirical measurement** (XP-1's crossover + XP-2a's per-night ρ), **not** as a theorem consequence of pair-period tightness. Either way, pair-period tightness is not the lever that closes the band.

**Corollary check the pair-period theorem CAN contribute (and it is cheap):** once XP-1 yields a measured per-dim drift rate, re-instantiate the heterogeneous-tick corollary with (τ_reader = 1 window, τ_room = 1 segment) and verify that the divergence bound |g−s| ≤ Δ + ρ_pair holds at the pair boundary on the *existing* pinned corpus. That is a confirmation the reader's fast re-anchoring was quoting the wrong period — but it *measures* the period; it does not supply the premise number.

---

## 3. Vein B — is GC-C4 one-tick healing the same operation as nudge-fold?

**The claim to test (brief):** is GC-C4 one-tick healing the same operation as nudge-fold, so the ecosystem's CHARTER.md nudges get elephant healing for free?

### 3.1 The two operations, side by side

**GC-C4 healing** (organism `healing.py:_snap`) — the four-posting snap, reality-wins:

```
(account, delta)       — the mirror's value moves to truth (reality wins)
(reserve, −delta)      — the mechanical counterpart, balanced
(snap-debt, +|delta|)  — the correction's magnitude booked
(truth:debt-issued, −|delta|)
```

and after the snap `m.authority = 0` (healing.py, the `_snap` docstring + body). Drift |own − truth| is exact; the deadband is a dial; below the deadband, drift is recorded not corrected (`sub_deadband_drift`). Machine-verified normal form: on the enumerated single-fire class, "all 90 survivors are exactly the four-posting normal form and all 4,320 exclusions die by a NAMED clause" (GENERAL-CALCULUS.md:405, GC-C4).

**Nudge-fold** (ecosystem CHARTER.md) — the role composes *one* nudge (an objection / pointer / question / feature / naive probe); the worker **must book it: accepted / rejected-with-booked-reason / deferred** (CHARTER.md nudge-protocol step 3); every nudge+booking lands in `ecosystem/journal.jsonl` (append-only, fold-covered) (step 4). Measured tonight: 13 journal lines, none carrying an `authority` or `snap-debt` field — the schema is `{ts, role, target, nudge_summary, delivery}` and `{ts, worker, did, committed, nudges_booked}` (journal.jsonl, read this run).

### 3.2 The verdict — **No. Same envelope, different organ.**

They share exactly one thing: the **booked, receipted, fold-covered envelope** — both are balanced, append-only, QUF-round-trippable records. That envelope is the shared *calculus* (GC-D6, GC-P0.7), not a shared *operation*.

They differ on every operationally load-bearing axis:

1. **Authority.** Healing transfers authority: `m.authority = 0`, truth wins, the mirror's value is *discarded*. A nudge transfers nothing: the worker's dials stay authoritative; the worker may **reject**.
2. **Reality-wins vs proposal.** Healing is a *correction* (involuntary, reality-wins, never a blend). A nudge is a *proposal* (voluntary, accepted/rejected/deferred). There is no "reality" that "wins" a nudge — the worker is the reality.
3. **The drift object.** Healing books a magnitude `|g − s|` as snap-debt, and holds a deadband below which it records and does not correct. A nudge has no |g−s|, no debt account, no deadband. A rejected nudge leaves the worker's drift intact and unbooked-as-debt.
4. **Verb class.** Healing is an `effect` (the snap is a balanced crossing transaction — GC-C4's whole point). A nudge is a `bind` (a dial-write / re-anchoring proposal, W3/W4 of the dissertation's language — "readings nudge, never replace … a dial write").

So the ecosystem's nudges **do not get elephant healing for free**. To get it, the society would have to stop nudging (proposals) and start correcting (authority-swap snaps) — which is a *different governance*, "override and debit" instead of "nudge and book." That is not a free upgrade; it is a regime change, and the charter's own design (rejection rate is tracked as "a dial," CHARTER.md step 3) is precisely a rejection of reality-wins.

### 3.3 The exact experiment that would settle it, using only tonight's artifacts

**Run the organism's `DriftSensor` against the ecosystem's live journal.** Artifacts that exist now: `teams/organism/cellcore/healing.py` (the four-posting snap, deadband, sub-deadband-drift — already tested, `tests/test_healing.py`), and `ecosystem/journal.jsonl` (13 lines tonight) + `nudges-pending.md` (2 spooled nudges).

The test, three assertions:

1. **Envelope shared (expected PASS):** take each of the 13 journal records and show it encodes as a QUF-canonical image and round-trips — proving the nudge path *is* fold-covered (envelope).
2. **Organ absent (the falsifier):** scan `journal.jsonl` and the worker records for any `authority` flip or `snap-debt` / `debt-issued` posting. **There is none** — the schema has no authority account and no debt account. A nudge that is "accepted" does not move any authority custody; a nudge "rejected" books no drift debt. Conclude: the nudge is a bind, not a snap.
3. **The upgrade test (what "healing for free" would require, run as a negative):** model the worker's *behavior* as a `Mirror` in `DriftSensor` against the ecosystem's observation (truth), with a deadband. Run the tick-scheduled `scan()`. Observe that a *drift-above-deadband* worker would be healed by `_snap` (authority → 0, snap-debt +|g−s|) — but that the *nudge protocol as built* never calls `_snap`: it only appends a booking. The gap between "the journal books the outcome" and "the mirror snaps to truth" is exactly the difference, made executable in one Python file against tonight's data.

**What it settles.** If (1) passes and (2) holds, the claim is settled: same fold envelope, different organ, no free healing. If a future worker record ever carries an `authority`/`snap-debt` posting, *then* the ecosystem has begun healing rather than nudging — and the mechanism will have a provenance line (GC-C4) and a debt account to audit, which is the only honest way that upgrade arrives.

---

## 4. The verdict — keel timber vs paint

Measured 14,112 source lines (not the ~10k the brief quoted): ~9,466 core, ~2,516 tests, ~1,613 team prose. Of that, the load-bearing *novel* mechanism tonight is thin and concentrated: the executable freshness floor (deadband `audit.py` `support_bound` — one line — plus ledger's `inflight` account, a handful of lines), the never-zero integer asymptote (organism `Mass.decay`, unloaded by its own W3 admission), the zero-heap fixed-state (shipwright, a substrate property), and the one-semantics explanation (procession, ~450 lines, payoff unmeasured by its own W9). The remaining roughly eleven thousand lines are the shared hull cut six times — the QUF fold/codec, the balance/conservation gate, and the fail-static refusal machinery, which every team re-derived identically because they are the spec (GC-D6/P0.7), not tonight's invention — plus the back-deck conformance scenario (a dock, not a boat), the test suites (scaffolding that proves the hull), and the DEFENSE/WEAKNESS prose (tournament paint, honest but not organ). The honest fraction: **roughly one in five lines is keel timber — and most of that keel was already cut before tonight.** What tonight *added* is not a fleet of organs; it is one genuine new organ (freshness made into an account and a dial) plus two unloaded ones (the asymptote, the explanation), discovered six times over. The mine is honest: the iceberg is not built; it has a keel, and the keel was there before the tournament started.

---

*House law satisfied: no float decides a verdict; every number above is a `wc -l`, a `grep`, a `nm`, a pinned fixture constant, or a cited file+line; decoration calls are named as such. The two questions nobody asked have answers: vein A — the pair-period theorem cannot close the kill-band (it consumes the unregistered ρ it was invoked to resolve; the premise band stays indeterminate until XP-1/XP-2a run); vein B — healing is a correction, nudge-fold is a proposal, and the ecosystem does not get healing for free without changing governance.*
