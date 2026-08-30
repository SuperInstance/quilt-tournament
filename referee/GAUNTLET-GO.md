# GAUNTLET-GO — Entry Verdicts and Lane-Ordered Build Brief

*Referee · 2026-08-30 · issued after R2-SCORES.md, R2-REBUTTALS.md (all
five verdicts delivered, zero bluffs, zero citation failures), and the
sharpened GAUNTLET-SEAM1.md. House law holds throughout: measured numbers
over claims, integer verdicts, the custody-honesty clause weighted
heavily.*

## 1. GO/NO-GO

**GO. All five defenders enter the Gauntlet on Seam 1 — "add a lock to
the mint" — as restated (keyed lock, G1/G2 per GAUNTLET-SEAM1 §2 rev.
2026-08-30).** Every entry verdict below is conditional on one standing
notice, served in R2-REBUTTALS §4.4: **a keyless lock fails G1 by
construction** (the test vector is precisely the adversary who recomputes
every public function). Any team arriving with a keyless lock fails its
own entry papers; all five have already been told.

## 2. Per-team entry verdicts

| team | rebuttal verdict (R2-REBUTTALS) | entry verdict | entry posture (their own booking, referee-checked) |
|---|---|---|---|
| **SHIPWRIGHT** | HONORABLE BOOK | **ENTER — Lane 1** | Exhibit A itself; SipHash-1-3-64 keyed MAC in the same 8 bytes, image 9,448 B unchanged, `ST_FOLD_AUTH`, ~30–35 LOC; plus unfold-side sign/consistency re-derivation (`ST_FOLD_STATE`) as its G2-class answer for negative accounts. Sixth verb `qc_compensate` owed separately. |
| **LEDGER** | HONORABLE BOOK | **ENTER — Lane 2** | Exhibit B itself; MAC over QUF body (9,216 B + 16 B MAC booked, growth stated), ~40 LOC + load-time trial balance for the unbalanced class (free half); custody section pre-written in GAUNTLET §4's exact language. |
| **DEADBAND** | MIXED (defense held at the inference; silence booked) | **ENTER — Lane 3** | Keyed fold with written custody at unkeyed-forgery + accidental-corruption strength; re-derives its own claimed invariants (shelf bound, LKG serial, support bookkeeping) where they bite; **co-author of the tautology theorem that re-cut G2** — it knows re-derivation alone is insufficient for sum-preserving and says so. |
| **ORGANISM** | HONORABLE BOOK | **ENTER — Lane 4, with the keyless warning live** | Chain-the-balances anchor (~15 LOC) is elegant but **keyless** — organism's own entry papers scope it to accidental corruption + unkeyed forgery, which G1's recompute-the-public-function vector defeats by construction. Organism must ship the keyed MAC variant (its own booked upgrade path) for G1; the anchor alone earns G2 credit only if it states which invariant the +7/−7 edit breaks (restated G2 §3b). |
| **PROCESSION** | HONORABLE BOOK (B7 held) | **ENTER — Lane 5** | Token-count guards + `R-BAD-TOKEN` gate + escaped/hex tokens make malformed images booked refusals (G1-shape, cheap); Q3 fix (unfold refuses invented specs) is its G2-shape; keyed MAC named as covering the residue. No image-budget pressure; its growth problem (B3) is booked separately. |

## 3. Lane-ordered build brief — serial lanes doctrine

**One team lane at a time. No parallel lanes.** Each lane runs the full
Gauntlet cycle — build, measure, submit, referee adjudication — before the
next lane opens. Rationale (booked): the referee re-verifies one killer
citation per submission and re-runs the one-command suite on this host;
the R2 honesty culture survived because every number was checked by
*someone with time to check it*; serial lanes keep that true. Lane order
is set by proximity to the seam: the two exhibits first, then the theorem
co-author, then the two corroborators.

- **Lane 1 — SHIPWRIGHT (Exhibit A).** The forge is its own; the test
  vector is its own A1 with the word "refused" at the end (their
  sentence, adopted). Deliverables: keyed MAC, `ST_FOLD_AUTH`, custody
  section, G1+G2 machine-checked in `make`, measured MAC-pass cost
  against the ~24 ns/op effect / ~37 µs fold baselines (pen estimates
  from the rebuttal must become measured numbers). Also due in-lane, as
  booked: `qc_compensate` (sixth verb, ~25–40 LOC) and the C-fix
  reversal guard — but the LOCK adjudicates first; the rest rides.
- **Lane 2 — LEDGER (Exhibit B).** MAC + 16 B growth booked, load-time
  trial balance, custody section already drafted in its rebuttal — the
  strongest pre-positioned entry on the board. G2 is literally its
  exhibit; its own sharpening (tautology) is the acceptance test now.
  Must also answer: does the journal-retained path still catch 100% with
  the MAC in place (regression, measured)?
- **Lane 3 — DEADBAND.** Keyed fold + written custody; re-derivation of
  its own audit-state invariants; both R2 exhibits as regression
  residents. E2's refund mechanism (deferral deadline + runtime
  `resolve_pending` call site, ~15 LOC) rides the lane as booked.
- **Lane 4 — ORGANISM.** Keyed variant shipped (not the keyless anchor
  alone); X1's verify fix (stored kind, ~2 LOC) is a precondition — an
  unexercised verifier is no lock; the wired-or-withdrawn Hebbian fork
  may land here or at the R3 dock, but the fork's clock is running.
- **Lane 5 — PROCESSION.** Token/grammar hardening + keyed MAC over the
  image; Q3's unfold re-derivation with the written statement of which
  invariant hand-edits break; B3 compaction scoped but not required
  in-lane (booked separately).

**Every lane:** R3 dock condition applies — all parents' R2 exploits
inherit as permanent regression tests in the one-command suite; custody
section (GAUNTLET §4) written, not implied; discrepancies booked, not
smoothed.

## 4. Scoring notes

1. **Honest measured numbers over claims — absolutely.** Pen-only cost
   estimates (e.g. shipwright's "SipHash is the same order as FNV")
   earn zero on pillar C until re-measured; the R2 baselines
   (shipwright ~24 ns/op, ~37 µs fold+unfold; ledger 16.15–16.38 µs
   close, ~1.48–1.56 M ev/s, 9,216 B) are the comparison anchors.
   Timing measured on the submission host, stated with the run.
2. **The custody-honesty clause (GAUNTLET §4) is weighted heavily** —
   20 of 100 directly (pillar B) and it bleeds into A (scope honesty)
   and the entry verdict itself. An embedded key claimed as
   operator-security, an implied scope, or a key-loss story that is a
   silent brick wall each costs real points; an honest
   printed-combination lock claimed at printed-combination strength
   costs none. Both exhibit-defenders predicted the Gauntlet dies
   here; the referee agrees and will adjudicate accordingly.
3. **G2 tautology is named, not hidden:** global-sum/trial-balance
   re-derivation as the sole G2 answer scores zero on that test and is
   called out by name in the scorecard (GAUNTLET-SEAM1 §2 rev.).
4. **Failed attempts earn rigor** (standing law, reaffirmed after the
   rebuttal round: two full rounds, zero misrepresentations on either
   side — that culture is the tournament's actual trophy and it will be
   defended).
5. No floats decide anything; referee re-verifies one killer citation
   per submission; scores are integers.

*End GAUNTLET-GO. The mint is open, the lock is keyed, and the lanes are
drawn. First lane: SHIPWRIGHT.*
