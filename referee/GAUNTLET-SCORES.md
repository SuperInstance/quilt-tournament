# GAUNTLET-SCORES — Seam 1: "Add a Lock to the Mint" — Final Adjudication

*Referee · 2026-08-30 · adjudicated against GAUNTLET-SEAM1 rev. 2026-08-30
(sharpened keyed G1/G2, custody clause §4) and GAUNTLET-GO (rubric §5, lane
brief §3). House law holds: every claim below cites a file:line in the
submission repos or a number the referee measured on this host (WSL2).
Undersell, overdeliver. No float decides a verdict.*

## 0. Referee verification record (what was re-run, by whom — me)

- **LEDGER `cargo test` (re-run by referee):** **47 passed, 0 failed**
  across 6 suites (lib 3, adversarial 13, claims 7, conformance 8, fold 11,
  gauntlet 5; doc-tests 0). Gauntlet suite green, including
  `g1_forged_fold_is_refused_at_load`, `g1_wrong_key_is_refused`,
  `g2_sum_preserving_corruption_cannot_ride_reload`,
  `legacy_v1_images_refuse_not_silent`, `measured_load_cost`.
- **PROCESSION `npm test` (re-run by referee):** **46 passed, 0 failed**
  (206.7 ms), including the 11 new `test/seal.test.ts` tests.
- **SHIPWRIGHT `make` (re-run by referee, fresh key):** **218,160 checks,
  0 fails, PASS**, both builds (O2 + ASan/UBSan). Printed verdicts:
  `G1 forged-fold … REFUSED ST_FOLD_AUTH`, `G2 sum-preserving +7/-7 …
  REFUSED ST_FOLD_AUTH`. Referee-measured forge attempt: **15,999 ns**
  (submission claimed 14,900–15,469 — same order, within bench noise;
  my run is a cold-start run). Referee-measured timings ran noisier than
  the submission's (effect 82 ns/op vs claimed 10; pair 31,815 ns vs
  ~18,000): **verdicts identical, absolute numbers differ between benches —
  booked, not smoothed.** The claims are plausible on an isolated bench but
  the referee's numbers are the record for this host.
- **Key-file modes + gitignore status (all five, checked by referee):**
  - shipwright `qc-mint.key` — **mode 600**, `.gitignore:4` ✓
  - ledger — **no key file at rest**; `.gitignore` contains only `/target`
    (no key path ignored). The mint path `FoldKey::load_or_mint`
    (`src/mac.rs:140`, `mode(0o600)` at `:154`) is **never called anywhere
    in the repo** (grep: only its own definition and a doc reference) —
    the ceremony code exists but is unwired; tests mint in-memory. Booked
    as ledger's main deduction.
  - deadband `deadband-mint.key` — **mode 600**, `.gitignore:4` ✓
  - organism `fold.key` — **mode 600**, `.gitignore:4` ✓ (check-ignore
    confirms)
  - procession — no key at rest (minted on first use, tested in-suite);
    `.gitignore:3` ignores `procession-mint.key` ✓ (check-ignore confirms)
- **Procession pre-existing build breakage (referee-verified):**
  `npm run build` at the submission tree → **105 TS errors**, all
  type-resolution classes (43× TS2591 @types/node, 42× TS2339, 19× TS2345,
  1× TS18048) — zero logic errors. Consistent with the booked claim
  ("105 total, 0 novel classes, all type-resolution"). The "72 errors at
  HEAD pre-lock" stash measurement was **not** re-verified by the referee
  (stash in a nested repo is referee-hostile); the class distribution is
  the verified part.
- **Timing-safe compare (checked in all five sources):**
  - shipwright: `gu64(...) != mac64(...)` at `core.c:486` — plain integer
    compare, **NOT constant-time**.
  - ledger: `fold_tag(...) != bytes[body_len..]` at `src/quf.rs:382` —
    slice compare, **NOT constant-time**.
  - deadband: `hmac.compare_digest` at `cellcore/seal.py:127` ✓
  - organism: `hmac.compare_digest` at `cellcore/foldlock.py:110` ✓
  - procession: `crypto.timingSafeEqual` at `src/seal.ts:50` ✓

## 1. Per-team grades

### SHIPWRIGHT (Lane 1, commit 9f4710c) — 95/100 — PASS

