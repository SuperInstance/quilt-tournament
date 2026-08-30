# R2-SCORES — Shell 1 Adjudication (the five cross-attacks)

*Referee · 2026-08-29 23:16 AKDT start · scored after reading CHALLENGE.md,
referee/R2-PACKETS.md, all five ATTACK-R2.md in full, each target's
DEFENSE.md + WEAKNESS.md, referee/REACTIONS.md, and one killer-citation
spot-check per attack executed by the referee on this host (below). House law
holds in this file: every claim cites file:line or a measured number; no
float decides any verdict; scores are integers.*

## Referee verification basis (what I checked myself, not took on faith)

| attack | killer citation | referee spot-check | result |
|---|---|---|---|
| SHIPWRIGHT→ORGANISM | `cellcore/ledger.py:186` seals `rcpt.kind`; `ledger.py:229-234` `verify_chain` hardcodes `"kind":"applied"` | sed both regions; grep `NONCE_WINDOW` (:22, :176); grep `.rank(` (docstring only, no runtime caller) | **confirmed** |
| ORGANISM→PROCESSION | `src/fold.ts:128-130` (`parts[1]/parts[2]` + `kind.length` unguarded); `fold.ts:160` rethrows non-ParseErr; `reasons.ts:55` "bind it higher"; `core.ts:163` `dialSpecs`→`R-DIAL-UNKNOWN` | sed all four regions; `tutor.ts:131-136` writes account `"cas h"` | **confirmed** |
| PROCESSION→DEADBAND | `cellcore/fabric.py:120-127` judge; `cellcore/audit.py:34-44` `support_bound`; `cellcore/cell.py:186-189` `resolve_pending` | sed both; grep `resolve_pending` tree-wide → defined `cell.py:188`, sole caller `tests/test_fish.py:115` | **confirmed** |
| DEADBAND→LEDGER | `src/quf.rs:665` decode→`Fabric::from_parts`; `fabric.rs:180` area validates names only | sed `fabric.rs:172-195` (BadName check, no balance gate); grep quf decode | **confirmed** |
| LEDGER→SHIPWRIGHT | `core.c:412` `x->acct[k]=(i64)gu64(r)` no sign/custody check; `core.c:203/220/264` `n<=q->journal→ST_REPLAY`; `core.c:341-345` reversal overflow-only | sed all regions (line 412 exact); `sha256sum core.c` both copies = `93de861e…d1fd` | **confirmed** |

Evidence-artifact sweep: all five attackers committed runnable probes + raw
logs (`run_exploits.py`+`evidence-x1-x7.log`; `probe.ts`/`probe2.ts`+
`probe2-results.txt`+`tutor-measure-records.jsonl`; `deadband_probe.py`;
Cargo harness `src/main.rs`; `probe.c`+`probe-run.log` ending
`== 100433 checks, 0 fails => PASS ==`). Headline numbers inside the logs
match the ATTACK-R2.md claims (referee grepped: the raw-throw lines, the
`code=R-STICKY-PARKED` forge line, `199B vs 165B`, `3 fish … 0 pounds`,
X5 `FALSIFIED (8/35 runs, worst -12pp)`). Suite re-runs corroborated against
referee/REACTIONS.md appendix A (all five suites re-run on this host earlier
this round). **Zero misrepresentations found in any attack.**

## The rubric (referee-fixed, attack round, 100 pts)

| pillar | pts | measures |
|---|---|---|
| A. reproduction honesty | 25 | ran the rival suite themselves; own numbers; discrepancies booked, not smoothed |
| B. exploits landed vs booked | 30 | real exploits with killer citations; failed attempts conceded; no padding |
| C. deepest-bet verdict | 20 | broken / scoped / survived-with-inertness, evidence-backed, philosophically forceful |
| D. weakness-drive | 15 | the two most damaging W entries driven further, with measured numbers |
| E. house law & rigor | 10 | citations everywhere, no float verdicts, self-caught defects; deductions for misrepresentation |

STREAM is not scored: R2-PACKETS §0 skipped its packet (no DEFENSE.md, no
WEAKNESS.md, no suite — nothing to attack honestly, no house to attack from).

---

## 1. SHIPWRIGHT attacks ORGANISM — 95/100

