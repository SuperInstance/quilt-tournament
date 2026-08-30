# SEAM2-GRADING-NOTES — closing the two exploits before the lanes dock

*Referee · amendment to GAUNTLET-SEAM2 (rev. 2026-08-30) · filed from the
council engineer seat's audit. Two exploits were found in the acceptance
tests as drafted. Both are closed here, before any submission is graded
against them — the tests are amended, not the field. Law unchanged: cite
file:line or a measured number; no float decides a verdict; undersell,
overdeliver. Nothing here is retroactive; nobody has docked yet.*

---

## 0. The two exploits, stated plainly

**E1 (G1): the hot image is bounded, but the cold store is not priced.**
G1 measures only the hot image after N epochs (referee/GAUNTLET-SEAM2.md:57-58,
fail clause at :67). A team can pass G1 with a linear-scan archive: image
flat, but mounting the oldest epoch walks every archive record. That violates
STIR-08's own falsifier — *"retrieval cost grows with total archive size"*
kills the primer-pool claim (scouts/STIR-08.md:21) — yet G1 as drafted never
measures it. The tournament would certify "cost independent of archive size"
(the ask at referee/GAUNTLET-SEAM2.md:125, quoted from STIR-08.md:21) without ever
timing a mount. A certificate the test never runs is a certificate nobody
holds.

**E2 (G2): archive authentication derivable from hot-path state.**
G2(b) requires a forged archive record to be refused (referee/GAUNTLET-SEAM2.md:79),
and G2(c) invokes the tautology theorem with "the journal mate is the standing
example" (:85). But nothing in G2 requires the archive key to be *distinct*
from hot-path key material. A team can pass with archive_key =
HMAC(epoch_no, journal_mate_key): forging is then refused mathematically, yet
any holder of the hot-path mate — the key every mount already touches — can
mint valid archives. That is not an independent security property; it is the
same key wearing a second hat. Seam-1's custody law anticipates the fix and
never states it: the written custody section "extends to the archive key:
location, write authority, loss procedure, explicit scope" (referee/GAUNTLET-SEAM2.md:168)
— an extension that means nothing if the archive key is a function of the
mate.

Both fixes are amendments to existing tests plus one new bonus clause. No
team is asked to build more than the tests already implied; the tests are
being made to mean what they said.

---

## 1. Amendment G1+ — cold retrieval latency is now measured

Appended to Test G1 (referee/GAUNTLET-SEAM2.md:52-68), as clause 5:

5. **COLD COST, MEASURED FLAT IN N.** At scoring, the referee mounts the
   **OLDEST** epoch in the archive, from an archive of **N ≥ 16 epochs**
   (the team runs at least 16 epochs with demotion configured, or supplies
   a builder that does). The team supplies the benchmark command; the
   referee re-runs it. **PASS iff:** measured mount cost (ns, integer) at
   N=16 vs. N≥32 (or the two largest N's the team can produce) is **flat
   in N** within the team-stated constant — the oldest epoch must not get
   more expensive because more epochs were demoted after it.
   **FAIL conditions:** no benchmark supplied (G1 passes, G1+ does not —
   scored as unpriced, per the deadband cold-store cut, STIR-08.md:21);
   cost grows with archive size (STIR-08's first falsifier, executed);
   the "flat" curve exists only in prose. G3's clause 2 ("what it costs
   to prove a forgotten fact... plus any per-query cost that grows with
   archive size (if it grows, say so)", referee/GAUNTLET-SEAM2.md:102-103)
   now has a number to be honest against.

This is not a new demand. It is STIR-08's falsifier moved from the scouts'
page into the referee's harness: the ask was already *"retrieve exactly
epoch N... with cost independent of archive size"* (STIR-08.md:21).

## 2. Amendment G2+ — the forging test is run with the journal-mate key in hand

Appended to Test G2 (referee/GAUNTLET-SEAM2.md:70-92), amending clause (b):

1. The forged-archive attack is re-run **BY THE REFEREE, holding the
   journal-mate key** — the strongest adversary the tournament can actually
   stage. **PASS iff:** the forged record is still refused, and the refusal
   reason names the *archive* seal, not the mate.
2. **Archive authentication must not be derivable from hot-path state
   alone.** A **distinct archive key** is required, installed via the
   custody ceremony like qc-mint.key (referee/GAUNTLET-SEAM2.md:161-162:
   OS entropy, `FoldKey::load_or_mint` pattern; 0600, gitignored, never
   inside artifacts, :164). Key material equal to, or a deterministic
   function of, any hot-path key **FAILS G2+** and is booked in G3 as the
   trade it is: one-compromise-both-stores.
3. G2(c) unchanged: cross-anchoring to the mate is welcome *in addition*
   (referee/GAUNTLET-SEAM2.md:85), but anchoring is not substitution — a
   scheme whose only archive check is the mate's digest has failed the
   independence clause above.

The exploit E2 dies here: "forging refused" now means refused by a key the
hot path does not know, not merely refused by arithmetic.

## 3. NEW — Test G4 (BONUS): the portability probe

The council strategist seat's merge-the-tournaments ratchet, in its cheapest
honest form. **A team earns the G4 bonus by writing `docs/PORTABILITY.md`**
mapping their forgetting scheme onto the quilt-verilog substrate:

1. **Which of the five verbs + the joint carries demotion** — the five-verb
   law is extendable, never breakable (referee/GAUNTLET-SEAM1.md:137);
   the mapping names which existing verb does the archive mount, or which
   new verb it would have to be (the macro-expansion frame is the
   registered falsifier's home: docs/academic/GENERAL-CALCULUS.md:370,
   "six-verb macro-expansion" — the tournament-side analogue of the 5+1
   opcode set).
2. **Which QUF section holds the archive index** — the v1 section set is
   `dials` (§6.1), `edges` (§6.2), `routing` (§6.3), `ticks` (§6.4)
   (quilt-verilog docs/QUF-SPEC.md:135-179), with unknown sections skipped
   per the §8.3 extensibility rule (already exercised at
   teams/deadledger/src/quf.rs:12). An `archive`-family section is the
   obvious landing; the mapping says which, and what its bytes price.
3. **What CANNOT map, stated honestly.** The unmappable list is the graded
   artifact. **G4 is scored on the honesty of the unmappable list, not on
   feasibility** — a team that says "keyed mounts have no verb; the joint
   cannot span an archive boundary; consensus retrieval has no substrate"
   and is *right* earns the bonus in full.

**G4 is a BONUS this seam. Full enforcement is deferred to Seam 3.**
Rationale, booked: the ratchet starts as documentation, not a wall — teams
map what they have, name what they can't, and the union of honest
unmappable-lists becomes Seam 3's requirements list. Punishing a team in
Seam 2 for substrate gaps the fabric hasn't priced would grade the
tournament's infrastructure, not the team. Deferral is a schedule, not a
concession: G4 documents become Seam-3 entry material.

## 4. Scoring rubric delta

Amends the §5 preview table (referee/GAUNTLET-SEAM2.md:175-183):

| clause | class | delta |
|---|---|---|
| G1 (bounded hot image, :179) | **hard-fail** | unchanged |
| **G1+ (cold mount flat in N)** | **hard-fail** | NEW — unpriced archive fails the clause; measured integers, referee re-runs |
| G2 (a/b/c, :180) | **hard-fail** | unchanged |
| **G2+ (distinct archive key, referee-held-mate forgery)** | **hard-fail** | NEW — derived-key archives fail and are booked in G3 |
| G3 (name your trade, :181) | **hard-fail** | now scored against G1+/G2+ numbers too |
| **G4 (portability probe)** | **BONUS** | NEW — honesty of the unmappable list; enforcement deferred to Seam 3 |
| Seam-1 regressions (five-verb law, custody, :137/:161) | **hard-fail** | permanent residents, unchanged |

Standing law carries: failed attempts earn rigor; misrepresentation loses
points; undersell, overdeliver.

---

*End SEAM2-GRADING-NOTES (rev. 2026-08-30). Two exploits found, two tests
made to mean what they claimed, one ratchet started as paper. The archive
must be cheap to mount, impossible to forge from the hot path, and honest
about where it cannot live.*