- **G1: PASS (keyed).** `ST_FOLD_AUTH` enum `core.c:81`; fail-closed guards
  `core.c:443` (mint) and `core.c:485` (load); the seal check `core.c:486`
  is a function of `mkey0/mkey1` (`core.c:149`), loaded from `qc-mint.key`.
  Referee re-ran the suite; the refusal line printed. Wrong-key and random-
  tag controls in `test.c` (claimed; suite green).
- **G2: PASS (keyed path).** +7/−7 with public re-tag refused `ST_FOLD_AUTH`
  (referee re-ran; printed). Zero re-derivation credit claimed — the
  tautology theorem honored in writing (LOCK §2). **Ordering control
  (re-seal-under-true-key-passes-the-seal): ABSENT** — shipwright is the
  only team whose G2 proof does not isolate the seal from incidental
  parse failures. The seal is nonetheless the only load gate the edit can
  trip, so the pass stands; the evidentiary gap is booked (−4 on A).
- **Custody (§4): full marks.** Path, 0600 verified, gitignored, outside
  image/binary/git, write authority = key possession, key-loss cost stated
  ("all fold images since first boot"), recovery procedure stated, scope
  claim exact — including the honest concession that keyed-FNV is not
  SipHash and is scored at "keyed MAC, 64-bit tag" strength (LOCK §5).
- **Cost honesty: good.** Same-session baseline, delta indistinguishable
  from noise, honestly undersold. Referee re-run noisier (booked §0).
- **Debt paid in-lane: YES.** `qc_compensate` shipped (`core.c:414`,
  `ST_LINKGUARD` guards at `:391`/`:424`, `LK_COMP` tagged receipt `:435`,
  receipt-kind range check at `:538`) + C-fix reversal guard — both the
  debts GAUNTLET-GO Lane 1 booked. Verified in source.
- **Gaps:** non-constant-time compare (`core.c:486`); 64-bit tag (2^-64
  per attempt — honestly booked); homebrew keyed-FNV PRF (honestly booked,
  no claim of SipHash strength); migration rule present (`ST_FOLD_VER`,
  v1 refused) ✓.
- **Pillars:** A 36 (G1+G2 keyed; −4 ordering control absent) · B 20 ·
  C 18 (claims sane, referee re-run diverged in absolute ns — booked) ·
  D 15 (image 9,448 B unchanged, one command, no network) · E 5 (citations
  verified; debts paid) → **95**.

### LEDGER (Lane 2, commits 4f6fda0 + 050939f) — 82/100 — PASS (with custody deduction)

- **G1: PASS (keyed).** `tests/gauntlet.rs::g1_forged_fold_is_refused_at_load`
  and `g1_wrong_key_is_refused` green on the referee's re-run. Seal gate
  `src/quf.rs:382` before structural parse (`:349` decode order comment);
  `DE_FOLD_AUTH = 14` (`src/quf.rs:40`).
- **G2: PASS (keyed, WITH ordering control — the pattern's first appearance
  in lane order).** `g2_sum_preserving_corruption_cannot_ride_reload` green
  (referee re-run); the ordering control — same edit re-sealed under the
  true key passes the seal and is refused later by a semantic check — is
  in the test and stated in LOCK. Authenticate, then interpret.
- **Custody (§4): the weakest of the five.** The written LOCK section is
  the shortest; it cites `FoldKey::mint` but **never states the key file
  path**; the §4 answers (write authority, key-loss cost, recovery
  procedure) live only in a doc comment (`src/mac.rs:145-150`), not in the
  submission's written section; **`load_or_mint` is never called** — the
  0600 ceremony is dead code as shipped; **no gitignore entry for any key
  path**. Key-loss and migration (`DE_FOLD_LEGACY`, `src/quf.rs:361`,
  tested green) ARE stated. This is a custody *paperwork and wiring* gap,
  not a lock gap — but GAUNTLET-GO §4.2 said the Gauntlet dies here, and
  it costs ledger real points.
- **Cost honesty: honest but thin.** No pre-lock baseline snapshot —
  admitted in writing ("a same-image delta is not claimable"), absolute
  numbers given (decode ~114–136 µs sealed, trailer exactly 16 B,
  bench-scale 118.6/162.8 µs). Booking the gap is worth more than inventing
  a baseline — but pillar C measures decomposed deltas and there are none.