**(a) Reproduction honesty 24/25.** 67/67 tests reproduced; `cellcore.measure`
re-run with numbers identical to MEASURED.md including the QUF wave bytes
(700,376 → 766,948 → 820,161 B); the asymptote triple (1075 / 58 / never-zero)
reproduced. Credit-where-due is explicit ("their numbers are real,
deterministic, reproducible"). −1: the packet ordered the measure wall time
recorded (they claim 6.6s); not recorded.

**(b) Exploits landed 29/30.** Five landed + one scoped, each machine-checked
via `run_exploits.py`:
- **X1 (novel — nobody's WEAKNESS predicted it):** the shipped chain verifier
  fails on honest life. `ledger.py:186` seals `rcpt.kind`;
  `verify_chain` (`ledger.py:229-234`) recomputes with hardcoded
  `"kind":"applied"` — one booked refusal or one nonce no-op makes
  `verify_chain()==False` on an *untampered* ledger, including their own
  40-cycle gauntlet end-state. Referee confirmed both code regions. The
  honest scoping ("audit-integrity break, not a balance break") is in the
  body; −1 only because the header "C6 FALSIFIED" runs one notch hotter than
  the DEFENSE sentence it maps to.
- **X2 (the packet's ordered exploit, both forms):** evicted-nonce replay —
  silent form: full `land()` path after natural window roll, replay ACCEPT,
  census_ok()==True with a phantom second fish (the debit is fish #1's,
  spent twice); loud form: direct `effect()` → census break. Killer:
  `NONCE_WINDOW=4096` at `ledger.py:22,176-178`; window rolls at ~2,048 fish
  — inside their own 4,200-fish measurement.
- **X3:** input-size unbounded state — 120 txs × 100 KB nonces →
  36,027,486 B image before AND after fold (fold reclaims 0 B); ~300 KB/tx.
- **X5:** C3's falsifier produced under a fidelity check — 8/35 runs wreck a
  tuned start by >3pp, worst −12pp, after first reproducing their 0-1pp
  headline on their own regime.
- **X6:** Hebbian layer has zero runtime consumers — grep (referee-verified:
  `rank()` appears only in tests) + scramble-all-masses mid-run → stats and
  census identical.
- **X4 (correctly scoped):** recompute the public seal → balance lie loads
  ACCEPT; chain never checked on load. Scoped to corruption-detection, not
  overclaimed as forgery break — the honest call.

**(c) Deepest-bet verdict 20/20 — SURVIVED-WITH-INERTNESS, the round's
cleanest specimen.** "True and inert": the integer never-zero mass claim is
a theorem (conceded unbreakable — C1 held, 109/109 one-tick heals held, C4
held by construction), and X6 proves nothing consumes it — "the most
expensive decoration in the organism." This is exactly the third verdict
category, delivered with a measured zero-consumer proof rather than a quote.

**(d) Weakness-drive 12/15.** W3 driven to the zero-consumer proof (X6) ✓;
W5 driven twice (X2 replay measured, X3 input-size) ✓. −2: the packet's
costume quantification ("which fraction of the ~10k-line organism is
load-bearing vs pheromone") was answered by consumer-grep, not LOC fraction;
the QUF ceiling was extrapolated (~1.2 GB from measured 300 KB/tx), not run
to saturation as ordered ("run to true saturation… or show it never
plateaus").

**(e) House law 10/10.** Every verdict measured or cited; held-claims
scoreboard (C1, C2, C4, C7 basics, fold mechanics all HELD and said so);
"the most honest WEAKNESS.md on the board" — respect booked, not exploited.
No float decided anything; no misrepresentation found.

---

## 2. ORGANISM attacks PROCESSION — 100/100

**(a) Reproduction honesty 25/25.** 35/35 tests (~195 ms, own timing); drill
gate 18 drills / differential 0; scenario 5/5; the 2,100-landing flood
re-run in their own probe with exact counts (committed=2000, refused=100,
deferred=233, `scale == −deck`, BigInt); LOC honesty re-measured (455/1,210
= 37.6% vs claimed ~37%). Zero discrepancies, zero smoothing.

**(b) Exploits landed 30/30.** Four landed + three scoped, each with exact
inputs/outputs and committed logs (referee grepped `probe2-results.txt`):
- **B1 — totality hard-rule break (novel):** three corrupt images throw raw
  `TypeError` out of `unfoldCell` (`fold.ts:128-130` unguarded
  `kind.length`; `fold.ts:160` catches only ParseErr — referee confirmed
  both); three other images load *silently* as `undefined` half-states. C5's
  "never a throw, never a partial load" falls in both directions, on inputs
  their single-char fuzz cannot reach.
- **B2 — round-trip break with ledger forgery (novel):** space/newline in a
  nonce is reachable state; `decode(encode(x))` then refuses — the cell
  cannot warm-restart from its own fold. Worse: nonce `x code=R-STICKY-PARKED`
  round-trips a *forged refusal code onto a commit that never refused*,
  truncates the nonce (re-commit after restart = idempotence dead), drops a
  formation posting, and breaks canonicality (199 B vs 165 B — in the log).
  Root cause one line: grammar is space-delimited (`fold.ts:43`), tokens
  never validated.
- **B3 — bounded-state hard-rule break (their W3, quantified):** 50,000
  phantom arrivals → 50,003 ledger entries, 17,177 KB fold (352 B/refusal),
  heap +19,600 KB, O(ledger) unfold.
- **B4 — phantom gate bypass (novel):** no sign check anywhere:
  +620/−600/−20 tenths → **3 fish in the hold, 0 pounds booked** (log line
  71-72); a count-only balanced commit satisfies `R-FISH-UNBOOKED`
  (`scenario.ts:127`). Honest scoping: custody still balances — the
  *semantics* decouple, not the invariant.
- B5 (view refusals never booked), B6 (tick wedge survives restart), B7
  (cross-src nonce collision) — scoped correctly, with the concession that
  same-src replay *is* refused.
- **Self-caught probe defects:** the first pass (P1–P12) was corrected into
  a second pass (Q1–Q9); both raw logs committed. Rigor bonus, earned.

**(c) Deepest-bet verdict 20/20 — BROKEN, four measured counterexamples.**
The kill: C2's machine-checked one-semantics guarantee *certifies a
falsehood* — `R-OVERFLOW`'s lesson says "the bound is a dial… bind it
higher, on the record" (`reasons.ts:55`), but no verb can bind an account
bound (`core.ts:163`: `dialSpecs` only → `R-DIAL-UNKNOWN` ×4 measured);
consistency amplifies error into authority, booked into the ledger and the
docs at 03:00. Then: books that lie post-restart (B2), a refusal surface
persistence rewrites (Q3: refused pre-restart, commits post-restart), and a
differential invariant under operator competence (fixed "press 2" policy =
66.7%, differential stays 0 — it contains zero bits about operators). The
booked concession for genuine value (grep-able lessons, real containment)
keeps it honest.

**(d) Weakness-drive 15/15 + beyond.** W3 → bounded-state falsifier with
bytes-per-refusal and slope; W1 → the thrown-path denominator exhibited
concretely (the TypeError class is exactly the unregistered boundary W1
admits). Beyond orders: they *built the W9 instrument* (`tutor-measure.ts`,
two-pass protocol, null controls: robot-2 → Δ=0 at the six predicted
positions, records committed) — turning procession's "we did not measure
learning" into a measured-zero-plus-a-shipped-meter. That is the rarest
attack move: closing the target's gap while proving it was open.

**(e) House law 10/10.** Dense citations; concessions explicit; no float; no
misrepresentation (the `tutor.ts:131-136` "cas h" detail referee-verified).
Clean sweep.

---

## 3. PROCESSION attacks DEADBAND — 98/100

**(a) Reproduction honesty 25/25.** 55 tests; `measure.py` matches DEFENSE
**cell for cell** (full D2 table re-printed from their own run); D3 both
arms reproduced; floor 1/2×2=1 exact. Bonus honesty: they found the
drift-trig arm's `lkg=472` expiry storm that DEFENSE's table omits — and
booked it as a detail (W5 already owns the label), not a hit. Zero
discrepancies.

**(b) Exploits landed 28/30.**
- **E1 — mis-dial rho (the packet's ordered exploit, landed as premise-
  break):** one fixed realized world (K=2 flips/tick = their own D3 world
  speed, rho_real=2), dial swept: at every dial 1/8…3/4 — *including their
  design point 1/2* — the runtime accepts 10 fish moves, **9 of 10
  materially wrong** (custody booked against a flipped label; `covBAD=0`
  in every row). Killer citations referee-verified: `fabric.py:120-127`
  (judge uses `obs.rho`), `audit.py:34-44` (`support_bound` from the dial),
  `benches/measure.py:63-64` (covBAD checked against dialed support —
  tautological by construction, which concession #2 books as the finding).
- **E2 — deferral is terminal:** at `rho*F >= margin`: 240 audits spent,
  239 pending bookings, 0 resolutions; `resolve_pending` has exactly one
  caller in the tree — a test (`cell.py:186-189`; referee grep: defined
  :188, sole caller `tests/test_fish.py:115`). No runtime verb drains the
  shelf: bounded state, unbounded deferral *duration*. "They built the
  refusal and never built the return."
- Concessions exemplary: bounded state (D5) held under everything; covBAD
  unbreakable through the public API (booked as structural); fold and exact
  arithmetic untouched; D3's contrast reproduced and explicitly *not* called
  misrepresentation. −2: both landed items are premise/liveness exploits —
  no state, conservation, or fold break; the E1 seam was conceded in words
  by deadband's W2/W5 (procession's contribution is the quantification,
  which is real: the interval, the 9/10, the wrong-species custody).

**(c) Deepest-bet verdict 20/20 — BROKEN as champion thesis, SCOPED as
theorem.** E4: one world, two dials — "sits exactly on the floor" at heights
1 and 4, wrong bookings 9/10 vs 0/10, both covBAD=0: *the exhibited floor is
a readout of the dial, not the world.* Mis-dial interval booked: ≥7/8 in
dial units, unbounded below, no operator-visible signal across it. The
Switch Test consequent driven home with E2's measured empty regime —
"we refuse more honestly" is a negative superiority whose cost face is
"booked nothing, permanently, at full audit spend"; the wrongness-amplifier
resonance (drift-trig 10/10 wrong vs static 1/10 at K=4) shows the adaptive
policy adapts to the dial, not the world.

**(d) Weakness-drive 15/15.** W2 → the mis-dial interval as a booked number
+ the no-signal finding. W3 → the productivity cliff table (K-sweep with
the K=240 internal control proving the harness doesn't fabricate wrongness),
rescue price 48 audits/fish, and the sharpest line of the round: "the cliff
is a *dial* cliff, not a world cliff — productivity is gated on operator
knowledge, and the runtime offers no path from observation to dial."

**(e) House law 10/10.** Integer counts; internal controls; concessions;
no float; no misrepresentation.

---

## 4. DEADBAND attacks LEDGER — 97/100

**(a) Reproduction honesty 25/25.** All reproduced with own numbers and
file:line back-citations: 39 tests; 1,465,456 events/s (bench) and
1,458,669 (harness); 34.0 checks/event; 16.38 µs close; 23.06 ms replay;
9,216 B image; **5002/5002 zero closes**; audit overhead 21.7–23.6% (their
published bound conservative). Inline numbers corroborated by the referee's
own re-run (REACTIONS.md appendix A). Zero discrepancies.

**(b) Exploits landed 28/30.**
- **Exploit 1 — compensating corruption persists into recovery (landed,
  honestly conditional):** 50/50 sum-preserving injections pass the trial
  balance (parked=None, balance=0) **and survive QUF reload as truth** —
  `quf::decode` never re-derives conservation (`quf.rs:665` →
  `Fabric::from_parts`, which validates account-name uniqueness only,
  `fabric.rs:180` — referee confirmed both). D1's "every transition
  audited" is false in exactly the recovery mode the philosophy advertises.
  The conditional is priced, not hidden: journal retained → replay catches
  100% (measured both sides). Verdict line: "a disk-less/truncated recovery
  silently resurrects corrupted books."
- **Exploit 2 — same-epoch race (W2) confirmed measured:** catch+arrive in
  one epoch → the same 3 fish in `inflight` AND `quarantine`, suspense
  carrying the double-count.
- −2: both exploit surfaces were machine-checked or admitted by the target
  itself (W2/W4; the packet said so) — the new work is the recovery-mode
  persistence demonstration and the measured tables, which is real, but the
  falsification weight rides a pre-conceded seam.

**(c) Deepest-bet verdict 19/20.** Two measured counters: (1) the crash
gate is sum-preservable and the ring then forgets — forensics span measured
per cell (sea 4 epochs, hook 53), so a corruption that outpaces the ring is
provably unrecoverable without the journal W5 lets you truncate: "the book
is the program, and the book is overwritable." (2) `inflight` is bounded in
*encoded size* but unbounded in *quantity* (grew to 120 in 20 batches) —
bounded state ≠ bounded exposure. Verdict: broken in the recovery regime,
scoped in the golden path — with "conceded by the target itself, now
measured" honesty. −1: the per-event-commit comparison in the W1 line is
argued pen-only (no rival available in-lane to measure against — fair, but
it stays pen).

**(d) Weakness-drive 15/15.** W4 → the number the packet asked for:
audit-net coverage is a **step function of journal survival** (0% at
survival 0, ~100% with journal — 50-trial table, no regime in between).
W5 → the forensics-horizon table per cell plus the false-economy pricing
(~1.2 KB/cell saved vs. the only always-on corruption net).

**(e) House law 10/10.** Five booked concessions (golden path unbroken, gate
airtight for unbalanced, codec solid, conservation type-level, no float
anywhere); the fairness note mirroring their own W4 scar onto Seam 1 is
exactly the tournament's culture. No misrepresentation.

---

## 5. LEDGER attacks SHIPWRIGHT — 100/100

**(a) Reproduction honesty 25/25.** Full table reproduced on their host
including the exact fuzz histogram (100,000 ops, all ten buckets) and the
`== 218116 checks, 0 fails => PASS ==` line in both builds; their probe
harness itself runs 100,433 checks, 0 fails, under **both** `-O2` and
ASan/UBSan `-fno-sanitize-recover=all`; sha256 provenance on the verbatim
core.c copy (referee-verified identical: `93de861e…d1fd`); their own timings
*beat* the published ones (12–13 ns vs 24 ns effect) and are booked as host
variance inside the stated envelopes, not as a gotcha.

**(b) Exploits landed 30/30.**
- **Exploit 1 — the fold is the mint (the round's hardest single exploit):**
  `core.c:412` loads account values with no sign, custody, or consistency
  check (referee-verified line-exact). A1: mint 10 fish into HOLD — 16 bytes
  touched (8 body + 8 checksum), 17.9 µs end-to-end, loads `ST_OK`, **the
  forged image round-trips byte-exact** (it is canonical — a valid state,
  not corruption), view reports 11 `VD_ACCEPT`. A2: mint then move through
  verbs — C7's phantom refusal never fires (no custody-origin check exists).
  A3: drain 40→0, no receipt. A4: negative account values load. The honest
  two-sided statement is booked: corruption-resistant = true (C1–C4 all
  reproduced), forgery-resistant = false (zero bytes of attack surface —
  the checksum is a public function, not a key).
- **Exploit 2 — silent stale-nonce drops:** `core.c:203/220/264/335` return
  `ST_REPLAY` before any booking (referee-verified at 203/220/264); 100,000
  genuinely-new moves issued late: journal delta 0, log delta 0, fold
  byte-identical — the audit window for this class is **zero entries**,
  not 256. "Refused ≠ silent, ever" is true of refusals and false of the
  replay class: the move is gone, nothing refused it, nothing recorded it.
- **Bonus (W4 made runtime-reachable):** legal `qc_effect` moves link-units
  as if custody; the unguarded reversal (`core.c:341-345`, overflow checks
  only) then mints `AC_LINKS = −1` — passing their own 100k-fuzz invariants
  by construction, because the fuzz checks global cuts, never per-cell
  meaning. "Conservation by cut cannot see corruption by kind" — measured,
  end to end, sanitizer-clean.

**(c) Deepest-bet verdict 20/20 — KILL CONDITION MET, by the target's own
clause.** DEFENSE §6: "if a rival can show a duty that NEEDS the sixth
function as a separate verb… this joinery was glue, and we concede." Two
duties shown: (1) CICS two-machine compensating recovery (scouts/STIR-01)
— with measured consequences (the unguarded reversal's −1; the reason-free,
evictable `LK_FORGET` receipt, gone after 256 booked events); (2) GC-T4
escrow/n-ary consent — their own W5: "unrepresentable, not merely unbuilt."
Plus the dodge named: "no verb creates custody" is true and irrelevant —
custody is created by the fold author in ~18 µs with no signature, and
minimalism removed the only place minting could have been *refused*. The
two outs are offered, not demanded: cut forget into a sixth function with
guards and receipt identity, or concede in writing.

**(d) Weakness-drive 15/15.** W11 → the forge cost table (16 bytes / 17.9 µs
/ any account, any value). W7 → the silent-drop count (100k induced, 0 ever
readable). Both exactly the numbers the packet ordered.

**(e) House law 10/10.** C1–C5, C10–C12 held and reproduced in concessions;
the fairness mirror ("my own house shares Seam 1… both are unauthenticated")
is the round's best sentence about the tournament's actual state. No float;
no misrepresentation.

---

## R2 LEADERBOARD (attack round)

| # | attacker → target | A | B | C | D | E | total |
|---|---|---|---|---|---|---|---|
| **1** | **LEDGER → shipwright** | 25 | 30 | 20 | 15 | 10 | **100** |
| **2** | **ORGANISM → procession** | 25 | 30 | 20 | 15 | 10 | **100** |
| 3 | PROCESSION → deadband | 25 | 28 | 20 | 15 | 10 | **98** |
| 4 | DEADBAND → ledger | 25 | 28 | 19 | 15 | 10 | **97** |
| 5 | SHIPWRIGHT → organism | 24 | 29 | 20 | 12 | 10 | **95** |

**Tie-break (booked before application):** (T1) severity of the hardest
single landed exploit against the challenge's core adversarial duty —
LEDGER's 16-byte fold forge (core.c:412) mints phantom custody at the exact
layer duty 4/5 lives, costed and canonical, and is the round's headline
exhibit; (T2) novelty share of landed exploits — ORGANISM (B1/B2/B4 were
conceded by no one; 2 hard-rule breaks + a gate bypass); (T3) count of
hard-rule-class breaks — ORGANISM (totality + bounded state). LEDGER takes
pole on T1; ORGANISM holds T2 and T3. Both scores stand at 100; the order
is a booked tie-break, not a re-grade.

**Field observations.** (1) Every attacker reproduced every headline number
— zero fabrication pressure survived contact; the tournament's honesty
culture is holding. (2) The strongest attacks executed the target's own
booked concessions to measured conclusions (shipwright X2 on organism W5;
deadband on ledger W4; ledger on shipwright W7/W11) — WEAKNESS.md quality is
now a leading indicator of attack surface. (3) Four of five attacks landed
on the fold (see below). (4) STREAM remains unhoused and unattackable;
its packet is still open.

---

## THE THREE-SEAM SYNTHESIS (R2 evidence, folded)

**Seam 1 — the fold is a mint — is no longer a referee hypothesis; it has
two independent, machine-measured exhibits from two teams against two
different substrates:**

1. **LEDGER's 16-byte forge on SHIPWRIGHT** (`core.c:412`): unkeyed
   FNV-1a-64 recomputed over 8 body bytes → arbitrary custody mints, loads,
   round-trips canonical, `VD_ACCEPT` — 17.9 µs per mint, zero verbs
   involved, zero bytes of attack surface.
2. **DEADBAND's reload-persistence on LEDGER** (`quf.rs:665` →
   `from_parts`, no conservation re-derivation): a sum-preserving
   corruption that passes the trial balance **survives QUF reload as
   truth** — 50/50 — because the recovery loader validates names, never
   balances. The fold doesn't just fail to refuse forgery; it launders
   corruption that the live gate already missed.

Different languages, different mechanisms (unkeyed checksum vs.
no-revalidation-on-load), same verdict: **whoever authors the fold is the
mint, and the audit layer authenticates nothing.** Corroboration from the
ring: SHIPWRIGHT's X4 on organism (recompute the public seal → balance lie
loads ACCEPT, `verify_chain` never called on load) and ORGANISM's Q8 on
procession (the fold *writes a forged refusal code onto a commit* and
truncates a nonce with `ok:true`). Four of five attacks landed on or
corroborated Seam 1 — the phantom-custody duty is enforced at the verb
layer and absent at the fold layer, everywhere.

Seam 2 (bounded accounts, unbounded history) confirmed in three places:
organism B3 (17,177 KB fold from 50k refusals, 352 B/refusal), shipwright
X3 (36 MB image from 120 txs, fold reclaims 0 B), deadband's forensics
table (ring span 4–53 epochs). Seam 3 (rho·F priced against a dial)
confirmed quantitatively by procession E1/E4: the floor is a readout of
the dial, wrong bookings 9/10 at the design point, covBAD blind across a
≥7/8 dial interval.

## THE GAUNTLET OPENING PROBLEM — "add a lock to the mint"

The champion's first defense (Shell 4, round 1): **fold authentication
without breaking one-command run or bounded images.** Booked constraints,
falsifiable acceptance:

1. **The lock must hold against the two R2 exhibits as acceptance tests:**
   a forged image with a *recomputed* checksum/MAC and no key must be
   refused with a booked reason (kills exhibit 1); a reload must re-derive
   or re-verify whatever conservation/consistency the live gate claims
   (kills exhibit 2). One machine-checked test per exhibit, integer
   verdicts.
2. **One-command run survives untouched:** `make` / `cargo test` / `npm
   test` still pass with zero external ceremony — no PKI, no network, no
   manual key step. An auth story that costs the one-command property has
   bought a lock by selling the house.
3. **Images stay bounded:** shipwright 9,448 B fixed, ledger 9,216 B fixed —
   auth material fits the fixed budget or the growth is booked in bytes.
4. **No float decides anything**, and the key-custody question is answered
   *honestly*: a key embedded in the binary is a lock with the combination
   printed on the safe. The champion may scope the claim (authenticated
   against all accidental corruption and all unkeyed forgery; key secrecy
   delegated to operator custody, booked as such) — but the scope must be
   written, not implied.

This is the right opener because R2-PACKETS named it the one seam no team
had a defense for, and R2 has now weaponized it twice from different
houses. A champion that cannot survive its own round's sharpest finding
cannot survive the Gauntlet.

## R3 HYBRID GO/NO-GO (from referee/REACTIONS.md, updated by R2 evidence)

**DEADLEDGER (D×L, R3-A) — GO. Priority 1.** R2 made the case stronger
than the chemistry did: deadband measured ledger's recovery regime (their
exploit becomes the hybrid's acceptance test — reload must re-validate or
authenticate, Seam 1 carry-over); ledger's `inflight` (D4) and deadband's
deferral counters (D1) are the same floor in two ledgers; deadband's E2
finding ("refusal needs a refund mechanism; they did not build one") is
answered by ledger's quarantine/forget machinery; the CICS machine-
identity field is one label + one dial on a substrate that already has
both machines. Both teams' R2 conduct (deadband's fairness mirror, ledger's
seam-1 mirror) shows they can merge without ego. No blockers.

**SHIPSTREAM (S×T, R3-B) — CONDITIONAL GO.** The chemistry is right
(golden C as executable spec for the silicon; iverilog/verilator present)
and R2 *raised* the stakes: the checksum seam is now a demonstrated
forgery class (16 bytes, 17.9 µs), so the hybrid's CRC16-vs-FNV question
becomes "close it or book the collision class" with a working attack as
the test vector, plus machine-identity receipts on reversals (ledger's
kill-condition verdict gets its field trial here). **Condition:** STREAM
must deliver a DEFENSE.md + WEAKNESS.md + a runnable suite (R2-PACKETS §0
standard) before the R3 dock. If it does not: NO-GO on S×T, and the
pre-approved fallback is the S×L alloy (REACTIONS: complementary witnesses
— each closes the other's only corruption hole; ledger's own fairness note
already concedes the shared scar).

**SYNAPTIC STREAM (O×T, R3-C) — CONDITIONAL GO, with a sharpened kill
clause.** Stream dependency as above. R2 evidence cuts both ways:
shipwright's X6 measured organism's Hebbian layer at *zero runtime
consumers* — so the hybrid's claim 4 ("the masses finally read": `w`
weights FIRE fanout and VIEW ranking) is now the load-bearing claim of the
entire compound, and falsifier (d) ("a proof that `w` never influences any
outcome") is already half-met in Python. GO with the clause: if silicon
`w` cannot move one measured outcome, O-W3 stands permanently and claim 4
is withdrawn on the record. Fallback if STREAM misses the dock: O×L
STABLE (metabolism on the audit substrate; the heal re-registers as one
epoch, C2 re-scoped honestly).

**R3 dock condition, all three hybrids:** every hybrid inherits its
parents' R2 exploits as regression tests — a compound that forgets its
parents' scars starts the next round already broken.

---

*End of R2-SCORES. House law: every verdict above cites a file:line or a
measured number; the referee re-verified one killer citation per attack on
this host before scoring; no float decided any verdict; scores are integers;
the tie-break was booked before it was applied.*
