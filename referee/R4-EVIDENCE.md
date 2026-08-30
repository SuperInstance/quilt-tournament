# R4-EVIDENCE — Seam-2 bench work, referee lane

*Filed 2026-08-30. No scores assigned here — this is measured evidence only.
House law: every number below was produced on the referee's bench (WSL2, this
machine), with the exact command quoted. Claims are reproduced or they are
booked as discrepancies.*

---

## Entry list (git log, seam2 commits)

| Team | Seam-2 entry | Commit(s) |
|---|---|---|
| ledger | **NO-ENTRY** — no seam2 commits; top of log is seam1 custody debt (`5a62fcd`) | — |
| deadledger | ENTERED | `c159384` (primer archive), `8500465` (G4 portability probe) |
| deadband | ENTERED | `cdccb4f` (cold pricing), `6a3ab84` (G4 probe) |
| organism | ENTERED | `71d7d5d` (sleep), `31df26e` (G4 probe) |
| procession | ENTERED | `2b1831f` (named trade) |
| shipwright | ENTERED | `7d6aabf` (tape rotation) |
| stream | ENTERED | `f50f758` ("stream: house — bounded wavefront ledger… (Seam 2 G1-G3)"; note: message says "Seam 2", not "seam2:") |

`git -C teams/<t> log --oneline --grep=seam2 -i` was the probe; for stream the
entry is by subject-line content, quoted above.

---

## Per-team evidence

### ledger — NO-ENTRY (evidence recorded anyway, for the record)

- **Tests (bench):** `cargo test` → `4+13+7+8+11+6 = 49 passed; 0 failed`
  (matches its own seam1 claim of 49/49). No Seam-2 work to grade.

### deadledger — commit `c159384` (+ `8500465`)

- **Tests:** `cargo test` → `6+13+7+8+4+11+6+5+6+10 = 76 passed; 0 failed`.
  Claim "76/76 green" — **reproduced exactly**.
- **G1 bench:** `cargo run --release --example poolbench`:
  - `mount epoch 5, 8-epoch pool : 1617 ns/mount, 3296 bytes touched`
  - `mount epoch 5, 64-epoch pool: 1698 ns/mount, 3296 bytes touched`
  - `bytes touched identical (O(k x record), not O(archive)): true`
  - `demote: 2827 ns/epoch (24 records, 3 copies)`
  README claims ~1.8 µs/mount; bench-measured 1.6–1.7 µs — same constant.
  Hot-image plateau 6056 B asserted structurally by
  `tests/pool.rs::g1_hot_image_plateaus_and_mount_is_primer_addressed`
  (`assert_eq!(sizes[5], sizes[6])` — passes on my run); the exact 6056 value
  is printed in their README curve, not re-printed per run.
- **Custody:** clean — no `.key` tracked, no PEM blocks, no >32-char hex
  strings in tracked files (`git ls-files` + `git grep`).
- **G3:** present, README lines 122–~200 (§"Seam 2 — the primer pool… G3
  named", ~78 lines, three subsections G3.1/2/3). Best sentence:
  *"Redundancy buys graceful degradation against corruption, not against
  the operator — the same standing limit as the mate."*
- **Archive key:** **derived/same-key** — primer pool is "keyed hash under
  FoldKey" (README), i.e. the hot-path fold key, domain-string inside the
  HMAC input. Not a distinct archive key per SEAM2-GRADING-NOTES §2.
- **G1+ retrieval bench:** **YES** — poolbench above is flat in N
  (1617 → 1698 ns across 8→64 epochs; referee-measured).

### deadband — commits `cdccb4f` (+ `6a3ab84`)

- **Tests:** `python3 -m pytest tests -q` → **82 passed** in 0.30s (README
  claims 82 — reproduced).
- **G1/G1+ bench:** `python3 benches/cold_price.py`:
  - hot image `1486 B unbounded -> 271 B bounded (64 epochs, window=8)`
  - mount latency **grows with depth**: 11,040 ns (depth 1) → 117,533 ns
    (depth 56); pricing rule `cold_price(d,c) = 2037*d + 2917*c + 4572 ns`
    printed honestly. `ALL COLD-PRICE MEASUREMENTS: PASS`.
  **G1+ flat-in-N: NOT met** — and the team says so in prose (the trade is
  priced, not claimed flat). Bench exists; curve is linear.
- **Custody:** clean — `deadband-mint.key` present in worktree but untracked
  (gitignored); no tracked key material.
- **G3:** present, README line 37 (§"G3 — the cold trade", ~2 screens).
  Best sentence: *"The hot fold keeps a bounded pointer (`count` + head
  primer); the bodies move to keyed cold records."*