- **Debt paid in-lane: YES.** IFQ overage second book (STIR-03): journal
  `Overage` record (`src/fabric.rs:967`, replay at `:1190`), ring+journal
  split as booked. Verified in source.
- **Gaps:** non-constant-time compare (`src/quf.rs:382`); unwired key
  ceremony; unstated key path; no gitignore. Tag 128-bit (SipHash-2-4
  double-pass, reference vectors cross-checked — good rigor).
- **Pillars:** A 38 (both tests keyed, ordering control present; −2
  constant-time) · B 11 (path unstated in LOCK, ceremony unwired, no
  gitignore; migration + loss stated) · C 12 (no baseline, booked) ·
  D 15 · E 5 → **82**.

### DEADBAND (Lane 3, commit 802467d) — 97/100 — PASS (Seam-1 champion)

- **G1: PASS (keyed).** Wrong-key control, keep-old-tag variant, and
  4,096 random-tag draws (0 loads) all claimed in-test; refusal
  `DE_SEAL_AUTH` (`cellcore/seal.py:123`), constant-time
  (`hmac.compare_digest`, `seal.py:127`). The strongest keyless recompute
  the team could construct (unkeyed SHA-256 truncation — stronger than the
  R2 FNV vector) is the test adversary. Good.
- **G2: PASS (keyed, WITH ordering control).** The exhibit-B attacker
  turned its own attack on its own fold; the ordering control — same edit
  re-sealed under the true key passes the seal with tampered balances
  arriving intact — proves the refusal was the seal. The team that
  co-signed the tautology theorem claims zero re-derivation credit and
  means it.
- **Custody (§4): full marks.** Path, 32 B OS entropy, mode 600 tested
  in-suite (`tests/test_seal.py::test_key_ceremony_file_mode_0600`),
  gitignored, write authority = key read, key-loss cost + recovery
  procedure + exact scope claim (2^-128, not-claimed list) all written.
- **Cost honesty: the best-decomposed relative story.** Same-state,
  same-run keyless baseline method stated; +20–96% relative **with both
  causes named** (HMAC pass + JSON-in-JSON envelope) and the absolute
  delta (~4–8 µs, once per boot) argued as load-path-only; +124 B growth
  booked. Honest that the keyless baseline was the hole, not a lock.
- **Debt paid in-lane: YES.** Mis-dial drift signal (REBUTTAL §2
  direction): `cellcore/fabric.py:110 _drift_signal`, `drift_watch`
  telemetry (`:49`), never a verdict input (dedicated test). E2/E3 remain
  booked as R3-dock debts — correctly not smuggled in half-done.
- **Gaps:** smallest of the five. The +96%-worst-run relative overhead is
  real and booked; envelope re-canonicalization is a future-collision
  surface nobody attacked. No constant-time gap. No ordering gap.
- **Pillars:** A 40 · B 20 · C 17 · D 15 · E 5 → **97**.

### ORGANISM (Lane 4, commit 5115032) — 96/100 — PASS

- **G1: PASS (keyed).** Wrong-key control (refused → true key → ACCEPT),
  keep-old-tag, 1,024 random-tag draws (0 loads); constant-time compare
  (`foldlock.py:110`). Refusal `auth-mismatch` in `quf.decode`.
- **G2: PASS (keyed, WITH ordering control).** Test asserts global sum
  preserved before reload; re-sealed-under-true-key control loads with
  tampered balances intact. Zero re-derivation credit claimed; the keyless
  anchor from the rebuttal is explicitly superseded, not shipped.
- **Custody (§4): full marks**, and the strongest hardening detail of the
  five: mode 0600 enforced at create **and re-chmodded on every read**
  (O_EXCL + chmod belt, in-test verified); env-var override documented;
  full not-claimed list.
- **Cost honesty: the deepest decomposition.** Same-process keyless-v1
  baseline; decode delta ~+95% **split into measured parts** (~3.2 ms HMAC
  + ~3.6–4.3 ms load-time `verify_chain` over 1,331 entries), the chain
  cost correctly attributed to the X1 precondition the referee itself set.
  Image: −1 B (zero growth). Load-path-only argued; verb path shown
  untouched by regression.
- **Debt paid in-lane: YES — the heaviest lane debt.** X1 (stored-kind
  fix, `ledger.py:235-240`; fold anchor `:131`; verifier wired into load,
  `quf.py:87` chain-broken refusal — even a keyed author cannot load a
  broken chain). GAUNTLET-GO made this a precondition; organism paid it in
  full. The Hebbian wire-or-withdraw fork correctly left to its clock
  (referee-accepted, not lane debt).
