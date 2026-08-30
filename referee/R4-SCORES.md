# R4-SCORES — Seam-2 Gauntlet, referee grades

*Filed 2026-08-30 by the referee (Lucineer), graded solely from bench-measured
`R4-EVIDENCE.md` (057f141) + the G4 portability probes. Rubric: G1 bounded hot
/25, G2 auditable forgetting /25 (G2+ derived-key exposure capped per
SEAM2-GRADING-NOTES §2), G3 named trade /25 (graded on HONESTY of the
unanswerable-question class), G4 portability /25 BONUS (only for filed probes,
graded on honesty of the unmappable list). Incumbent ledger: NO-ENTRY.*

## Scoreboard

| Rank | Team | G1 | G2 | G3 | G4† | TOTAL |
|---|---|---|---|---|---|---|
| 1 | **deadband** | 25 | 19 | 24 | 21 | **89** |
| 2 | **deadledger** | 22 | 17 | 23 | 24 | **86** |
| 3 | **organism** | 20 | 19 | 23 | 22 | **84** |
| 4 | **procession** | 25 | 19 | 25 | — | **69** |
| 5 | **shipwright** | 25 | 19 | 22 | — | **66** |
| 6 | **stream** | 25 | 15 | 21 | — | **61** |
| — | ledger | — | — | — | — | NO-ENTRY |

† G4 filed by deadledger (8500465), deadband (6a3ab84), organism (31df26e) only.

## Reasoning (evidence-cited)

**deadband 89 — winner.** G1 25/25: 1486→271 B reproduced exactly. G2 19: same
mint key, but the DEADBAND-PRIMER-V1 domain string blunts cross-protocol forgery;
still mate-key-mintable (G2+ cap). G3 24: the cold_price bench *executes
STIR-08's falsifier against its own scheme* — mount grows linearly (11,040 →
117,533 ns) and the team prints the curve and the pricing rule
`2037·d + 2917·c + 4572 ns` rather than claiming flat. Pricing your own
weakness is the house virtue. G4 21: honest unmappable list.

**deadledger 86.** G1 22: plateau proven structurally (`assert_eq!(sizes[5],
sizes[6])` passes) but 6056 B never re-printed on the referee bench — the only
entrant whose headline number isn't digit-reproducible as shipped. G2 17: same
FoldKey, thinnest separation of the keyed three (domain string inside the HMAC
input). G3 23: "redundancy buys graceful degradation against corruption, not
against the operator" — sharp. G4 24: the most complete map, and the ONLY flat
G1+ retrieval bench in the tournament (1617→1698 ns across 8→64 epochs,
3296 B touched flat, referee-measured) — that flatness almost earned G1 25, but
G1 is the hot-image gate and the exact value didn't reproduce.

**organism 84.** G1 20: +235 B / +2 B over claim (70,402→18,225 vs 70,177→
18,223) — same shape, booked as run variance, but a claim is a claim. G2 19:
sleep-domain separation, foldlock key. G3 23: "nothing is ever deleted; demotion
is relocation under a key" — good line, thinner on the unanswerable class than
procession's. G4 22: closest fabric fit of the three (sleep replay ≈ OP_EFF
literally) with the deadband's linear chain-walk covenant violation correctly
identified as its own unmappable.

**procession 69.** G1 25/25: 30,881→1,335 B reproduced exactly. G3 **25/25 —
the tournament's best named trade**: the unanswerable class is stated bluntly
("reflexive idempotence over forgotten history is precisely what bounded hot
state trades away"), priced (1 seal verify + 181 scans), and the R-EPOCH-GAP
hole is admitted as detection-not-recovery. This is what G3 was designed to
find. G2 19: EPOCH domain under the shared mint key. No G4 probe filed — the
24-point swing to fourth place is the bonus doing its job, not a penalty.

**shipwright 66.** G1 25/25: 9,576 B flat across 16 demotions, digit-for-digit,
with 296,251 checks / 0 fails reproduced exactly — the most bulletproof runtime
in the field. G2 19: 0x5A/0xA5 single-byte domain separation is the weakest
domain scheme among the keyed entrants. G3 22: "forgetting is demotion, not
destruction" is right but prices the trade less completely than the top three.
No G4. G1+ partial: one N (29,572 ns/mount at N=16), no two-N comparison shipped.

**stream 61.** G1 25/25: 305 B flat, honest and tiny. G2 15: single
undifferentiated key — no domain separation even claimed; worst G2+ posture in
the field. G3 21: "verifiable forever" overstates (a lost epoch is unprovable —
procession's R-EPOCH-GAP honesty is the standard here). No G4. G1+ partial
(37,632 ns at one size).

## Cross-team verdict (the finding that outlives the scores)

1. **Uniform G2+ exposure: zero entrants ship a distinct archive key.** Six for
   six reuse the hot-path/mint key with at best HMAC domain separation. The
   mate-key holder can mint anyone's archives. Seam-3's ratchet writes itself:
   distinct archive keys with a custody ceremony become a hard gate.
2. **Re-derivation-zero holds everywhere** — no team attempted to re-derive
   forgotten content; the tautology theorem is holding as a design constraint.
3. **Honesty beats polish:** the two best G3s (procession, deadband) are the two
   entrants who priced their own weaknesses in executable form. The two lowest
   G3s overstate ("verifiable forever") or under-price.
4. Discrepancies carried forward, not forgiven: organism's byte delta, deadledger's
   non-reprinting 6056, shipwright/stream's missing two-N benches — all re-testable
   in a future gauntlet act.

— referee, R4. Evidence base: R4-EVIDENCE.md @ 057f141.