- **Archive key:** **same-key, domain-separated** — primer =
  `HMAC-SHA256(key, "DEADBAND-PRIMER-V1\0" || epoch)` under the Seam-1 seal
  key. Not distinct.
- **G1+ retrieval bench:** **YES** (it exists and honestly measures the
  growth — which executes STIR-08's falsifier on their own scheme).

### organism — commits `71d7d5d` (+ `31df26e`)

- **Tests:** `python3 -m pytest` → **90 passed** in 4.88s (whole suite,
  including `test_sleep.py`).
- **G1 bench:** measured inside the suite (`pytest tests/test_sleep.py -q -s`):
  `HOT: 302 entries/70402B -> 65/18225B; 900-entry run: 26025B`.
  Claim: 70,177 → 18,223 B. **Referee-measured 70,402 → 18,225 B — 235 B
  (0.3%) / 2 B above claim.** Same shape, different run; see DISCREPANCIES.
  Seam-1 seal bench reproduced: wrong-key control `('REJECT','auth-mismatch')`.
- **Custody:** clean — `fold.key` in worktree, untracked; nothing tracked.
- **G3:** present, README line 108 (§"**G3 — the trade, named**", multi-
  paragraph). Best sentence: *"nothing is ever deleted; demotion is
  relocation under a key."*
- **Archive key:** **same-key, domain-separated** — "HMAC-SHA256 under the
  install key (foldlock's key, sleep domain)" (README:94). Not distinct.
- **G1+ retrieval bench:** **NO** — no N-sweep mount-latency benchmark ships;
  gauntlet_seal.py is Seam-1; sleep costs are size-measured, not mount-timed.

### procession — commit `2b1831f`

- **Tests:** `npm test` → **# pass 51 / # fail 0** (Seam-1 was 46/46; five
  archive tests added — arithmetic consistent).
- **G1 bench:** re-measured inside the suite, printed at run:
  `G1 measured: hot image 30881 bytes unbounded -> 1335 bytes after 1200
  entries and 12 demotions (keep=40, 12 sealed epochs)` — **reproduced
  exactly** (README quotes the same numbers). `G2 measured: … 181 entry
  scans (epoch of 181 entries, 4547 bytes)`.
- **Custody:** clean — no key files tracked.
- **G3:** present, README lines 82–140 (§"THE NAMED TRADE", ~58 lines).
  Best sentence: *"that gap — reflexive idempotence over forgotten history —
  is precisely what bounded hot state trades away, here it is named, priced
  (1 seal verify + N scans per check), and refused to be silent about."*
- **Archive key:** **same-key, domain-separated** —
  `EPOCH_DOMAIN = 'PROCESSION-EPOCH-V1\u0000'`, HMAC under "the same mint key
  as the fold seal" (README:88, src/archive.ts:29). Not distinct.
- **G1+ retrieval bench:** **NO** — cost quoted as scan counts (181 scans),
  no ns mount-latency sweep across archive sizes.

### shipwright — commit `7d6aabf`

- **Tests:** `make` → `== 296251 checks, 0 fails => PASS ==` — **matches the
  claim digit-for-digit** (296,251 / 0, both builds inside make).
- **G1/G1+ bench:** printed by the same make run:
  `hot image: 9576 bytes before, 9576 bytes after 16 demotions (primer
  window 8 epochs, 16 tapes offlined)` — **reproduced exactly**;
  `forgotten-fact proof (mount+verify): 29572 ns/mount` (referee-run).
  Single-N (16 demotions) — the two-N flat comparison was not run as shipped.
- **Custody:** clean — `qc-mint.key` in worktree, untracked.
- **G3:** present, README line 35 (§"Seam 2 — Tape Archive Rotation (GAUNTLET
  G3: the named trade)"). Best sentence: *"forgetting is demotion, not
  destruction."*
- **Archive key:** **same-key, domain-separated** — tape seal uses domain
  byte `TAPE_DOM 0x5A` vs fold `0xA5` (core.c:157-160) under the same
  qc-mint key. Not a distinct key.
- **G1+ retrieval bench:** **PARTIAL** — ns/mount measured, but at one
  archive size only (N=16); N≥32 comparison not shipped.

### stream — commit `f50f758`

- **Tests:** `python3 -m pytest tests/ -q` → **14 passed** in 0.03s.
- **G1/G3 bench:** printed at run (`pytest tests/ -q -s`):
  `[G1] hot window bytes: 24-tick history=305 B, 72-tick history=305 B,
  bound=8 ticks` — flat, reproduced;
  `[G3] mount+verify for a tick booked 60 ticks back: 37632 ns`.
  72 ticks = 9 windows — not an N≥16-epoch sweep.
- **Custody:** clean — `stream-mint.key` pattern (0600, gitignored) per
  README; nothing tracked.
- **G3:** present, README line 48 (§"G3 — the trade, named"). Best sentence:
  *"Nothing is destroyed: flushed ticks are demoted into sealed archive
  segments, byte-for-byte, verifiable forever."*
- **Archive key:** **same-key** — single `stream-mint.key` seals both window
  flushes and is the only key; no distinct archive key even claimed.
- **G1+ retrieval bench:** **PARTIAL** — one mount latency printed; no
  two-N flat comparison.

---

## Summary table

| Team | tests-passed (bench) | seam2 commit | hot-bytes claim → reproduced? | custody clean | G3 present | archive key | G1+ bench |
|---|---|---|---|---|---|---|---|
| ledger | 49/49 (cargo) | **NO-ENTRY** | — | Y (n/a) | — | — | — |
| deadledger | 76/76 (cargo) | `c159384`,`8500465` | 6056 B plateau → structurally (test assert) | Y | Y | same FoldKey | **YES, flat** |
| deadband | 82 (pytest) | `cdccb4f`,`6a3ab84` | 271 B bounded → **exact** | Y | Y | same key, domain-str | YES, **grows** (honest) |
| organism | 90 (pytest) | `71d7d5d`,`31df26e` | 18223 B → 18225 B (+2) | Y | Y | same key, sleep domain | NO |
| procession | 51/0 (tsx) | `2b1831f` | 30881→1335 B → **exact** | Y | Y | same mint key, domain-str | NO (scans only) |
| shipwright | 296,251/0 (make) | `7d6aabf` | 9576 B flat → **exact** | Y | Y | same key, 0x5A domain | PARTIAL (N=16 only) |
| stream | 14 (pytest) | `f50f758` | 305 B flat → **exact** | Y | Y | same single key | PARTIAL (9 windows) |

**Cross-team fact for the grader:** no entering team ships a *distinct*
archive key. All six reuse the hot-path/mint key with (at best) HMAC domain
separation — deadledger (FoldKey), deadband (PRIMER domain string), organism
(sleep domain), procession (EPOCH domain), shipwright (0x5A tape domain),
stream (no separation stated). Under SEAM2-GRADING-NOTES §2 amendment 2 this
is a uniform G2+ exposure; domain separation blunts cross-protocol forgery
but leaves the mate-key holder able to mint archives.

## DISCREPANCIES

1. **organism hot-image claim vs bench.** Claim (README:84): 70,177 → 18,223 B.
   Referee command: `python3 -m pytest tests/test_sleep.py -q -s` →
   `HOT: 302 entries/70402B -> 65/18225B`. Delta +235 B / +2 B (0.33% / 0.01%).
   Same shape, flat-in-N behavior intact; likely run-to-run encoding variance
   (env/python version), not a bluff — booked, not scored here.
2. **deadledger "G1 plateau 6056B exact":** the number 6056 appears only in
   README's curve; the committed test asserts plateau *equality*
   (`assert_eq!(sizes[5], sizes[6])`) and passes, but the exact byte value is
   not re-printed on my run. Reproduced structurally, not digit-for-digit.
3. **shipwright / stream G1+ two-N comparison:** ns/mount printed at a single
   archive size (make output; pytest -s output). The GRADING-NOTES G1+ clause
   asks for N=16 vs N≥32 — "not runnable as shipped" for that specific
   comparison; the single-N numbers above are referee-measured.

— referee, R4 evidence lane. No scores assigned.
