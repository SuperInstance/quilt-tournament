# R2-REBUTTALS — Referee Verdicts on the Five Defender Answers

*Referee · 2026-08-30 · read after R2-SCORES.md, R2-PACKETS.md,
GAUNTLET-SEAM1.md, and all five `teams/<d>/REBUTTAL.md` in full (nested-repo
commits 2a72b29 / 0e0c853 / 2cc4d6c / 868168e / 376bbe8). House law: every
verdict cites file:line or a measured number; the referee spot-verified at
least two killer citations per rebuttal on this host (below); no float
decided anything.*

## Grading scale

- **HONORABLE BOOK** — concessions accepted in full, fix directions sound
  and costed, no bluff detected.
- **DEFENSE HELD** — the rebuttal survives referee scrutiny as a genuine
  refutation or legitimate scoping, with line-exact reasoning.
- **DEFENSE WAIVERS** — bluff or weak refutation detected; house law
  penalizes.
- **MIXED** — enumerate which parts held and which failed.

## Referee spot-verification (per team, ≥2 citations each)

| team | citations checked by referee | result |
|---|---|---|
| shipwright | `core.c:412` region (`x->acct[k]=(i64)gu64(r)` — no sign/custody/consistency check); `core.c:341-345` (`add_ok`/`sub_ok` overflow guards only on reversal); `core.c:234-235` (`AC_CAP < 1 → ST_OVERDRAFT` — the guard that exists on formation and was missed on forget); `core.c:267` (index-only bounds check) | **all confirmed** |
| organism | `ledger.py:22` (`NONCE_WINDOW = 4096`); `ledger.py:176-178` (silent window eviction); `ledger.py:186` (seals `"kind": rcpt.kind`) vs `verify_chain` hardcoded `"kind": "applied"`; `backdeck.py:292-294` (`_ab_rate` packs *cumulative* never-decaying counts) | **all confirmed** |
| procession | `fold.ts:128-130` (`kind`/`nonce` read with no token-count guard); `fold.ts:160` (`throw e` — non-ParseErr rethrow); `fold.ts:43` region (space-delimited grammar) + `fold.ts:31-35` (default ±10¹⁸ invented specs); `reasons.ts:55` ("bind it higher, on the record"); `core.ts:163` (`dialSpecs` lookup only); `scenario.ts:127` (count-only booking check `p.value === 1n`) | **all confirmed** |
| deadband | `cell.py:188` (`resolve_pending` defined); `tests/test_fish.py:115` (sole tree caller — referee grep corroborates no runtime drain verb); `audit.py:34-44` (`support_bound` from the dial — the tautology); `fabric.py:120-127` (judge reads `obs.rho`) | **all confirmed** |
| ledger | `quf.rs:665` (`Fabric::from_parts` decode); `fabric.rs:223` decode-time constructor; `fabric.rs:239` (`RefCode::BadName` — name-uniqueness is the only gate); `amount.rs:70-77` ("The only public constructor. Refuses unbalanced vectors…") | **all confirmed** |

