# R2-PACKETS — Cross-Attack Referee Assignments

**Referee lane · 2026-08-29 · Shell 1 (attack).** Read in full before any
team writes a single line of attack. This document is the referee's standing
order to the six attackers; it does not itself contain the attacks. The
attacks land as `ATTACK-R2.md` in the **attacker's own directory** — never in
the target's dir. The target's dir is read-only to every attacker.

**House law, stated once, applies to every packet:**

- **No float decides any verdict.** Every claim in an attack is falsifiable
  and carries either a measured number, a file+line citation, or a booked
  concession. Where an attacker cannot measure, it must *concede in writing*
  rather than hand-wave.
- **Failed attacks earn rigor; misrepresentation loses points.** A false
  accusation ("your fold loads corrupt state") is worse than a correct
  concession ("I could not break X; here is what I measured and why it held").
  The rubric already says so: defense-holds 15, honesty & clarity 10.
- **Evidence at every shell.** Depth rule from CHALLENGE.md: no team may skip
  a shell it is assigned; evidence or booked concession at every step.
- Every number in this document came from the target's own `DEFENSE.md`,
  `WEAKNESS.md`, `README.md`, or `MEASURED.md`, read in full by the referee
  before writing this packet. Attackers reproduce the numbers themselves; they
  do not copy them.

---

## 0. State re-check (relaunch after the z.ai outage)

- **Partial output found:** `teams/organism/attack-r2/probe.ts` — a 12-part
  measured probe (P1–P12) ORGANISM already ran against PROCESSION before the
  lane died. It is a probe harness, not a finished attack. Packet 2 orders
  ORGANISM to consolidate this probe into `ATTACK-R2.md` (formatted, verdicts
  written, numbers kept, dead-ends marked as concessions). No other
  `ATTACK-R2.md` / `COUNTER-R2.md` exists. No `R2-PACKETS.md` existed.
- **STREAM has not delivered.** Its dir holds only `rtl/sc_cell.v` (914 lines,
  salvaged, self-described "known-buggy"), with **no `DEFENSE.md` and no
  `WEAKNESS.md`**. Per CHALLENGE.md the field is six; but an attacker without a
  house cannot be held to it, and a target without a defense cannot be
  attacked honestly. **STREAM's packet is skipped** until it delivers a
  `DEFENSE.md` + `WEAKNESS.md` + a runnable suite. When it does, it attacks
  the champion's gauntlet line, not this ring.
- **Round-robin is therefore five packets** (stream is neither attacker nor
  target this round):

  | packet | attacker | target |
  |---|---|---|
  | P1 | SHIPWRIGHT (C) | ORGANISM (Python) |
  | P2 | ORGANISM (Python) | PROCESSION (TS) |
  | P3 | PROCESSION (TS) | DEADBAND (Python) |
  | P4 | DEADBAND (Python) | LEDGER (Rust) |
  | P5 | LEDGER (Rust) | SHIPWRIGHT (C) |

  The ring closes: shipwright→organism→procession→deadband→ledger→shipwright.

---

## PACKET 1 — SHIPWRIGHT attacks ORGANISM

**Target files to read fully before attacking:** `teams/organism/DEFENSE.md`,
`teams/organism/WEAKNESS.md`, `teams/organism/MEASURED.md`,
`teams/organism/README.md`.

**Deliverable:** `teams/shipwright/ATTACK-R2.md`.

### (a) Run the target's suite yourself; record YOUR OWN numbers

```bash
cd teams/organism
python3 -m pytest tests/ -q        # they claim 67 tests
python3 -m cellcore.measure        # rewrites MEASURED.md — record BEFORE and AFTER
python3 -m cellcore.demo           # the conformance demo run
```

Reproduce and re-state, in your own words and your own numbers, at least:
- C1 asymptote: `float_halving_hits_zero_at_step == 1075`, `mass_steps_to_floor == 58`,
  `mass_never_zero == true` (their MEASURED.md `asymptote`).
- C2 healing: `one_tick_heals == true` and `above_deadband_healed == trials`
  across deadbands {1,3,7}.
