# REACTIONS.md — Shell 3: tournament chemistry

*Referee table of all 15 pairwise reactions, with scouts/STIR-01 (CICS
two-machine compensating recovery) as the reagent, and the three most
energetic syntheses speced as R3 hybrid-build assignments.*

Compiled 2026-08-29 ~22:30 AKDT. Method: read all six teams' DEFENSE.md +
WEAKNESS.md (stream: none exist — only `rtl/sc_cell.v`, cited pen-only from
the RTL itself), read scouts/STIR-01.md. Every headline suite re-run on this
host before writing (appendix A): shipwright `make` (218,116 checks, 0 fails),
procession `npm test` (35/35), organism `pytest` (67/67), deadband
`benches/measure.py` (floor rho*F=1, covBAD=0 everywhere, adversarial arm
0-vs-40), ledger `cargo test` (39/39). Verdicts cite measured numbers from
the defenses and this host's re-runs — no float decides any classification;
rankings are integer counts of fixed weaknesses, not vibes.

Team keys: **S**=shipwright, **O**=organism, **P**=procession, **D**=deadband,
**L**=ledger, **T**=stream (RTL-only, no defense).

---

## 0. The reagent: where CICS two-machine recovery bonds

STIR-01's mechanism: **Machine 1 (backward recovery)** — before-images on a
system log physically undo UNCOMMITTED work automatically, even after a
crash. **Machine 2 (compensating recovery)** — COMMITTED work is never
physically rolled back; it is logically undone by a NEW forward transaction,
itself a full booked unit of work. The deep claim: one machine doing both
either un-commits committed history (audit forgery) or cannot undo it.

The reagent does not bind evenly. Measured placement:

| team | the seam the reagent finds | bond energy |
|---|---|---|
| **L** | Batch = unit of work. An epoch that never closed is uncommitted; reloading the last trial-balanced close IS automatic backout (machine 1, already built). Forget/quarantine-reconcile IS a forward refund (machine 2, already built — D3's suspense/quarantine). The two machines exist but are *unnamed*: nothing books which machine touched a recovery. | **bonds natively** — the compound is one label field + the epoch-length dial |
| **T** | The pending cross-escrow (`hold_active`) is uncommitted work with **no timeout and no journal**: dst applies, src commits a cycle later — a mid-cross crash leaves a half-committed transaction the image fold cannot see (no transcript). Machine 1 is absent; machine 2 exists only as NAK. | **bonds at the escrow** — needs a backout path (journal or timeout+compensation flit) |
| **S** | The `forget` joint reverses through the SAME balanced-apply path as forward effect. Receipts exist (`LC_DROPPED`, `lastf` tally) but carry no machine identity — the "which machine touched this reversal" question (STIR-01's named strongest target) is unanswerable from the receipt. | **bonds at the receipt** — a 1-field machine tag answers without a sixth verb; else shipwright's own concession clause fires |
| **O** | The GC-C4 snap is compensation-shaped (new forward correction, debt |g−s| booked — the scar EXISTS) but is branded "healing"/"recovery in one tick," which reads as backout. CICS: compensation is NOT recovery. | **bonds at the brand** — book the snap as class COMPENSATION, keep the scar |
| **P** | Measured-zero differential covers 17 refusal paths, **zero compensation paths** (STIR-01). The tutor can explain "refused"; it has no lesson for "committed, then undone." | **bonds at the reasons table** — add an undo/compensation code class + drills |
| **D** | W1 admits the crash question is deferred: after a crash, which in-flight work rolls back automatically vs defers to audit? CICS's before-image log is a mechanism for *un-seeing*, not just un-verifying; deadband only un-verifies. | **bonds at the crash path** — the unclosed epoch's rollback as a booked class |

Strongest bond: **ledger** (both machines already exist, machine-checked;
the reagent only demands naming them). Runner-up: **stream's escrow** (a real
hole, CICS-shaped). The three R3 syntheses below each carry a piece of the
reagent; D×L carries the whole thing.

---

## 1. The reaction table — all 15 pairs

| pair | compound | class | the one experiment |
|---|---|---|---|
| S×O | the joinery that metabolizes | STABLE (bonds only in the presence of the reagent) | 100k-op shipwright fuzz with organism's integer masses as the judgment dial: cut==40 must hold AND every live link's mass stay ≥1 AND a verdict must actually change on mass (else O-W3 stands) |
| S×P | the pedagogical ledger | STABLE | cap procession's refusal ledger at shipwright's 256-ring + counters; re-run differential (must stay 0) and the 218,116-check suite (no regression); falsifier: any drill needing an evicted ring entry |
| S×D | the clockless joint meets the freshness budget | INERT — one machine refuses the time dimension, the other IS the time dimension | exhibit deadband's rho*F floor on shipwright: no audit instants, no support accounting → the floor is undefined, the schedule has nothing to schedule against |
| S×L | two witnesses, one fold | STABLE | ledger's compensating-corruption attack (+7/−7 sum-preserving, L-W4 machine-checked) against shipwright's FNV fold loader (must refuse — byte change), and a targeted FNV-forgery (S-W11) against ledger's journal replay (must catch — transcript) |
| S×T | the golden C and the silicon | STABLE | co-sim: run shipwright's corruption suite (75,584 bit-flips, 30,000 multi-byte) against stream's CRC16 fold — a crafted flip pair that collides 16-bit loads silently = falsifier; the checksum seam is the reaction |
| O×P | the tutor as the mass-reader | CATALYTIC — third mechanism: **the rank-ordered lesson** | 5 seeds × 12-day adaptation, drills ranked by Hebbian mass vs random: +11pp naive gain preserved AND drill pass-rate on previously-failed paths improves; if rank() changes nothing, O-W3 stands |
| O×D | the one-tick heal vs the deferral duty | EXOTHERMIC destructive — named collision | deadband's adversarial arm (rho=2, margin=8) with organism's healing: inject F-stale drift → either the heal fires (covBAD>0, D1 dead) or defers (max_ticks_to_heal>1, C2 dead). One machine-checked claim dies either way |
| O×L | the metabolism that audits | STABLE | organism's 12-day adaptation (5 seeds) on ledger's substrate: trial-balance-zero at every close across all 17 adaptations AND +11pp naive gain reproduced, audit toll measured (34.0 checks/event) |
| O×T | the silicon synapse | STABLE | port organism's asymptote contrast (float dies at step 1075; mass floors at 1) to RTL: 100k leak/fire cycles — live-link w must never hit 0 without FORGET; act may (allowed); 68-word fold warm-restart byte-exact |
| P×D | the tutor of blindness | STABLE | register deadband's DEFERRED + LKG as procession codes 18–19, drill them on the live seeded bench; differential must stay 0; falsifier: timing-dependent reason text (F-dependent verdict drilled as if deterministic) |
| P×L | the auditing tutor | STABLE | cap procession's refusal ledger at ledger's 64-ring; re-run C2 differential (0) and the 2,100-landing flood (233 deferrals) — ring + counters must carry the flood; falsifier: a lesson requiring an evicted entry |
| P×T | the tutor in silicon | STABLE | map procession's 17 codes ↔ stream's 15 NAKs; co-sim every drill's wrong move as flits; differential must be 0; falsifier: a hardware NAK with no registered explanation |
| D×L | the floor booked as an account | STABLE (the reagent's home) | kill a batch mid-close, reload: unclosed epoch's effects absent (backout, machine 1) AND a forget is a new journal entry, never a rewrite (compensation, machine 2); then deadband's adversarial arm with epoch-length as the policy dial |
| D×T | the wavefront has no waiting room | EXOTHERMIC destructive — named collision | feed deadband's scenario (60 moves, 30–45 deferrals) as flits to a stream fabric: the second concurrent deferral parks E_BUSY (one `hold_active` slot); covBAD=0 becomes unrepresentable in one cell |
| L×T | the journaled wavefront | CATALYTIC — third mechanism: **CICS two-machine recovery** | kill a stream fabric mid-cross (dst applied, src uncommitted), reload from ledger's journal: half-committed cross absent (backout) and a booked backout entry present; falsifier: src/dst disagree after reload |

---

## 2. Pair notes (evidence, not vibes)

**S×O — STABLE, reagent-assisted.** Both integer-exact, both book their
changes; the joint is organism's `rank()` masses becoming shipwright's
judgment organ. Shipwright's judgment is one pseudometric |Δi64| (S-W13);
organism's Hebbian layer "guides only probe ordering... mostly potential
energy" (O-W3). 32 shipwright links × 8B integer = 256B — fits the fixed
9,496B machine; no float; the sizeof survives. The seam: shipwright's tick
posts nothing (GC-L2, machine-cited) while organism's heal is four postings
inside one tick (C2: `one_tick_heals:true`, 39/39, 37/37, 33/33) — and
shipwright has no autonomous cell action (verbs are caller-invoked), while
organism's cells self-heal. The reagent resolves both: the heal is a
COMPENSATION — a new forward effect, issued by the (bounded) audit layer,
booked with its |g−s| scar — not tick work and not backout. Bonds only under
the reagent; without it the autonomy gap is a collision.

**S×P — STABLE.** Procession's unbounded refusal ledger (P-W3: "a hostile
party can grow a cell's ledger without bound by spamming refused nonces")
meets shipwright's 256-entry ring + attempt-counting tallies (S-W6 books
refusals as tallies+ring). The 105-LOC reasons table lives code-side; the
ring only needs to carry the last-N codes, and the 17 explanations are
regenerated — so procession's pedagogy survives boundedness. Shipwright's
terse refusal codes gain operator language (fixes S-13's "AMBIGUOUS exists;
richness doesn't"). Totality note: procession throws on fabric-misuse
(P-W1), shipwright never throws (C10, ASan/UBSan-clean) — the hybrid takes
shipwright's totality as substrate.

**S×D — INERT.** Shipwright by design has no clocks in state (W9: "Nothing
measures wall time") and freshness is nonce-lag, never wall time (W8);
deadband's entire product is F/rho/margin against a tick clock with audit
instants. On a clockless machine the support bound `rho*(now−serial)` has no
`now`, the floor is undefined, the scheduler has no schedule. Neither
mechanism changes the other; deadband on shipwright is app-convention (which
shipwright's own W says escrow/cron are). A sum, not a reaction. (The CICS
reagent also does not bind: shipwright's crash story is reload-the-image, no
before-image log; deadband's un-seeing needs one neither has.)

**S×L — STABLE.** The two book-first entries, near-identical philosophy in C
and Rust — an alloy, low heat, high integrity. The real reaction is
complementary witnesses: shipwright's FNV-1a-64 image checksum refuses any
byte change (75,584/75,584 bit-flips, 30,000/30,000 multi-byte) — including
ledger's compensating +7/−7 flips, which evade the trial-balance gate
(L-W4, machine-checked) but change bytes and so die at the checksum; ledger's
journal replay (state = fold(journal), 227,426 entries replayed bit-identical)
catches what shipwright's trusted-image doctrine cannot (S-W11: FNV detects
corruption, not forgery). Each closes the other's only corruption hole.

**S×T — STABLE.** The classic co-design bond: shipwright's 444-line C core +
218,116-check suite is the executable spec; stream's 914-line `sc_cell.v` is
the silicon. Shipwright's W8 (Q1 "holds trivially in a single-threaded
interleaving — nothing under genuine parallelism") is answered by stream's
synchronous wavefront; stream's empty `tb/` (zero verification, zero defense)
is answered by shipwright's suite as co-sim oracle. The sharp seam: FNV-1a-64
vs CRC16-CCITT — a 16-bit checksum has a 2^16 collision class; shipwright's
corruption guarantees are NOT portable to the RTL fold as-is. That measured
mismatch is the reaction's energy (see R3-B).

**O×P — CATALYTIC.** Neither core changes. The third mechanism is the
rank-ordered lesson: procession's drill queue is ordered by organism's
Hebbian masses, so the masses finally decide what gets taught = what gets
remembered — giving O-W3's "potential energy" a reader without touching
either runtime. Organism's adaptation (17 booked dial-writes, +11pp naive /
0pp tuned, MEASURED.md) gives procession's W9 ("we taught, but did not
measure, learning") a measurable substrate: lesson retention on adapted vs
frozen dials. Catalyst, not compound: no merge required, both falsifiable
claims survive independently.

**O×D — EXOTHERMIC destructive.** Organism C2 (heal in exactly one tick,
machine-measured `one_tick_heals:true` at every deadband) vs deadband D1
(never answer with support >= margin; covBAD=0 across all 8 policy arms).
Deadband's W1 is the same collision in its own words: sub-verified staleness
is a refusal; organism's W1 admits drift sits uncorrected below the deadband
indefinitely. If the heal's drift evidence is F-stale, deadband's duty says
DEFER the heal; organism's contract says heal now. One machine-checked claim
dies. The reagent names the survivor: healing is a compensation (forward,
schedulable, scarred — organism already books |g−s|), so deferral is legal
for compensations; the dead claim is "healing is recovery/backout," which
was always the poetry (O-W2 already concedes the enforcement-vs-emergence
gap). Sharpest collision in the field.

**O×L — STABLE.** Ledger's audit-first net (138 invariant evals/batch, 34.0
checks/event, trial-balance-zero 102/102 closes, 1.48M events/s) is the
enforcement O-W2 admits its metabolism lacks ("conservation is enforced, not
emergent"). Ledger's suspense/quarantine (D3) is already the booked-forward-
refund shape — organism's snap becomes an audited compensation transaction on
ledger's substrate. Ledger's thin tick body (L-W7: "the drift-response
family: carried, not exercised") gains organism's exercised adaptation
(17 booked dial-writes). Seam: the heal commits at batch close, not in one
tick — C2 re-registers as "one epoch," and the freshness floor applies to
healing (organism W1 already lives with that). Booked residue, not a refusal:
ledger's inflight account is the legible scar.

**O×T — STABLE.** Stream's cell is already an organism: `act` accumulates
(satadd), leaks (`>>> d_leak`, clamps to 0), fires when `act >= d_thresh`,
refractory `refr`, fanout to all links — a leaky-integrate-fire neuron with
balanced books, integer-only. The link slot's `w[3:0]` is a saturating usage
counter that is never decremented — only FORGET clears it: organism's
never-zero mass contract (C1: float dies at step 1075, integer floors at 1)
is trivially honored in 4 bits because there is no decay path at all. The
mass/potential split (`w` = mass, `act` = potential) resolves the apparent
"decay dies" collision — `act` may hit zero, `w` never does; that is
literally organism's dormancy-vs-death distinction. Fixes O-W5 (820,161-byte
QUF → 68-word fold) and O-W6 (Python → nanoseconds). Stream's `w` is
currently read nowhere (the RTL's own potential-energy problem, same as
O-W3) — the hybrid must give it weight (see R3-C).

**P×D — STABLE.** Deadband's verdict universe is three-way — ACCEPT /
DEFERRED / LKG (D4, all booked, fail-static) — and procession's registry has
17 refusal codes with zero deferral/last-known-good classes. The bond:
register DEFERRED and LKG as codes 18–19 with drills; the operator learns why
the runtime refuses to see (support >= margin), which is deadband's W1 made
legible ("The Switch Test lives on in every DEFERRED we book" — now the
deferral is a lesson, not a tombstone). Seam: deferral outcomes are
F-dependent; the drills must run on the seeded deterministic bench (deadband
W5: "seeded deterministically") so the differential (P-C2) stays 0.

**P×L — STABLE.** Ledger's 64-entry audit ring forgets (L-W5) but stores
codes; procession's explanations are code-side (105-LOC table), not
history-side — so ring eviction costs the ledger nothing the tutor needs:
the code regenerates the text. This caps procession's unbounded ledger
(P-W3) at ledger's bound with counters for the flood (P-C6: 2,100 landings,
233 deferrals). Modification owned: P-C3 ("a booked reason IS the error
message") re-registers as "a booked code IS the error message; the text is
derived" — one semantics, two encodings.

**P×T — STABLE.** Stream's 15 NAK codes (E_BADOP…E_BUD, all booked against
`err_cnt`/`budget_pool`) are a hardware refusal registry with a 1:1-ish
footprint to procession's 17; procession's code=message=lesson lifts onto
the RTL (the E_* codes even carry the TUTOR-lineage budget-park: E_BUD at
MAXCYC=32 — totality by budget, exactly what procession's lineage cites in
GENERAL-CALCULUS §6.4). Fixes stream's zero-verification (procession's
35-test suite + doc-tests as the RTL's co-sim harness) and procession's W6
(coarse work-time ticks → real synchronous beats). Seam: procession throws on
fabric misuse (P-W1); the RTL never throws (E_STRAY for stray responses,
E_PARK for bad folds) — the hybrid takes the RTL's totality.

**D×L — STABLE, the reagent's home.** Both teams independently implement the
same floor: ledger D4 machine-witnesses ρ·F with F=1 epoch (5 fish mid-epoch
invisible, residue in `tote-p:inflight` — the freshness window is an
ACCOUNT); deadband D6 exhibits rho*F=1 as a support bound with covBAD=0.
The compound: ledger's batch epoch length becomes deadband's scheduled
quantity — RF-P2's purchasable freshness (deadband W4: unbuilt) is the dial
both sides were missing. And the CICS two machines are already ledger's:
an epoch that never closed is uncommitted → reload of the last
trial-balanced close is automatic backout (machine 1, before-image = the
closed fold); forget/quarantine-reconcile is a new journal entry, never a
rewrite (machine 2, compensation). The hybrid's work is a machine-identity
field on recovery entries and the epoch-length policy dial. Highest reagent
energetics in the field.

**D×T — EXOTHERMIC destructive.** Deadband's slow-cadence rows book 30–45
deferred moves against a 256-entry pending shelf (D5); stream's cell has ONE
outstanding cross (`hold_active`, `E_BUSY` on the second). A deferral queue
is unrepresentable in the shipped RTL: feed deadband's scenario as flits and
the second concurrent deferral parks E_BUSY — deadband's covBAD=0 coverage
(its headline D1) cannot be expressed in one hardware cell. Second clash:
deadband's drift-triggered cadence is dynamic policy; stream's `wf_tick` is
a fixed barrier. STIR-01's one-log charge lands here too (before-images vs
after-images in a single flit stream — "a synthesis bug waiting for a
mid-fold crash"). The reagent's fix (two streams, two lifetimes) is a real
hardware change, not a joint.

**L×T — CATALYTIC.** Stream's pending cross has no timeout and no journal;
ledger has a journal and no wavefront. Neither changes the other's core —
the third mechanism is CICS two-machine recovery itself: the pending
`hold_val` is a before-image needing backout (machine 1 — journal reload
erases the uncommitted cross), and the refund/teardown flit is the
compensation (machine 2 — a new booked entry). The catalyst makes the
mid-cross crash hole (dst applied, src uncommitted — invisible to both the
image fold and each cell's locally-balanced books) into a replayable,
booked backout. This is the reagent's second-strongest bond, and the only
one that requires no change to either team's existing mechanism.

---

## 3. The three most energetic syntheses — R3 hybrid-build assignments

Ranking by integer counts of fixed weaknesses and by falsifier sharpness
(no floats): D×L fixes deadband W1/W4 + ledger W3/W4/W5 and carries the
whole reagent; S×T fixes shipwright W8 + stream's everything (no defense, no
tests, no concurrency) with a machine-checkable checksum seam; O×T fixes
organism W5/W6/W3 + stream's unused `w`. Each spec: participants, the
compound, the claims, the falsifiers. Hybrid builds land in referee-assigned
build dirs — teams/ is not modified.

### R3-A — DEADLEDGER (D×L): "the floor booked as an account"

**Merge.** Deadband's audit scheduler (audit policies: static + drift-
triggered, support bounds, covBAD accounting) ported into ledger's Rust
batch core as the epoch-length controller. Runner: Rust (`cargo test` +
a new `examples/bench.rs` arm). Build shape: `batch()` epoch length driven
by a drift-triggered policy dial; recovery entries gain a machine-identity
field (`BACKOUT` vs `COMPENSATION`) in the journal/ring; deadband's deferral
counters join ledger's existing accounts.

