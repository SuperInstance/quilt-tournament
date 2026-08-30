# R3-SCORES — DEADLEDGER graded; the field's next challenge

*Referee · 2026-08-30 · every number below re-measured by the referee on
this bench (not inherited from the build lane's report); citations
spot-checked file:line. Undersell, overdeliver.*

## 1. DEADLEDGER verification (referee's own runs)

- `cargo test` (teams/deadledger): **68 passed, 0 failed** across 7
  suites, re-run cold by the referee after the lane docked. Parent
  ledger's repaired core carried 49/49 green before the first new
  commit (996f2dc verbatim keel harvest, parent 4f6fda0/050939f/5a62fcd
  cited in-message).
- `cargo run --release --example r3bench`: encode 1870 ns/fold, decode
  2626 ns/load, mated load 7669 ns (+192% over decode), empty close
  32 ns, floor close 233 ns (+201 ns), image +912 B — within noise of
  the lane's booked numbers (2631/7713/+193/+195). **Costs confirmed.**
- Custody: `qc-mint.key` stat'd 0600 by the referee; key ceremony wired
  (`FoldKey::load_or_mint`, inherited from the repaired ledger parent).

### Citation spot-checks (file:line)

- Mate fail-closed path: `src/mate.rs:94-96` — `NoJournalMate` on
  encode failure AND on byte-compare mismatch. **Checks out.**
- Two-books verbs: `src/fabric.rs:686` (`Op::Observe`) and `:748`
  (`Op::Reconcile`). **Checks out.**
- The reconcile law is TESTED, not asserted: `tests/twobooks.rs:218`
  `reconcile_repairs_balance_and_marks_but_never_removes`, plus
  `:266` out-of-overage reconcile refused AND booked. **Checks out.**
- The load-bearing exhibit, `tests/mate.rs` (key-holding forger): the
  +7/−7 edit honestly encoded under the TRUE key passes decode alone
  and is refused by the mate — this is the tautology theorem
  reproduced on deadledger's own fold, and the referee confirms the
  code path is real (mate byte-compare, not an invariant re-run).
  **G2 authenticity: genuine.**

## 2. The hybrid verdict

Did pole + runner produce a ship stronger than both? Per scored
dimension:

| dimension | ledger (R2: 100) | deadband (R2: 97) | deadledger | verdict |
|---|---|---|---|---|
| fold integrity | keyed seal, ct_eq | n/a (Exhibit B victim) | same seal + journal mate | **stronger than both** — the mate closes what the seal alone cannot (tautology theorem) |
| conservation semantics | hard refusal only | audit drift | two-books: bounded overage, observer channel, reconcile-marks | **stronger than both** (STIR-03 generalized) |
| freshness pricing | none | ρ·F axiom | floor as booked cost, never verdict input | **equal to deadband, honestly scoped** |
| cost | decode ~µs | 4–8 µs path | mated load +192% | **weaker than ledger alone** — the price of the mate, booked not hidden |
| image | +16 B | +124 B | +912 B | **weakest of the three** — fault book + floor sections; honest, but it should be on next seam's agenda |
| fault record | none | drift signal | 128-record bound | **new surface** — the bound is the next seam's first customer |

**Hybrid verdict: CONFIRMED.** Deadledger is the first ship in the
tournament that is stronger than the sum of its parents on the seam it
was built for, and it paid visible, measured costs for the strength.
The 1834 archive-burn fail-closed test (`tests/mate.rs:136`, empty
archive refuses) is the kind of historical joke the referee cannot
penalize.

## 3. R3 go/no-go for the field

- **DEADLEDGER GO: CONFIRMED.**
- **SHIPSTREAM + SYNAPTIC STREAM: still conditional. Stream has still
  not delivered a house.** Stated as fact; no penalty invented; the
  conditional stands until stream docks.
- **Next Gauntlet: SEAM 2 — unbounded history.** Rationale: Seam 3
  (rho·F measurement) is already half-closed by deadledger's floor
  being cost-not-verdict, and referee/RD-SEAM23-BRIEF.md's STIR-07
  (Tape Archive Rotation — forget by demotion, not destruction) aims
  Seam 2 directly at the +912 B image and the 128-record bound. Seam 3
  follows as Gauntlet 3 with RD-brief experiments (CUSUM vs control
  chart on the deadband tree).

### GAUNTLET-SEAM2 acceptance tests (drafted)

- **G1 (bounded memory):** after N epochs with archival configured, the
  hot image size is O(recent state), NOT O(total history) — measured,
  with the archive mount as the only access path to demoted epochs.
- **G2 (auditability survives forgetting):** a fault booked in a
  demoted epoch remains provable after demotion (mount + verify) AND a
  forged archive record is refused — keyed seal extends to archives,
  no re-derivation credit (tautology theorem applies to summaries).
- **G3 (the trade is named):** the team states, in writing, what their
  scheme forgets and what it costs to prove a forgotten fact — per
  RD-brief finding #1 (every production system names its trade; the
  six teams never have).

## 4. STIR-06 table-note (formal, late)

scouts/STIR-06.md (split tally) is hereby TABLED. With deadledger's
mate machine-checking the counterfoil law (`NoJournalMate` on a key-
holding forger), the tally's thesis — authentication by possession of
the unforgeable half — is no longer a rival mechanism; it is adopted
doctrine. Sharpest remaining targets: shipwright and deadband, whose
folds remain self-contained truth (their Gauntlet locks key the image
but nothing outside the image holds the counterpart claim). A Seam-2
entrant that makes the ARCHIVE the counterfoil — keyed, demoted,
mountable — answers both STIR-06 and G1 above in one joint.