- **Gaps:** +95% decode relative is the largest booked regression of the
  five (decomposed, argued, and partly the referee's own precondition —
  but the number is the number); suite count (79/79) not re-run by the
  referee (booked; ledger+procession+shipwright were the re-run picks).
- **Pillars:** A 40 · B 20 · C 16 · D 15 · E 5 → **96**.

### PROCESSION (Lane 5, commit cecf40a) — 96/100 — PASS

- **G1: PASS (keyed).** Wrong-key, honest-loads, keep-old-tag controls and
  1,024 random-tag draws all in `test/seal.test.ts`; referee re-ran the
  suite: 46/46.
- **G2: PASS (keyed, WITH ordering control).** Test asserts global sum
  preserved; re-sealed-under-true-key ordering control loads with ±7
  balances arriving intact (`test/seal.test.ts:151`). Zero re-derivation
  credit claimed.
- **Custody (§4): full marks, with two unique strengths:** the only team
  whose tag compare is `timingSafeEqual` **and** whose decode-side key
  loader *refuses* a key file with wrong mode or wrong length (fail-closed
  on the key itself, not just the image). Tutor drills D18/D19 teach both
  new codes with semantic-differential 0 — the lock booked in the house's
  own one-semantics idiom.
- **Cost honesty: good.** Same-image baseline, +1.4–2.7 µs absolute /
  ~+30–40% relative stated both ways, +69 B booked at fixed size.
- **Debt: NONE owed in-lane** (B1–B7 booked to R3-dock/future lanes by the
  entry verdict) — and the team correctly resisted smuggling Q3
  re-derivation in as G2 credit. The pre-existing tsc breakage is booked,
  not smoothed, and the referee verified its class distribution (§0).
- **Gaps:** none in the lock itself. The build surface (`npm run build`)
  remains broken at the submission tree — pre-existing, environment-class,
  verified type-resolution-only, and the green one-command path (`npm
  test`) is intact; −1 on D for the unresolved surface.
- **Pillars:** A 40 · B 20 · C 17 · D 14 · E 5 → **96**.

## 2. Seam-1 standings

| rank | team | score | lock | tag | ct-compare | ordering ctrl | custody | debt paid |
|---|---|---|---|---|---|---|---|---|
| 1 | DEADBAND | 97 | HMAC-SHA256, 16 B | 2^-128 | ✓ | ✓ | full | drift signal |
| 2 | ORGANISM | 96 | HMAC-SHA256, 32 B hex | 2^-256 | ✓ | ✓ | full+hardening | X1 (precondition) |
| 2 | PROCESSION | 96 | HMAC-SHA256, 64-hex | 2^-256 | ✓ timingSafe | ✓ | full+key-guard | none owed |
| 4 | SHIPWRIGHT | 95 | keyed FNV-1a-64 ×2, 8 B | 2^-64 | ✗ | ✗ absent | full | qc_compensate + C-guard |
| 5 | LEDGER | 82 | SipHash-2-4 ×2, 16 B | 2^-128 | ✗ | ✓ first | paperwork+wiring gap | IFQ overage |

Tie-break at 96: organism paid the heaviest lane debt (the X1 precondition)
and decomposed its cost deepest; procession is even on the lock itself and
cleaner on environment honesty. Booked as a coin-width margin, not a
verdict on lock quality — both locks are champion-grade.

**All five PASS G1 and G2 as keyed.** The seam the R2 record called "the
one seam no team has even named a defense for" is closed five-for-five,
in five languages, with the same architecture converging independently.

## 3. Cross-team synthesis

