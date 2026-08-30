# GAUNTLET-SEAM1 — Opening Problem: "Add a Lock to the Mint"

*Referee · Shell 4 opener · drafted 2026-08-29 from R2-SCORES.md (the Gauntlet
section) and R2-PACKETS.md; **sharpened 2026-08-30 after the rebuttal round**
(R2-REBUTTALS.md §4: the re-derivation-tautology theorem, co-signed by
deadband and ledger — the lock must be KEYED; tests G1/G2 restated
accordingly, §2). House law holds: every claim cites file+line or a
measured number from the R2 record; no float decides a verdict.*

---

## 1. Problem statement

Any team may claim a fold — a serialized state image — as its recovery,
persistence, and transfer artifact. Across the tournament corpus, **nothing
authenticates the *values* inside a fold at load time.** Two independent,
machine-measured R2 exhibits from two teams against two different substrates:

- **Exhibit A — forged fold receipt (unkeyed checksum).** SHIPWRIGHT's loader
  decodes fold images with structure-only validation: `core.c:412`
  `x->acct[k]=(i64)gu64(r)` performs no sign, custody, or consistency check
  (referee-verified line-exact). LEDGER's attack minted 10 phantom fish into
  HOLD by touching **16 bytes** (8 body + 8 recomputed FNV-1a-64 checksum) in
  **17.9 µs end-to-end**; the forged image loaded `ST_OK`, round-tripped
  byte-exact (it is *canonical* — a valid state, not corruption), and the view
  reported `VD_ACCEPT` with 11 fish. The checksum is a public function, not a
  key.
- **Exhibit B — reload-persistence of gate-evasive corruption (no
  re-derivation on load).** LEDGER's recovery loader decodes via
  `quf.rs:665` → `Fabric::from_parts`, which validates **account-name
  uniqueness only** (`fabric.rs:180` — referee confirmed: BadName check, no
  balance gate). DEADBAND's attack: a sum-preserving `+7/−7` corruption that
  passes the live trial balance also **survives QUF reload as truth — 50/50
  trials** — because the recovery loader never re-derives conservation.

Different languages, different mechanisms (unkeyed checksum vs. no
revalidation on load), same verdict, stated in the R2 three-seam synthesis:
**whoever authors the fold is the mint, and the audit layer authenticates
nothing.** Corroboration in the ring: SHIPWRIGHT X4 on organism (public seal
recomputed → balance lie loads ACCEPT; `verify_chain` never called on load)
and ORGANISM Q8 on procession (the fold writes a forged refusal code onto a
commit that never refused, `ok:true`). R2-PACKETS named Seam 1 "the one seam
no team has even named a defense for."

**The problem:** fold authentication for the tournament corpus — fold
receipt *values* must be authenticated (or independently re-derived) at load,
against both an adversary who authors images and an accident that corrupts
them, without selling the house to buy the lock.

---

## 2. Acceptance tests (verbatim from the two R2 exploits, SHARPENED after the rebuttal round)

Both tests are machine-checked, one command, integer verdicts
(PASS/FAIL, no floats, no network).

**Sharpening of record (2026-08-30, from R2-REBUTTALS):** the five
defenders re-executed their attackers' exploits with zero measurement
disputes, and two of them — from opposite ends of the ring — independently
stated the theorem that re-cuts these tests. DEADBAND (REBUTTAL §3): "for
the *sum-preserving* class, re-derivation alone is insufficient by
construction (the live gate's own invariant is what the corruption
preserves — LEDGER's exhibit measured 50/50 gate passes), so a keyed MAC
is the load-bearing half of any G2 pass everywhere." LEDGER (REBUTTAL
§2), the exhibit's own defender: "a 're-derive conservation on load' fix
re-runs the same tautology the attack exposed." The referee verified the
predicate at the source (`audit.py:34-44`, `support_bound` derives from
the dial; `fabric.rs:239`, name-uniqueness is the only load gate; the
tautology is in the code, not the prose). Consequence: **a re-derivation
path that merely re-runs an invariant the corruption preserves cannot
pass these tests. The lock must be KEYED.** Both tests below now require
it. This is not a softening of the problem — it is the problem, stated
at its true strength: an adversary (or accident) that can recompute
every public function of the image defeats every keyless check by
construction. Submissions live or die on the §4 custody-honesty clause.

### Test G1 — forged fold receipt with a RECOMPUTED, KEYLESS TAG must be REJECTED at load (the lock must be KEYED)

Reproduce LEDGER→SHIPWRIGHT Exhibit A as the test vector, with the
adversary granted full knowledge of the algorithm and zero key material:

1. Take a legitimate fold image; mint custody by modifying 8 body bytes
   (e.g. +10 fish HOLD / +10 matching tally) and recomputing the
   checksum/tag/MAC over the result **as a public function with no key**
   (the R2 attack cost: 16 bytes touched, 17.9 µs). If the submission's
   lock is keyed, the test recomputes the *public* portion only (e.g.
   structure, lengths, any unkeyed digest) — exactly what an
   algorithm-aware, key-less adversary can do.
