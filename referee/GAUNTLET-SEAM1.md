# GAUNTLET-SEAM1 — Opening Problem: "Add a Lock to the Mint"

*Referee · Shell 4 opener · drafted 2026-08-29 from R2-SCORES.md (the Gauntlet
section) and R2-PACKETS.md. House law holds: every claim cites file+line or a
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

## 2. Acceptance tests (verbatim from the two R2 exploits)

Both tests are machine-checked, one command, integer verdicts
(PASS/FAIL, no floats, no network).

### Test G1 — forged fold receipt must be REJECTED at load

Reproduce LEDGER→SHIPWRIGHT Exhibit A as the test vector:

1. Take a legitimate fold image; mint custody by modifying 8 body bytes
   (e.g. +10 fish HOLD / +10 matching tally) and recomputing the
   checksum/MAC over the result, **without any key** (the R2 attack cost:
   16 bytes touched, 17.9 µs).
2. Attempt `qc_unfold`-equivalent load.
3. **PASS iff:** the load is refused with a **booked reason** (not a crash,
   not a silent partial load, not `ST_OK`). The refusal must be a
   distinguishable, citable reason code — "refused ≠ silent, ever" applies
   to the fold layer now.
4. **FAIL conditions:** load succeeds (`ST_OK`/equivalent); load succeeds
   with round-trip canonicality (the forged image is accepted as a valid
   state — this is exactly the R2 outcome and it fails); view reports
   `VD_ACCEPT` on phantom custody.

### Test G2 — sum-preserving corruption committed then reloaded must be DETECTED

Reproduce DEADBAND→LEDGER Exhibit B as the test vector:

1. Commit a sum-preserving `+7/−7` corruption across two accounts
   (gate-evasive by construction — R2 measured 50/50 pass the trial
   balance; journal-retained replay catches 100%, journal-absent catches
   0%).
2. Fold, then reload the image **with no journal** (the recovery regime the
   philosophy advertises).
3. **PASS iff:** the corruption is **either rejected with a booked reason or
   visibly quarantined** (an operator-readable marker, not a silent load).
   Re-derivation of the live gate's claimed invariants on load, or an
   authenticated fold that the corrupted hand-edit cannot satisfy, both
   qualify.
4. **FAIL condition:** **silent acceptance** — the corrupted balances load
   as truth with no signal. This is the exact R2 outcome ("a disk-less/
   truncated recovery silently resurrects corrupted books") and it fails.

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
| **A. authentication strength** | 40 | G1 and G2 pass machine-checked (20 each). Partial credit only for verified quarantine paths on G2. Claim-scope honesty is scored here too: the written custody section (§4) must match what the tests actually demonstrate — no embedded-key solution scored as operator-key-security. |
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

*End GAUNTLET-SEAM1. House law: every claim above cites a file:line or a
measured number from the R2 record; no float decides a verdict; the lock is
judged against the two exploits that opened it.*