- **Strongest per dimension:**
  - **Tag strength:** organism / procession (256-bit HMAC-SHA256) over
    deadband/ledger (128-bit) over shipwright (64-bit, honestly booked).
  - **Custody:** deadband / organism / procession / shipwright (full §4,
    all verified) — organism's re-chmod-on-read and procession's
    key-file-mode gate are the hardening details worth copying fleet-wide;
    ledger trails (path unstated, ceremony unwired, no gitignore).
  - **Fail-closed semantics:** procession (no-key refused, key-file
    hygiene, decode never mints) and deadband (three-code ladder,
    both directions tested) — with organism's chain-broken-under-true-key
    as the deepest fail-closed statement of the round.
  - **Cost accounting:** organism (decomposed to component level,
    X1 cost attributed to its true cause) and deadband (both overhead
    causes named, relative + absolute given) — ledger's no-baseline
    admission is the honesty benchmark and the accounting gap at once.
  - **Migration rule:** five-for-five stated, never silent — every team
    refuses legacy images with a dedicated code (`ST_FOLD_VER`,
    `DE_FOLD_LEGACY`, `DE_FOLD_LEGACY`, `legacy-image:v1`,
    `R-UNSEALED-FOLD`). The house converged on "re-author under the key."
- **The shared proof pattern — authenticate, then interpret.** All five
  teams independently converged on the same decode order (magic →
  version/legacy → **keyed tag** → structural parse → semantics) and four
  of five shipped the same *ordering control*: re-seal the corrupted image
  under the true key, show it passes the seal, and is then judged on
  semantics — isolating the seal as the refusal's cause. Ledger named the
  pattern in prose; deadband, organism, and procession shipped it as
  tests; **shipwright alone omitted it** (booked, −4). This control is
  now house-standard evidence for any keyed-lock claim.
- **Gaps nobody closed:**
  1. **Constant-time comparison: 2 of 5.** shipwright (`core.c:486`,
     integer `!=`) and ledger (`src/quf.rs:382`, slice `!=`) verify tags
     with early-exit-able compares. The G1 adversary of record is
     offline (recompute-and-retry), so this is not a pass/fail defect
     under §2 — but it is a live side-channel surface every sealed fleet
     inherits, and it is booked here as Seam-1 debt. Fix is one line in
     each: XOR-accumulate (C), fold bytes into a u8 or (Rust).
  2. **Key-ceremony wiring:** ledger's `load_or_mint` is dead code as
     shipped — the only 0600 ceremony in the corpus with no caller.
  3. **No team shipped a key-rotation/re-seal verb** (re-authoring under a
     new key is a manual state event in all five write-ups). Loss-of-key
     cost is booked everywhere; cheapening it is not.
  4. **No cross-image chaining:** organism's chain-broken-under-true-key
     is the only anchor tying image *history* to the seal; no one else
     binds fold N to fold N−1.
- **Pre-existing breakage booked:** procession `tsc` at the submission
  tree — 105 errors, all type-resolution classes (referee-verified §0),
  pre-dating the lane per the team's stash measurement (not re-verified;
  class distribution is). The green one-command path is `npm test`, and it
  is green.

## 4. R3 go/no-go (carried from R2-SCORES, now with the Gauntlet fact)

- **DEADLEDGER (D×L): GO.** Both parents passed the Gauntlet (deadband 97,
  ledger 82, both G1+G2 keyed, both exhibit-authors against their own
  exhibits) — and the GAUNTLET-SEAM1 §6 condition (G1-class and G2-class
  regressions passing in the one-command suite, both parents' scars
  inherited) is satisfied by both submissions' own suites. The hybrid must
  keep them resident.
- **SHIPSTREAM (S×T): still CONDITIONAL — and the condition is now failing
  on the clock.** Shipwright passed its lane (95, forge refused, debts
  paid), but STREAM did not enter the Gauntlet at all — no DEFENSE.md, no
  WEAKNESS.md, no runnable suite in `teams/stream/`. Stated plainly, no
  penalty invented: **the stream has not delivered a house.** If it misses
  the R3 dock, the pre-approved fallback S×L stands — and ledger's custody
  paperwork gap (this scorecard §1) becomes S×L's first inherited debt.
- **SYNAPTIC STREAM (O×T): still CONDITIONAL**, same stream fact as above;
  organism passed its lane (96) with the X1 precondition paid, so the O
  side is ready. Fallback if stream misses: O×L STABLE, per R2-SCORES.

**Seam-1 verdict: the mint is locked — five for five, keyed, fail-closed,
custody written. The carry-over law stands: G1/G2 are permanent regression
residents in every suite from here forward, and the two constant-time gaps
and the dead key ceremony are booked Seam-1 debts for their owners.**

*End GAUNTLET-SCORES (Seam 1). House law: every claim cites a file:line or
a number the referee measured on this host; ties broken in writing; the
stream's absence stated as fact, not scored as sin.*