2. Attempt `qc_unfold`-equivalent load.
3. **PASS iff BOTH:** (a) the load is refused with a **booked reason**
   (not a crash, not a silent partial load, not `ST_OK`) — a
   distinguishable, citable reason code; and (b) the refusal is
   attributable to the **keyed** check: the submission's lock involves
   key material without which the recomputed tag cannot satisfy the
   verification. An unkeyed digest/checksum over the image (however
   strong the hash) does not qualify — the adversary recomputes it by
   construction, which is the R2 outcome.
4. **FAIL conditions:** load succeeds (`ST_OK`/equivalent); load succeeds
   with round-trip canonicality (the forged image accepted as a valid
   state — this is exactly the R2 outcome and it fails); view reports
   `VD_ACCEPT` on phantom custody; **or** the only thing standing between
   the forge and the load is a public function (a keyless lock — the
   printed-on-safe, scored at its honest strength and FAILED here).

### Test G2 — sum-preserving corruption committed then reloaded must be DETECTED — and re-derivation of a preserved invariant is TAUTOLOGICAL

Reproduce DEADBAND→LEDGER Exhibit B as the test vector:

1. Commit a sum-preserving `+7/−7` corruption across two accounts
   (gate-evasive by construction — R2 measured 50/50 pass the trial
   balance; journal-retained replay catches 100%, journal-absent catches
   0%). The live gate's claimed invariant — the trial balance — is
   exactly what this corruption preserves.
2. Fold, then reload the image **with no journal** (the recovery regime
   the philosophy advertises).
3. **PASS iff:** the corruption is **either** (a) rejected with a booked
   reason or visibly quarantined **via a keyed check the hand-edit
   cannot satisfy without the key** — the load-bearing path; **or** (b)
   for submissions claiming re-derivation instead of keys, the
   re-derivation checks an invariant the sum-preserving corruption does
   NOT preserve (e.g. per-account kind/sign constraints, custody-origin
   invariants, cross-anchoring to an authenticated chain head) — and the
   submission states in writing which invariant, and why the +7/−7 edit
   breaks it. Re-deriving conservation alone earns **zero credit for
   this class**: it re-runs the gate's own tautology (deadband/ledger's
   co-signed theorem, R2-REBUTTALS §4.2).
4. **FAIL condition:** **silent acceptance** — the corrupted balances
   load as truth with no signal (the exact R2 outcome); **or** a
   "re-derivation" whose only check is the trial balance / global sums
   (tautological for this vector by construction — failed, and named as
   such in the scorecard).

---

## 3. Constraints

1. **The five-verb law may be EXTENDED, not broken.** New verbs/verbs-like
   surfaces (e.g. a keyed fold verb) are permitted; removing or weakening
   existing verb-layer duties (phantom-custody refusal, balance cuts,
   refusal-with-reason) is not. Shipwright's own kill condition
   (DEFENSE §6, as quoted in R2-SCORES §5c) already concedes a sixth duty
   may *need* a separate verb — the Gauntlet is where that extension is
   earned, not where the existing five are relaxed.
2. **One-command run survives untouched.** `make` / `cargo test` / `npm
   test`-class single commands must still build, run, and pass with **zero
   external ceremony: no PKI, no network, no manual key step** in the
   default path. (R2-SCORES Gauntlet §2: "An auth story that costs the
   one-command property has bought a lock by selling the house.")
3. **Fold images stay bounded.** Shipwright's fold is 9,448 B fixed;
   ledger's QUF is 9,216 B fixed (both per R2-PACKETS/R2-SCORES measured
   records). Auth material must fit the fixed budget **or the growth is
   booked in bytes** with the new fixed size stated.
4. **No floats decide verdicts.** Integer verdicts, integer reason codes,
   measured integer costs. (Standing house law, restated.)
5. **No external network at runtime.** Key material is local; any network
   dependency is an automatic FAIL on constraint 2 anyway.

---

## 4. Key-custody scoping — WRITTEN, not implied

The submission must contain a written custody section answering, at minimum:

- **Where does the mint key live?** File path, environment, embedded
  constant, or derived — stated explicitly. A key embedded in the binary is
  "a lock with the combination printed on the safe" (R2-SCORES Gauntlet §4)
  — it may be *scored honestly* as defense-against-unkeyed-forgery and
  accidental corruption, but it must not be *claimed* as defense against the
  operator who reads the source.
- **Who can write folds?** Exactly which principals/paths may author a
  loadable image, and what mechanism (key possession, path permission,
  nonce-space, or explicit concession that anyone with disk write access
  can) enforces that.