**The hybrid claims.**
1. *Freshness is purchasable and booked in both units.* The epoch length is a
   scheduled quantity; ledger's `inflight` residue (ρ·F as fish, D4
   witnessed: 5 mid-epoch fish invisible) and deadband's deferral counts
   (ρ·F as booked deferrals, D1: covBAD=0) are the same floor in two
   ledgers of the same run.
2. *Two-machine recovery, explicit.* A crash mid-batch auto-rolls-back to the
   last trial-balanced close (machine 1 — the closed fold image is the
   before-image; ledger D2's reload+replay is the mechanism); a forget or
   quarantine-reconcile is a NEW journal entry with machine identity, never a
   rewrite (machine 2 — ledger D3's suspense/quarantine is the refund shape).
3. *D3 reproduces on the audit-first substrate.* Deadband's adversarial arm
   (rho=2, margin=8): static epoch → 0 accepted / 60 deferred (booked),
   drift-triggered epoch → 40/40, covBAD=0 — with ledger's trial-balance-zero
   at every close (D1: 102/102 closes) and the audit toll measured (34.0
   checks/event, 1.48M events/s).

**How falsified (all machine-checked, no floats).** (a) any effect of an
unclosed epoch visible after reload; (b) any compensation that edits an
existing journal entry (audit-chain forgery — ledger W4's replay net is the
catcher); (c) covBAD > 0 in any policy arm; (d) trial balance nonzero at any
close. One passing test per falsifier; verdicts are integers.

**The stir's role.** This is where CICS bonds natively: ledger already has
both machines and the unit of work (the batch) that defines "uncommitted."
The reagent's demand is one label field and the epoch dial. STIR-01's
deepest deadband threat (W1: "which in-flight work rolls back automatically
vs defers to audit?") is answered by construction: an epoch that never
closed rolls back; everything else defers or compensates.

### R3-B — SHIPSTREAM (S×T): "the golden C and the silicon"

**Merge.** Shipwright's core.c + test.c (the 444-line reference and its
218,116-check suite) as the executable oracle; stream's sc_cell.v as the
device under test. Build shape: a co-simulation harness (C model emits flit
vectors; iverilog/verilator — both present on this host — simulate the RTL;
compare state and folds byte-for-byte after every vector). The hybrid owns a
shared fold cross-check: C's 9,448-byte image and the RTL's 68-word frame
must agree on every state reached by identical flit sequences.

**The hybrid claims.**
1. *Parity.* Stream's cell passes shipwright's C1–C7 classes in co-sim:
   fold round-trip (canonical), every truncation refused, corruption
   refused, custody cut conserved under fuzz, replay idempotent, phantom
   refused with a booked NAK, tick unstarvable under ingress storm.
2. *The checksum seam is closed or booked.* Shipwright's corruption
   guarantees (75,584/75,584 single-bit flips, 30,000/30,000 multi-byte)
   must hold against the RTL's CRC16-CCITT fold. Known weak point: 16-bit
   space vs FNV-1a-64. The hybrid either upgrades to a 32-bit CRC or
   measures and books the collision class (which corruptions a 16-bit CRC
   silently accepts — and refuses them by policy).
3. *Reversals carry machine identity (the CICS answer to the forget-joint).*
   Every FORGET/teardown receipt (`lastf_slot`/`lastf_peer`) and every
   pending-hold backout carries a machine tag in the fold. This directly
   tests shipwright's own concession clause ("if a rival shows a duty that
   needs the sixth function as a separate verb, we concede"): if a 1-field
   receipt answers "which machine touched this reversal," the forget remains
   a joint, not a sixth board; if it cannot, shipwright concedes, on the
   record.
4. *Concurrency with receipts.* Shipwright's W8 (Q1 holds only in single-
   threaded interleaving) is answered: the RTL's synchronous cells are the
   genuine-parallelism evidence, and co-sim shows the C model's serial
   interleaving and the RTL's wavefront reach identical final states
   (per-link FIFO discipline parity, both machine-cited).

**How falsified.** Any co-sim divergence on identical flit vectors; any
CRC16-colliding corruption that loads silently; any reversal without
machine identity in the receipt; any state reachable in the RTL but
unrepresentable in the golden C, or vice versa.

**The stir's role.** Stream's pending-hold escrow is the CICS hole (no
timeout, no journal — mid-cross crash = half-committed transaction invisible
to the image fold). The hybrid answers with machine identity on reversals
and — for the escrow — a defined backout (timeout → booked teardown flit).
STIR-01's named strongest target (shipwright's forget-joint) gets its
field trial here, with the receipt as the witness.

