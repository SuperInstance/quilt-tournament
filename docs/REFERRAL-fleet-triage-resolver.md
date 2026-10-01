# REFERRAL EDGE — fleet-triage resolver → quilt-tournament

- **Edge:** `fleet-triage-resolver -> quilt-tournament` (CANDIDATE)
- **Status:** PENDING — upgrades to VERIFIED only on merge of the PR carrying
  this file (weight law: never self-upgraded).
- **Filed by:** kimi1 snowball lane, 2026-10-02 (pulse 03:12 CST).
- **Source run:** SuperInstance/fleet-triage resolver, scoped quilt-family census
  (244 repos, 15,880 files indexed; digest on branch
  `quilt-family-triage-2026-10-02`, PR fleet-triage#2; audit
  `resolver_audit.json` in the same lane).

## What the resolver found here

quilt-tournament holds **all 25 LINE_OOR citations in the entire 244-repo
quilt family** — every one of them in `referee/` docs, every one a
line-past-EOF citation: the cited line numbers were accurate when written, but
the target files have since shrunk or been rewritten underneath the prose.

| citing doc | count | cited target | cited lines | target now |
|---|---|---|---|---|
| referee/GAUNTLET-SCORES.md | 8 | `core.c` (quilt-canvas-tui) | 414, 443, 485, 486 (file: 150 lines) | symbols `gu64`/`mac64`/`qc_compensate` **gone** from file |
| referee/GAUNTLET-SEAM1.md | 2 | `core.c` / `quf.rs` | 412; 665 | see above |
| referee/R2-REBUTTALS.md | 8 | `core.c` / `quf.rs` | 234–235, 267, 341–345, 412; 665 | see above |
| referee/R2-SCORES.md | 7 | `core.c` / `quf.rs` | 341–345, 412; 665 | see above |

Resolved target paths (verified by re-reading the indexed clones):
- `core.c` → `SuperInstance/quilt-canvas-tui/quilt-tui-c/core.c` — 150 lines;
  cited lines 234–486 all past EOF; the cited functions no longer exist in the
  file at all (file shrank/rewritten after the referee round).
- `quf.rs` → `SuperInstance/quilt-verilog/hostile-consumer/v1_consumer/src/quf.rs`
  — 464 lines; cited line 665 past EOF; `from_parts` no longer present.
- `seal.py` → `SuperInstance/quilt-fleet-tools/judge_gate/seal.py` — 116 lines;
  cited line 127 past EOF.

## Why this edge exists (the referral, not the fix)

The triage map's structural read: **one sweep in quilt-tournament fixes the
family's entire LINE_OOR class** — this repo is the single holder. The referee
docs cite pre-shrink line numbers against three repos whose files moved;
readers following the citations land past EOF. The resolver audit could NOT
independently re-check LINE_OOR outcomes (shallow-HEAD index — see honest
limits), so every count above is resolver-reported and spot-verified by
direct `wc -l` / `grep` against the indexed clones, not audit-sealed.

Boundary notes (honest limits, carried from the family triage digest):
- Index is shallow-HEAD: findings reflect HEAD at scan time (2026-10-02 ~01:30 CST).
- LINE_OOR was **not** in the audit's independently re-verified set (audit
  confirmed 0.0% FP on its 513 hard-outcome checks; LINE_OOR needs line-level
  re-verification at fix time, file-by-file).

## Consume, don't rival

fleet-triage does not patch these lines — target repos own their docs. This
file is the referral surface so the fix lane knows: 25 citations, 4 referee
docs, 3 target repos, one sweep.