- C3 adaptation: naive frozen **29%** vs adapted **40%** join rate (`adaptation`).
- C5 fold: `quf_bytes_waves [700376, 766948, 820161]`, `fold_bound_holds == true`.
- C6 gauntlet: 67/67 pass, census conserved after every attack.

Any discrepancy between your run and their published number is a finding in
itself. Record the host line and the wall time of `measure` (they claim 6.6s).

### (b) One real exploit vs their adversarial claim (C6)

C6 claims: *"any input that produces an exception escaping a verb, a silent
state change, or a census break"* is the falsifier — "everything refused or
contained, never silent." Attempt **one** of these, and only claim what you
actually produce:

- **The nonce-window replay (their W5, "convention, not a mechanism").**
  Recycle a nonce older than the 4096 window via a *direct local `effect()`
  call* (not a flit). W5 admits the per-link FIFO guard "holds ONLY for
  flit-borne replays." If a direct call re-applies, C6's "double-move refused"
  does not hold for the local API — a booked reason gone silent.
- **Census break under the label-bus mirror noise (their W8).** Exercise the
  4-ary flit against all four consumers (XID-MATCH, LEDGER-SCALE, AUDIT-CAPTAIN,
  NIGHT-CRON) and hunt for a `mirror:*` accounting drift that changes a
  custody census.

Do **not** pad the attack with the asymptote/float contrast — that is their
strongest, most reproducible claim (C1), and attacking it will cost you rigor
unless you actually exhibit a mass reaching zero by decay.

### (c) Attack the deepest bet

Their deepest bet: *"a runtime that can only be changed by booked, receipted,
exactly-counted events is the one you can trust when it changes itself"* —
and its engine, *"conservation emerges from metabolism."*

**Booked concession available to them** (their own W2): conservation does not
emerge; it is enforced by `ledger.apply` (GC-D6: balance is an axiom). The
metabolism story lives *on top of* the gate. Attack the gap between "life is
the audit trail" and what actually decides a verdict:

- **Disable the Hebbian/metabolism layer and re-run conformance.** Their W3
  admits `rank()` is the only consumer of masses and "no conformance verdict
  depends on it." If verdicts are byte-identical with the biology off, the
  organism is a balanced-books engine wearing a biology costume — the deepest
  bet is decoration, and you have the measurement to say so. That is the
  counterexample, not a quote.
- Attack C1's "asymptote" as a **renamed zero** (their W3 concedes: dormancy
  and death "differ only in the future"). If nothing else reads the mass, the
  floor at 1 is a promise about a quantity nothing consumes.

### (d) Drive the two most damaging WEAKNESS entries further

1. **W3 — "the Hebbian layer is, today, mostly potential energy."**
   Measure it: run conformance with `rank()`/masses stubbed to a constant and
   show zero verdict delta; then show the A/B controller (W4) is the only
   thing left, and it was tuned on their own scenario (their `final_wins`
   still contains `1`). Quantify the costume: which fraction of the ~10k-line
   organism is load-bearing vs pheromone?
2. **W5 — "bounded structure, growing values, and the QUF is fat."**
   Push the fold past their reported 4,200 fish (they say growth is
   *decelerating*, not plateaued). Run to true saturation and report the
   actual QUF byte ceiling — or show it never plateaus. Then state the
   nonce-window replay hole as a measured exploit (from (b)), not a rumor.

---

## PACKET 2 — ORGANISM attacks PROCESSION

**Target files:** `teams/procession/DEFENSE.md`, `WEAKNESS.md`, `README.md`,
`TUTORIAL.md`. **Note:** ORGANISM already holds a 12-part probe at
`attack-r2/probe.ts` from before the outage — consolidate, do not discard.

**Deliverable:** `teams/organism/ATTACK-R2.md`.

### (a) Run the target's suite yourself; record YOUR OWN numbers

```bash
cd teams/procession
npm install
npm test          # they claim 35 tests
npm run drill     # the semantic-differential gate (should print differential = 0)
npm run scenario  # back-deck conformance demo
```