### R3-C — SYNAPTIC STREAM (O×T): "the silicon synapse"

**Merge.** Organism's metabolism (integer masses, refusal-nutrients, the
snap) into stream's cell. Build shape: extend the RTL link slot's `w[3:0]`
into the load-bearing Hebbian mass (it is already a saturating counter never
decremented except by FORGET — the asymptote contract is free in silicon);
make FIRE fanout and VIEW ranking consult `w` (mass-weighted: fire/teach the
strongest links first); add the snap as a booked compensation entry with a
visible scar in the fold. Runner: Verilog sim + organism's backdeck.py as the
golden Python model driving flit vectors; byte-compare folds. The 68-word
hardware fold replaces organism's QUF as the conformance image.

**The hybrid claims.**
1. *The asymptote in 4 bits.* `w` never reaches 0 for a live link — only
   FORGET kills (organism C1's contract: float halving dies at step 1075,
   integer mass floors at 1; in silicon there is no decay path at all).
   `act` leaks to 0 — allowed: the mass/potential split is explicit,
   machine-checked, and is organism's own dormancy-vs-death distinction.
2. *The fat dies.* Organism's QUF (820,161 bytes at 4,200 fish, growth
   decelerating but un-plateaued, W5) collapses to the 68-word fold
   (~136 bytes); warm-restart from the hardware fold reproduces identical
   metabolism state (mass, potential, nonces, escrow, scar) — organism's
   50/50 warm-load claim ported to silicon, byte-exact.