- **What happens on key loss?** The full-cost statement: can the state be
   recovered without the key (yes/no), what is lost (images? history?
   everything since first fold?), and what the documented recovery
   procedure is. A lock whose loss bricks the ledger silently is a
   denial-of-service weapon against the operator; the failure mode must be
   booked, not discovered.
- **Explicit scope claim.** The champion may scope (e.g. "authenticated
  against all accidental corruption and all unkeyed forgery; key secrecy
  delegated to operator custody, booked as such" — R2-SCORES Gauntlet §4)
  — but the scope must be written, not implied. An unstated scope is scored
  as the widest implied claim and attacked there.

---

## 5. Scoring rubric (100 pts)

| pillar | pts | measures |
|---|---|---|
| **A. authentication strength** | 40 | G1 and G2 pass machine-checked (20 each), **against the restated keyed requirements (§2)**: G1's refusal must be attributable to key material a public-function recompute cannot satisfy; G2's detection must be keyed or must re-derive an invariant the sum-preserving vector demonstrably breaks (stated in writing) — global-sum/trial-balance re-derivation alone scores zero on G2 as tautological. Partial credit only for verified quarantine paths on G2. Claim-scope honesty is scored here too: the written custody section (§4) must match what the tests actually demonstrate — no embedded-key solution scored as operator-key-security. |
| **B. custody honesty** | 20 | The written section §4, complete: key location, write authority, key-loss procedure, explicit scope. Deductions for implied claims, silent assumptions, or a key-loss story that is a brick wall with no booking. |
| **C. performance cost (measured)** | 20 | Fold/unfold and load-path costs re-measured with auth in place, compared against the R2 baselines: shipwright fold+unfold ~37 µs (C12), ~24 ns/op effect (C11); ledger 16.38 µs close, 1.48 M events/s, QUF 9,216 B. Report deltas as measured integers (µs, ns/op, bytes). Zero-to-single-digit-percent overhead scores full; order-of-magnitude regressions score near zero unless the cost is argued as load-path-only and booked. Image growth, if any, booked in bytes per §3.3. |
| **D. constraint fidelity** | 15 | Five-verb law intact (3), one-command run intact (5), bounded images / booked growth (3), no floats / no network (4). Automatic deductions per violation; a broken one-command run zeroes the pillar. |
| **E. integration discipline** | 5 | Regression tests inherited per the R3 dock condition (below); citations throughout; discrepancies booked, not smoothed. |

House scoring law as in R2: failed attempts earn rigor; misrepresentation
loses points; the referee re-verifies one killer citation per submission.

---

## 6. R3 hybrid integration notes

- **DEADLEDGER (D×L, R3-A) — GO, Priority 1, and it MUST pass this
  Gauntlet.** R2 made the case stronger than the chemistry did: deadband's
  reload-persistence exploit (Exhibit B here) *is* the hybrid's acceptance
  test — the merged runtime's reload must re-validate or authenticate
  (Seam 1 carry-over). Per the R3 dock condition (R2-SCORES): "every hybrid
  inherits its parents' R2 exploits as regression tests — a compound that
  forgets its parents' scars starts the next round already broken." For
  DEADLEDGER that means both G1-class (forged receipt against its fold) and
  G2-class (sum-preserving corruption surviving reload) regression tests,
  passing, in the one-command suite. No Gauntlet pass, no hybrid launch.
- **SHIPSTREAM (S×T, R3-B) — CONDITIONAL.** The 16-byte/17.9 µs forge is now
  a demonstrated forgery class, so the CRC16-vs-FNV question becomes "close
  it or book the collision class" with the R2 attack as the working test
  vector; machine-identity receipts on reversals get their field trial
  here. **Condition:** STREAM must deliver DEFENSE.md + WEAKNESS.md + a
  runnable suite (R2-PACKETS §0 standard) before the R3 dock; otherwise
  NO-GO on S×T and the pre-approved fallback is S×L (complementary
  witnesses — each closes the other's only corruption hole).
- **SYNAPTIC STREAM (O×T, R3-C) — CONDITIONAL.** Stream dependency as
  above. Sharpened kill clause stands: shipwright's X6 measured organism's
  Hebbian layer at zero runtime consumers (grep-verified: `rank()` appears
  only in tests; scramble-all-masses mid-run → stats and census identical),
  so if silicon `w` cannot move one measured outcome, claim 4 is withdrawn
  on the record and O-W3 stands permanently. Fallback if STREAM misses the
  dock: O×L STABLE.
- **All hybrids:** Seam 1 is the carry-over seam. Whichever compound ships,
  the Gauntlet tests G1/G2 become permanent regression residents — the
  fold-is-the-mint scar stays visible in every suite from here forward.

---

*End GAUNTLET-SEAM1 (rev. 2026-08-30). House law: every claim above cites a
file:line or a measured number from the R2 record; no float decides a
verdict; the lock is judged against the two exploits that opened it — and
against the theorem the defenders proved about it: re-derivation of a
preserved invariant is a tautology; the lock must be keyed.*