Reproduce: C1 (17/17 refusal codes registered), C2 (tutor/engine
differential = 0), C4 (9/9 executable docs), C6 (flood: 2,000 committed +
100 refused at bound, 233 ingress deferrals, scale == −deck). Re-run the
2,100-landing flood yourself and record the three counts.

### (b) One real exploit vs their adversarial claim (C5/C6)

C5 claims fold round-trip is byte-exact and *"never a throw"* over 500
single-char mutations; C6 claims 5/5 attack classes contained. The existing
probe already found candidate breaks — **now you must land exactly one as a
measured exploit, not a screenshot:**

- **Negative-weight fish (probe P9, already observed).** Land a fish with
  `weightTenPounds < 0` and show count and weight decouple: 3 fish landed,
  0 tenths booked, scale floor 0 only blocking the *first* negative. If it
  reproduces, C6's "phantom/overflow refused" does not cover the sign axis —
  the gate checks balance and bounds, never sign.
- **Totality hole (probe P1).** Craft a fold image their single-char fuzz
  cannot reach (a whole-token deletion, e.g. a missing nonce) and show a raw
  `throw` escaping `unfoldCell` — a falsifier of C5's "never a throw, never a
  partial load."
- **Fold round-trip break on reachable input (probe P2).** A nonce containing
  a space books a legal refusal, but the resulting fold then *refuses its own
  unfold* (`R-CORRUPT-STATE`) — `decode(encode(x)) != x` on a reachable
  input, breaking C5's canonicality claim.

Pick one; run it to a clean PASS/FAIL with the exact input, output, and any
thrown error type.

### (c) Attack the deepest bet

Their deepest bet: *"make the explanation the artifact — one semantics
(`reasons.ts`) that is simultaneously the error message, the booked reason,
and the tutor's lesson; drift measured = zero."*

- **The differential is a compiler self-consistency check (probe P11).**
  Show that C2's "0 divergences" compares the tutor's hand-written context
  against `explain()` **on the drill's own move** — the test contains zero
  bits about any operator. Then exhibit two reachable paths that emit
  *different* text for the *same* refusal code: "one semantics" is one
  *table*, not one *message*.
- **The actual bet is unmeasured (their W9).** "We taught, but did not
  measure, learning." The champion should be able to point at the
  interaction. Demand the number; if none exists, that is the concession the
  deepest bet rests on.

### (d) Drive the two most damaging WEAKNESS entries further

1. **W3 — "the ledger is append-only but NOT bounded."** Spam refused nonces
   and measure ledger growth (probe P7 already: 50,000 phantom arrivals →
   tens of thousands of refusal entries, ~KB-scale fold, O(ledger) unfold).
   Turn it into a bounded-state falsifier: "bounded accounts, unbounded
   history — the R4 bounded-state harness catches this." Give the bytes-per-
   refusal and the asymptotic slope.
2. **W1 — "the one-semantics guarantee is enforced, not proved."** Fuzz the
   verbs with garbage arguments (unknown cell id, malformed posting sets,
   type-wrong account values) hunting for a thrown `Error` they admit exists
   on the fabric-misuse boundary. Count how many distinct thrown paths you
   find that are *not* in `ALL_REFUSAL_CODES` — that is the C1 coverage
   denominator they did not exercise.

---

## PACKET 3 — PROCESSION attacks DEADBAND

**Target files:** `teams/deadband/DEFENSE.md`, `WEAKNESS.md`, `README.md`.

**Deliverable:** `teams/procession/ATTACK-R2.md`.

### (a) Run the target's suite yourself; record YOUR OWN numbers

```bash
cd teams/deadband
python3 -m pytest tests/ -q        # they claim 55 tests
python3 benches/measure.py         # the D2 frontier table + D1 coverage numbers
```

Reproduce: D1 `covBAD == 0` across all 8 policy×scenario rows; D2's frontier
table (audits/cost/deferred/accepted per policy); D3's adversarial arm
(static T=4 → 0 accepted/60 deferred at 4× drift; drift-triggered eps=1 →
40/40); the exhibited floor `rho*F = 1/2 * 2 = 1`; D5 `state < 200 slots`
under 10,000-transaction pressure. Record every cell of the D2 table from
your own run, not theirs.