3. *Healing is compensation, not backout (CICS, made fold-visible).* The
   snap is a booked, scarred forward transaction (debt |g−s| in the fold,
   machine-tagged COMPENSATION); nothing is rewound; sub-deadband drift sits
   uncorrected, as organism W1 honestly reports. The one-tick claim
   re-registers as "one effect, scheduled" — the CICS lesson organism's own
   DEFENSE invited ("book the scar or admit the heal is cosmetic"): the scar
   is already booked in Python; this makes it a first-class fold entry.
4. *The masses finally read.* FIRE fanout order and VIEW ranking consult
   `w` — the Hebbian layer carries behavioral weight, closing O-W3 ("if the
   referee never exercises rank(), our adaptation story reduces to integer
   bookkeeping wearing a biology costume") for the silicon side too.

**How falsified.** (a) a live link's `w` reaches 0 without FORGET; (b) fold
mismatch between Python model and RTL on identical traffic; (c) a heal
without a scar entry in the fold; (d) a proof that `w` never influences any
outcome (then O-W3 stands and claim 4 is withdrawn on the record). All
integer-only (signed 16-bit satadd — stream's arithmetic), all machine-
checked.

**The stir's role.** CICS demands the scar; organism already books |g−s|.
The hybrid's only real work is naming the heal COMPENSATION in silicon and
letting the fold carry the scar — machine 2 made explicit. Machine 1 is
trivial here (the fold is atomic; there is nothing uncommitted to back out
inside a cell — the pending-hold escrow is the R3-B problem, not this one).

---

## Appendix A — verification run log (this host, before writing)

| suite | command | result |
|---|---|---|
| shipwright | `make` | `== 218116 checks, 0 fails => PASS ==`; bench: effect 83 ns/op, fold 30.5 µs/pair (load-dependent; DEFENSE quotes 24 ns / 18–37 µs) |
| procession | `npm test` | 35/35 pass |
| organism | `python3 -m pytest tests/ -q` | 67/67 pass (67 test fns counted) |
| deadband | `python3 benches/measure.py` | floor rho*F=1 exhibited; covBAD=0 all 8 rows; adversarial arm: static T=4 → 0 acc/60 def, drift-triggered → 40/40 |
| ledger | `cargo test` | 39/39 pass (13+7+8+11) |
| stream | — | no suite exists; `rtl/sc_cell.v` only (914 lines), `tb/` `harness/` `quf/` empty; all stream citations are pen-read from the RTL |

House law honored: no float in any verdict here; all classifications are
arguments over machine-checked integers and pen-citable RTL lines. teams/
was not modified. STIR-01's reagent is distributed across the table as
shown in §0 and carried whole by R3-A.