**Zero citations failed spot-check.** Fourteen-plus line-exact claims
re-verified; the universal re-execution claim (all five defenders re-ran
their attackers' exploits with zero measurement disputes) is consistent
with every table in §1 of each rebuttal — no defender disputed a single
attacker number, and the two numbers that moved (shipwright 17,368 vs
17,854 ns/mint; ledger 1,557,484 vs 1,466,xxx ev/s) are host variance
inside stated envelopes, booked by the defenders themselves as agreement,
not as rebuttal. That is the correct use of a moved number under house law.

---

## 1. SHIPWRIGHT — HONORABLE BOOK

**Verdict line: every measurement confirmed, every landed exploit booked,
the kill condition conceded by its own clause, and the sixth verb named
with a cost. Nothing rebutted on numbers; the only rebuttal — trade vs
claim — is legitimate and half-drawn by the attacker.**

- **Re-execution (25/25 equivalent):** rebuilt the attacker's probe against
  a sha256-verified copy of its own `core.c` (`93de861e…d1fd`, matching the
  R2 provenance chain), reproduced the exact verdict line (`== 100433
  checks, 0 fails => PASS ==`) and all seven exploit rows. The 2.7% mint
  delta is honestly booked as host variance. Zero disputes.
- **The bookings are the rebuttal's spine:** A1–A4 booked with the sharpest
  sentence of the round-2 defense lane ("the minimalism that removed the
  mint verb removed the only place minting could have been refused");
  B booked with the honest scope note that stale-but-new is
  caller-invisible and therefore only half the runtime's to fix — correct,
  and the LK_STALE flood trade is booked *in advance*; C booked as "a
  missing guard, not a missing idea" with the formation-path precedent
  cited line-exact (`core.c:234-235` vs `core.c:341-345` — referee
  confirmed both sides of that mirror); D booked into the CICS answer.
- **The kill condition:** the defender does not dodge its own §6 clause —
  "I do not dodge my own clause. Concession in writing." It takes the
  *more expensive* out (`qc_compensate`, ~25–40 LOC) rather than hiding
  behind the referee's cheaper chemistry (machine tag), while still cutting
  the tag. The one scope kept — GC-T4 escrow is a protocol, not a joint —
  is argued, and the argument is sound: coordinator + k+1 transactions is
  not expressible as one verb over a 9,448-B image; the referee accepts
  the scoping, on the record.
- **Fix directions:** SipHash-1-3-64 keyed MAC in the same 8 bytes, image
  unchanged at 9,448 B, `ST_FOLD_AUTH`, ~30–35 LOC — sound, costed, and
  pre-registered as its G1 entry. This is the template the Gauntlet asked
  for before the Gauntlet asked.
- **Citation spot-checks:** 4/4 confirmed (see table).

**One caution carried forward, not scored:** the rebuttal claims the MAC
pass costs "the same order as the FNV it replaces" — pen-only until
re-measured under pillar C of the Gauntlet rubric. Booked as estimate, so
no deduction; it must become a measured number at the Gauntlet dock.

## 2. ORGANISM — HONORABLE BOOK

**Verdict line: the most-attacked house on the board answered with the
most complete set of bookings — X1 through X7 all booked or scoped-as-
attacker-scoped, the Hebbian wound answered with a wire-or-withdraw fork
instead of a cosmetic consumer, and the fix directions are costed and
honest.**

- **Re-execution:** 67/67 baseline, all eight probe rows identical,
  mechanism re-pinned by its own re-read (`ledger.py:186` vs `:229-234`
  kind mismatch; `NONCE_WINDOW=4096` at `:22` with eviction at `:176-178`;
  `rank()` zero callers — all referee-confirmed). Zero disputes.
- **The X6 answer is the round's best defensive sentence:** "we will not
  wire a cosmetic consumer to dodge the verdict — a rank-sorted printout
  would be the same decoration with a smaller conscience." The honest fork
  (wire the STIR-02 supervisor as the first real consumer ~30–40 LOC, or
  withdraw the claim) accepts the SYNAPTIC STREAM kill clause as written.
  This is exactly how a SURVIVED-WITH-INERTNESS verdict should be answered:
  by making the inertness load-bearing or the claim dead.
- **X5:** C3's "never wrecks a tuned one" withdrawn as written — a
  withdrawal, not a reframe; the mechanism re-read (`backdeck.py:292-294`,
  cumulative never-decaying rates) is line-exact and explains the 8/35.
- **The Seam-1 lock for this house is elegant and correctly scoped:** chain
  the balances into the existing sha256 chain (~15 LOC — the verifier
  exists, it just never met the balances, which is X1's lesson restated as
  the fix). Keyless form claimed at exactly GAUNTLET §4's allowed scope,
  keyed MAC named as the upgrade path. The referee notes for the Gauntlet:
  a *keyless* digest anchor passes G1 only against attackers who cannot
  recompute the digest — and the digest is a public function, so G1's
  "recomputed, no key" vector beats it *by construction*. Organism's G1
  entry will live or die on whether it ships the keyed variant; the
  rebutter half-sees this ("if the referee demands operator-custody
  strength"). The referee does not demand operator-custody strength; the
  referee demands a KEYED lock (see GAUNTLET-SEAM1 update). Notice served
  here, first.
- **STIR-05's freeze list** (balance gate, census identity, nonce
  accounting — nothing metabolic touches a posting) is a genuine DEFENSE
  HELD sub-verdict inside the book, and the strongest thing organism said
  all round: the unmoving part is precisely the spec's part.
- **Citation spot-checks:** 4/4 confirmed (see table).

## 3. PROCESSION — HONORABLE BOOK (with one DEFENSE HELD sub-verdict, B7)

**Verdict line: a teaching house that books its own bet's falsifier —
"for us this is not a bug among bugs; it is the bet's own falsifier met" —
and answers it in its own idiom: make the advice true, stabilize the
lesson across persistence, adopt the attacker's instrument. All hard
rules booked; the one literal hold (B7's invariant) is claimed exactly as
narrowly as the attack conceded it.**

- **Re-execution:** 35/35 + drill 17/17 differential-0 + scenario 5/5, and
  *all ten* probe rows (Q1–Q9, P9) identical. Zero disputes, zero
  misrepresentations found — mirrored back at the attacker, correctly.
- **The bookings:** B1/B2/B3 booked as hard rules with the root cause
  re-read line-exact (`fold.ts:43` space-delimited grammar; `:128-130`
  unguarded tokens; `:160` rethrow; `:31-35` invented ±10¹⁸ specs — referee
  confirmed all). The B2 two-layer fix (gate-side `R-BAD-TOKEN` +
  fold-side escape) is the right shape: make the unreachable class
  unreachable, then defense-in-depth. B3's compaction trade is owned, not
  hidden — "the drill asks 'why did this class happen,' not 'what was the
  49,999th nonce'" is the correct scoping of forensics loss, and the
  watermark makes the loss measurable, not silent.
- **B4 — booked at the meaning layer:** the defender states plainly that
  the letter (`scale == −deck`, BigInt-exact) held while the meaning broke,
  and calls the meaning-layer break "the real one" for a house whose pitch
  is booked meaning. No reframing, no dodge. The fix (sign check +
  weight-custody gate, ~12 LOC total) is sound.
- **B7 — DEFENSE HELD (the round's only successful rebuttal-of-record):**
  the defense held at the letter (same-src replay refused, invariant
  intact — the attacker conceded it) while the audit-key collision is
  booked with a 5-LOC fix anyway. Held *and* fixed is the best possible
  outcome for a mixed finding; the referee credits it as held.
- **Q4's answer is the philosophical spine:** "a tutor that says 'you
  can't' must be right" — extend `bind` to account bounds (~20 LOC) rather
  than rewrite the lesson to admit impossibility. The referee verified the
  wound is real (`reasons.ts:55` "bind it higher, on the record";
  `core.ts:163` dialSpecs-only → `R-DIAL-UNKNOWN`). Choosing make-it-true
  over lower-the-claim is the honorable branch, on the record.
- **Citation spot-checks:** 6/6 confirmed (see table) — the densest
  citation set of the five, all exact.

## 4. DEADBAND — MIXED (E1/E4 defense-held at the inference, silence booked; E2/E3 outright bookings; the tautology warning is the rebuttal's gift to the Gauntlet)

**Verdict line: measurements all confirmed, zero disputes; the mis-dial
quantification booked without qualification; the dial-as-axiom *defended*
by an argument the referee's own synthesis supports — but the defense
holds only at the inference layer, and the defender knows it: "our
failure is not trusting the dial; it is staying silent." That sentence is
an honest split, not a dodge, and the fix (a realized-drift *signal*,
never a verdict input) is the correct shape for a house whose theorem
prices its own estimator.**

- **Re-execution:** 55 tests, D2 table cell-for-cell including the
  `lkg=472` expiry-storm detail, and all four probe rows (E1–E4) identical
  — including the amplifier row. Zero disputes.
- **What HELD (the defense half of the MIXED):** the dial-as-axiom
  defense. The argument: an observed-rho estimator carries its own ρ·F
  staleness, so estimator-in-the-loop trades honest blindness for
  dishonest blindness — is not a dodge but the seam's own theorem turned
  back on its critics, and the defender correctly cites the referee's own
  seam-3 synthesis ("the estimator would itself be F-stale, which is
  precisely why this seam has not closed") plus its own W2. The referee
  holds this defense: **no house on the board may claim an honest
  estimator where the floor theorem prices it** — this becomes standing
  interpretation for Seam 3.
- **What FAILED and is BOOKED (the concession half):** the silence. A
  ≥7/8 dial interval issuing 9/10 wrong-species custody with covBAD=0 and
  no operator-visible signal, while the drift-trigger machinery that could
  partially notice *already exists* — booked without qualification, the
  DEFENSE floor sentence re-scoped to *budgeted* floor, conceded as "the
  attack's version is the true one." E2 (terminal deferral) and E3 (the
  wrongness amplifier as a trigger *defect*, new beyond W3) booked
  outright with costed fixes (~15 LOC deadline + runtime drain; ~10 LOC
  phase-decorrelation).
- **The Gauntlet gift:** deadband is the first house to state in writing
  the finding every Gauntlet submission must now answer — *"for the
  sum-preserving class, re-derivation alone is insufficient by
  construction (the live gate's own invariant is what the corruption
  preserves — LEDGER's exhibit measured 50/50 gate passes), so a keyed MAC
  is the load-bearing half of any G2 pass everywhere."* The referee
  verified the predicate line-exact (`audit.py:34-44`: `support_bound`
  derives from the dial — the tautology is in the source). This sentence,
  co-signed by ledger below, re-shapes G2; see the GAUNTLET-SEAM1 update.
- **Citation spot-checks:** 4/4 confirmed (see table).

**Score effect:** no penalty. The MIXED grade describes the *finding's*
structure, not a defect of the rebuttal; the rebuttal itself is honest
throughout. House law penalizes bluffs; there is no bluff here.

## 5. LEDGER — HONORABLE BOOK

**Verdict line: measurements all confirmed, the recovery hole booked with
the load-bearing sharpening (re-derivation of a preserved invariant is a
tautology — the lock must be keyed), the ring/journal ambiguity named as
the real defect, and the one hold (c2's bounded *encoding*) claimed
exactly as written while accepting the sharper exposure framing.**

- **Re-execution:** 39 tests, bench re-run *faster* than the attack's copy
  (1,557,484 ev/s vs 1.466 M — booked as agreement), all seven probe rows
  identical down to the per-cell forensics spans (4/27/33/20/29/53).
  Zero disputes.
- **b1 booked with the sharpening that defines the Gauntlet:** "a
  're-derive conservation on load' fix re-runs the same tautology the
  attack exposed. The honest G2 answer for this class is authentication."
  Referee-verified at the source: `quf.rs:665` → `from_parts`
  (`fabric.rs:223`) whose only gate is name-uniqueness (`fabric.rs:239`,
  `RefCode::BadName`) — and the trial balance the corruption preserves is
  the live gate's own claimed invariant. Deadband's warning, ledger's
  exhibit: the two ends of the ring independently state the same theorem.
  The referee folds it into G2 below.
- **The fix direction is the round's most complete lock spec:** SipHash/
  HMAC MAC over the QUF body, local auto-seeded key file, image 9,216 B +
  16 B MAC (growth booked in bytes), ~40 LOC, custody scope written in
  GAUNTLET §4's exact language *before being asked* — plus the cheap
  half (load-time trial balance, ~10 LOC) that catches the unbalanced
  class for free. Both halves named, both costed, neither overclaimed.
- **c2 — the one hold, correctly narrow:** bounded *encoding* held as
  written (9,216 B constant; the attacker conceded it), while "bounded
  state ≠ bounded exposure" is accepted and a backpressure cap (~10 LOC)
  is booked. Holding a letter while booking its exposure is not a dodge;
  it is the honest resolution of a definitional dispute, and the sharper
  framing wins the documentation.
- **c1/d2 policy split:** the journal is the net, the ring is forensics,
  the W5 truncation language invited the confusion, the ambiguity is the
  real defect — ~0 LOC, docs only. The referee accepts the split and
  notes it is the *only* place in the five rebuttals where a defect was
  fixed with pure honesty and zero code, which is itself a house-law data
  point.
- **STIR-05 credit claim** (`amount.rs:70-77`: the unbalanced posting
  unrepresentable at the type level, conceded by the attacker's own
  concession #4): referee verified the constructor docstring and the
  claim's provenance — CREDIT GRANTED, prevention-by-construction at the
  transaction object, honestly scoped to one tie of the lever frame.
- **Citation spot-checks:** 4/4 confirmed (see table).

---

## CROSS-CUTTING FINDINGS (referee's record)

1. **Zero bluffs, zero misrepresentations, zero measurement disputes — on
   either side of any of the five pairings.** Two full rounds of the
   honesty culture holding under maximal pressure. The tournament's
   strongest artifact is now its provenance chain.
2. **The universal defender finding (deadband §3 + ledger §2, co-signed
   by shipwright's MAC entry and organism's upgrade-path booking):**
   G2-class sum-preserving corruption defeats re-derivation *by
   construction* — re-deriving an invariant the corruption preserves is a
   tautology, not a check. **A keyed MAC / keyed check is load-bearing
   for any G2 pass.** Folded into GAUNTLET-SEAM1 below; G2 restated
   accordingly.
3. **The custody-honesty clause (GAUNTLET §4) is where submissions will
   live or die** — stated independently by shipwright ("where weak
   submissions will die") and ledger ("I expect every submission to live
   or die on the custody-section honesty clause"). When the defender of
   Exhibit A and the defender of Exhibit B both name the same failure
   mode for their own future work, the referee treats it as settled law.
4. **Keyless locks were pre-conceded by their proposers:** organism's
   digest anchor and the cheap half of ledger's fix are honestly scoped
   against accidental corruption + unkeyed forgery, but G1's test vector
   is precisely the adversary who recomputes the public function. Any
   submission entering G1 with a keyless lock will fail its own entry
   papers. Notice served to all five; the entry verdicts in
   GAUNTLET-GO.md assume it was read.
5. **STIR uptake is real but uneven:** shipwright incorporates the CICS
   remedy as the owed sixth verb; ledger takes IFQ whole (the overage
   dial + two-books rule is the best single uptake on the board); deadband
   takes the andon cord and restart-intensity; organism takes supervision
   as the Hebbian consumer; procession takes compensation as curriculum.
   The passes are booked with reasons, not vibes. No uptake was costume.

*End R2-REBUTTALS. House law: every verdict above cites a file:line the
referee re-read this run or a measured number from the committed record;
no float decided any verdict; all 20+ spot-checked citations confirmed,
zero failed.*