### (b) One real exploit vs their adversarial claim (D1/D5)

D1 claims *"zero verdicts were issued whose drift support >= the needed
margin"* — `covBAD = 0` everywhere, "never answered a question its freshness
window could not support." D5 claims bounded state. Attempt **one**:

- **Mis-dial rho (their W2) and show the coverage number is a dial artifact.**
  `rho` and `margin` are operator assertions, not estimates. Set `rho`
  optimistically low (or `margin` high), re-run the scenario, and show the
  runtime issues verdicts whose support — computed against the *realized*
  drift you induce — exceeds margin. If `covBAD` stays 0 only because
  "support >= margin" is checked against the *budgeted* rho, then D1's
  "100% coverage" is tautological: it refuses whenever its (possibly wrong)
  dial says to, and the world's true staleness is invisible. That is a
  measured exploit of the claim's premise, not its conclusion.
- **Burst arrivals between audits (their W5).** A correlated multi-tote flip
  or a burst landing inside the F=2 window that their single-horizon bench
  never generated. Show a `covBAD > 0` or a silently-stale accept.

### (c) Attack the deepest bet

Their deepest bet: *"the floor is everyone's constraint; we are the only team
that prices it, schedules for it, and refuses on it by construction —
freshness is a budget we spend."*

- **The floor is a theorem with asserted inputs (their W2 + W5).** The claim
  "we sit on it exactly" is true only against *dialed* rho, not *realized*
  drift — W5 concedes this in words ("the floor we sit on is the budgeted
  floor, not the realized one"). Make it a counterexample: run two different
  rho dials on the same realized-drift world and show the runtime happily
  "sits exactly on the floor" at two different heights. The floor is not a
  fact about the world; it is a fact about the dial.
- **The Switch Test lives on (their W1).** Deadband cannot prove a rival who
  answers in the `rho*F >= margin` regime is lying — "refusal is all anyone
  can honestly do." Attack the consequent: a runtime whose only honest
  output in that regime is refusal has *no positive claim at all* there —
  its superiority is entirely negative. Is "we refuse more honestly" a
  *champion* thesis, or a surrender that refuses to call itself one?

### (d) Drive the two most damaging WEAKNESS entries further

1. **W2 — "rho and margin are dials, and dials are trusted inputs."**
   Quantify the silence: sweep rho across a range on one fixed world and
   measure the interval of rho values for which the runtime issues verdicts
   with realized-drift support > margin. The wider that interval, the more
   of "exactly honest" is dial-faith. Book the width as a number.
2. **W3 — "liveness price: deferral storms."** Push the D3 static row
   (0 accepted / 60 deferred) and measure the *productivity cliff*: at what
   drift does the honest scheduler produce zero, and how many audits does the
   drift-triggered rescue cost? State the trade as a measured frontier, then
   ask whether "booked nothing" is a defense or an admission that the
   philosophy has no answer inside the floor.

---

## PACKET 4 — DEADBAND attacks LEDGER

**Target files:** `teams/ledger/DEFENSE.md`, `WEAKNESS.md`, `README.md`.

**Deliverable:** `teams/deadband/ATTACK-R2.md`.

### (a) Run the target's suite yourself; record YOUR OWN numbers

```bash
cd teams/ledger
cargo test                        # they claim 39 tests
cargo run --release --example bench   # the wall-clock numbers DEFENSE.md cites
```

Reproduce: D1 (138 invariant evals per catch-batch; 34.0 checks/event;
16.26 µs avg batch close; 1.48 M events/s; 102 consecutive zero trial
balances); D2 (5,000 batches / 227,426 journal entries replayed bit-
identically in 23.5 ms); D5 (QUF image 9,216 bytes, identical at batch 300
and 2,000); D6 (13 adversarial tests, all five classes). Re-run the bench
and report your own throughput, close time, and replay time.

### (b) One real exploit vs their adversarial claim (D6/D1)

D6 claims all five classes contained "never silent," and D1 claims *every*
transition is audited before commit. Attempt **one**:

- **Compensating corruption evades the trial balance (their W4, already
  machine-checked in their own test).** Inject two flips that preserve the
  sum (`+7` on one `book`, `−7` on another). Their own D6 table admits these
  "evade the gate and are caught **only** by journal replay." The exploit is
  the *conditional*: with the external journal absent or truncated (W5), the
  audit net is the last line — and it has a known hole. Demonstrate the hole
  *without* the journal and show the gate passes corrupted state. If you can
  make the gate accept a compensating corruption with no journal to catch it,
  D1's "every transition audited" is false in exactly the recovery mode their
  philosophy advertises.
- **Same-epoch arrival race double-books custody (their W2).** Catch and sort
  one fish inside a single epoch and show it appears in both `quarantine`
  and `inflight` until a forget reconciles — "the books never lie, but for
  that epoch the fish appears in two custody places."

### (c) Attack the deepest bet

Their deepest bet: *"the book is the program — conservation is the
primitive; state = fold(journal), byte for byte; no rival without a journal
can offer byte-exact recovery."*

- **The recovery protocol's single point of failure is the journal itself
  (their W4 + W5).** `state = fold(journal)` makes the journal the *only*
  source of truth. Corrupt it (or truncate it by policy — W5) and the
  entire "reload + replay" story collapses; the trial-balance gate is the
  last line and W4 proves it leaks. The bet "replayable from any point" is
  only as replayable as the journal is retained — and the audit ring
  forgets (64 entries/cell), so "bounded" and "complete history" are
  opposites they chose between. Counterexample: show that after ring
  saturation the *balances* still claim correctness while the *history*
  needed to prove it is gone — the book is the program, and the book has
  been overwritten.
- **The freshness floor is self-imposed and unbeatable (their W1).** "We do
  not claim to beat it; we claim to *book* it." Attack the claim: booking
  staleness as an `inflight` account balance is elegant, but a per-event
  commit answers "how many coho right now" correctly while ledger's answer
  is F-stale by construction. Is "we book our blindness legibly" a *win*, or
  an honest admission that batch pays for totality with correctness-at-the-
  instant?

### (d) Drive the two most damaging WEAKNESS entries further

1. **W4 — "compensating corruption evades the trial balance."** Turn the
   parenthetical into a measured table: for a range of journal truncation
   points, how many of your compensating-corruption injections does the gate
   pass vs the replay catch? The result is the *audit-net coverage as a
   function of journal survival* — the number that decides whether
   "audit-first" means anything when it matters.
2. **W5 — "the audit ring forgets."** Measure the forensics horizon: after
   how many batches is a given transaction unrecoverable from the ring?
   Then state the contradiction in their own terms — "bounded" and "complete
   history" are opposites, and they chose bounded — and ask whether a boat
   with a disk should ever make that trade.

---

## PACKET 5 — LEDGER attacks SHIPWRIGHT

**Target files:** `teams/shipwright/DEFENSE.md`, `WEAKNESS.md`, `README.md`.

**Deliverable:** `teams/ledger/ATTACK-R2.md`.

### (a) Run the target's suite yourself; record YOUR OWN numbers

```bash
cd teams/shipwright
make          # builds -O2 and -O1 -g -fsanitize=address,undefined, runs both
make loc      # their line counts
```

Reproduce: the verdict line `== 218116 checks, 0 fails => PASS ==` (both
builds); `sizeof(quilt_t) == 9,496` bytes, fold size 9,448 bytes; the
100,000-op fuzz histogram (OK 20,851 · REPLAY 42,105 · TICK_DUE 48 · BOUNDS
32,395 · AMOUNT 860 · FULL 2,188 · DUP 2 · NO_LINK 1,472 · THEORY 4 ·
OVERFLOW 75); C2 (9,448/9,448 truncations refused), C3 (75,584/75,584
bit-flips refused); C11 (24 ns/op) and C12 (~37 µs fold+unfold). Re-run `make`
and report the check count and any sanitizer report yourself.

### (b) One real exploit vs their adversarial claim (C7/C13)

C7 claims *"phantom fish refused WITH a booked reason"* and §2 claims *"the
mint does not exist — no verb creates custody."* C13 claims *"every balance
write is a balanced posting."* Attempt **one**:

- **Forge custody through the fold (their W11 — "the image is trusted").**
  FNV-1a-64 detects corruption, not forgery. Author a fold image with a
  *correct* checksum that mints arbitrary fish custody (or drains a tally),
  and show `qc_unfold` loads it. If a forged-but-checksum-valid fold mints
  custody that no verb created, then "the mint does not exist" is false in
  the only place custody enters cold — the fold *is* the mint, and W11's own
  words ("a doctrine, not a defense") become your finding. This is the
  sharpest possible attack on their phantom-duty: a fish in the hold with no
  booked debit, fabricated by the fold author.
- **Schema-less accounts (their W4, their #1-ranked fear).** Move an
  `AC_REFUSE` tally (or a link capacity) as if it were fish custody via a
  plain `qc_effect`. Conservation is by *cut*, never by *kind* — so the move
  is cut-conserved (C5 holds, C13 holds) yet semantically corrupt. Show a
  bookkeeping move that passes every invariant they check and still drains a
  refusal tally into a hold. If it reproduces, "craft is armor" is armor
  against magnitude, not against meaning.

### (c) Attack the deepest bet

Their deepest bet, stated falsifiably: *"a quilt-shaped runtime cut as one
hand-crafted 444-line C99 unit, five verbs and a joint, zero heap, zero
floats — and it survives its own fuzz. The calculus is a description of
joinery, and joinery is enough."* The self-offered kill: *"if a rival can
show a duty that NEEDS the sixth function as a separate verb, this joinery
was glue."*

- **The sixth verb was not removed, only renamed — and one duty was priced
  out.** W5 admits: binary consent only, *no escrow protocol (GC-T4
  unimplemented)*, a 3-party link *unrepresentable, not merely unbuilt*. The
  spec's own repair (GC-T4's escrow / n-ary consent) is a duty the
  five-verbs-plus-joint cannot carry. That is not a nit — it is their own
  kill condition, met. Book it as such: joinery is *enough for the slice*, and
  the slice is what the challenge happened to test, not what the calculus
  asks.
- **The "no mint" bet is a dodge, not a defense (their W11).** "No verb
  creates custody" is true and irrelevant: custody is still created — by the
  fold author, with no signature. The minimalism that removes the mint verb
  removes the only place minting could have been *refused*. The forge in (b)
  is the counterexample.

### (d) Drive the two most damaging WEAKNESS entries further

1. **W11 — "the image is trusted."** Complete the forge in (b) into a table:
   how many bytes of the 9,448-byte fold must you change, and at what cost in
   FNV-1a re-computation, to mint an arbitrary custody delta? The answer is
   "zero bytes of attack surface — just recompute the checksum," and that is
   the measurement that separates "corruption-resistant" (true, C1–C4) from
   "forgery-resistant" (false). State both honestly.
2. **W7 — "stale-but-new nonces are silently no-op'd."** Issue a genuinely
   *new* transaction under a nonce `<= journal` (a caller whose counter went
   backwards, or a delayed-but-new message) and show it returns `ST_REPLAY`
   with balances unchanged — a legitimate move *silently lost*. This falsifies
   the DEFENSE §2 claim *"Refused ≠ silent, ever"*: here nothing is refused,
   nothing is booked, and the move is gone. Count how many such silent drops
   you can induce before any audit reads them back out of the log ring.

---

## REFEREE SUMMARY

### The three sharpest seams across all six defenses

**Seam 1 — The fold is a mint, not a lock.** Every team's serialization
detects *corruption* and authenticates *nothing*. SHIPWRIGHT's FNV-1a-64
(W11: "the image is trusted… the fold is the mint is a doctrine, not a
defense"), LEDGER's compensating-corruption hole (W4: two sum-preserving
flips evade the trial balance, caught only by journal replay), ORGANISM's
seal and DEADBAND's CRC both stop at tamper-evidence. The phantom-custody
duty — *a fish in the hold without a booked debit is refused* — is enforced
at the verb layer and entirely absent at the fold layer. Whoever writes the
fold mints the custody. This is the deepest seam because it is universal and
it attacks the challenge's core adversarial duty, not a cosmetic one.

**Seam 2 — Bounded accounts, unbounded history.** Every team bounds the
*accounts* and bounds nothing about the *ledger/log/QUF image/nonce set*.
PROCESSION's ledger is "append-only but NOT bounded" (W3); ORGANISM's QUF
grows to ~800 KB and climbing with decelerating-but-unproven growth (W5);
SHIPWRIGHT's receipts outlive the link budget and the 256-entry log ring
wraps, losing receipts (W10); DEADBAND bounds by fiat at 200 slots but its
fold is "shallower than the v1 fabric's" (W4). "Bounded serialization" is
only as bounded as the history is — and the history is the leak. The audit
trail every team brags about is the unbounded state none of them capped.

**Seam 3 — The freshness floor is priced against a fiction.** rho·F is a
theorem, but rho, margin, and F are *operator dials*, never estimates.
DEADBAND says it plainly (W2: "mis-dialed rho is silent until it is loud";
W5: "the floor we sit on is the budgeted floor, not the realized one");
LEDGER books its floor as an `inflight` account but never estimates rho
(W1, W9); ORGANISM's nonce window is "a convention, not a mechanism" (W5).
Every team that claims to "sit exactly on the floor" sits on a floor of
asserted inputs — and no one has built the observed-rate estimator that would
turn the floor from a dial into a measurement. A champion whose honesty is
dial-faith is not *truly* honest; the floor theorem says the estimator would
itself be F-stale, which is precisely why this seam has not closed.

### Which matchups R4 / R5 measure rounds should stage

- **R5 head-to-head #1 — DEADBAND vs LEDGER on the freshness floor.** The
  only two teams that claim to *book* (not beat) rho·F, and the only two
  whose seam-3 exposure is mutually measurable: whose "honest refusal /
  booked blindness" survives a mis-dialed-rho sweep, and whose answer at
  `rho*F >= margin` is a defense rather than a surrender. The harness: one
  fixed realized-drift world, both dials swept, `covBAD` and
  productivity-vs-audit-cost measured per dial point.

- **R5 head-to-head #2 — SHIPWRIGHT vs LEDGER on bounded state and fold
  integrity.** The two "smallest" builds (9,496-byte sizeof vs 9,216-byte
  QUF). Stage them on the two seams they share: whose fold survives a
  *forgery* (not a corruption) attack, and whose "bounded" claim still holds
  once the log ring / link budget / audit ring is saturated. This is the
  keel-vs-paint measurement: both claim fixed-size, one (ledger) buys it by
  *forgetting* (W5), the other (shipwright) by *recompiling* (W12) — measure
  which failure is more honest.

- **R5 head-to-head #3 — ORGANISM vs PROCESSION on "does the explanation /
  the metabolism change a verdict?"** The two philosophy-first builds. The
  cold-read and devil-pass (R5) are the only instruments that can settle
  whether ORGANISM's Hebbian layer and PROCESSION's tutor are load-bearing
  organs or costume — because neither team has a number that shows their
  signature mechanism *moving a verdict*. Stage the disabler test: run each
  with its signature layer stubbed off, and measure the verdict delta. Zero
  delta is the finding both most fear, and the tournament must know it
  before the champion is crowned.

The Gauntlet (Shell 4) should open with a stir aimed at **Seam 1** (fold
forgery) — it is the one seam no team has even named a defense for, and the
champion must survive it to survive anything.

---

*End of R2-PACKETS. Packets are orders, not attacks; attacks land as
ATTACK-R2.md in each attacker's dir. House law: no float decides any
verdict; failed attacks earn rigor; misrepresentation loses points.*
