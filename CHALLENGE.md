# THE TOURNAMENT — Casey, 2026-08-29 20:03

*"that was too quick. I need you to make teams compete with each other from different philosophical viewpoints and technical starting points and keep bringing in rival ideas until a champion is found truly."*

## The challenge (same for every team)

Build **CELLCORE v3**: a complete, runnable cell runtime to the GENERAL-CALCULUS shape
(read `/home/eileen/projects/quilt-verilog/docs/academic/GENERAL-CALCULUS.md` — it is the spec,
your philosophy decides what it *means*):

1. Cells with bounded state; links with balanced consent; effects as balanced transactions.
2. Fail-static totality: errors are states, never escapes. Local, non-deferrable ticks.
3. QUF-style bounded serialization with fold round-trip (decode(encode(x))==x, canonical).
4. Conformance scenario: the back-deck fish pipeline (tote=pink/humpy, center=chum,
   starboard half-totes=king/coho, 30 hooks @1.5 fathoms) — moves are effects, a fish in the
   hold without a booked debit is refused with a booked reason.
5. Adversarial duty: double-move, overflow, phantom entry, corrupt state, truncated fold —
   all refused or contained, never silent.

**Hard rules:** no float decides any verdict; state bounded; the core must run on this host
(runner choice is free — that IS the technical starting point); everything self-graded with
house honesty (machine-checked / pen-only / claim).

## The teams (philosophy + starting point)

| Team | Philosophy | Starting point |
|------|-----------|----------------|
| **LEDGER** | The book is the program. Batch, audit-first, conservation as the primitive; correctness is bookkeeping done honestly | Rust, batch F, fold-first |
| **STREAM** | Everything is a signal. Wavefront ticks, FIFO delivery, synchronous discipline; freshness is a timing property | Verilog-2005, hardware-first |
| **ORGANISM** | The runtime is alive. Hebbian adaptation, stigmergy, cells that heal; conservation emerges from metabolism | Python + the elephant/Hebbian corpus |
| **SHIPWRIGHT** | Joinery, not fasteners. Minimal verbs, minimal lines, pieces shaped to fit; if it needs glue it was cut wrong | Hand-crafted C, craft-first |

Each team delivers: working core, test suite, DEFENSE.md (why its philosophy wins — with
falsifiable superiority claims and the numbers to back them), and WEAKNESS.md (own failures,
first-class).

## The rounds

- **R1 BUILD** — teams build independently, no peeking (separate dirs).
- **R2 CROSS-ATTACK** — each team receives a rival team's work and writes the strongest
  attack (BREAK-\<team\>.md): break it with inputs, or break its claims with reasons.
- **R3 RIVAL IDEAS** — scout/ideator-injected rival ideas delivered to every team; each must
  incorporate or rebut-with-booked-reason. Revise.
- **R4 THE MEASURE** — shared harness (referee-run): correctness, adversarial survival,
  fold round-trips, bounded-state proof, LOC/complexity, doc honesty. Plus: student cold-reads
  each DEFENSE; devil reads every WEAKNESS for false modesty.
- **VERDICT** — champion by scored rubric, judged by a multi-model panel; scores, attacks,
  and dissents all published. A team that wins on numbers but loses the cold-read is not
  champion *truly* — the rubric says so before the first score is given.

Rubric weights (referee-fixed, Casey may overrule): correctness 40, adversarial survival 20,
bounded/fold integrity 15, defense holds under attack 15, honesty & clarity 10.

## EXPANSION (Casey, 20:13: "make it big and long") — the field grows to six

Two more entrants, from the corpus's own lineages:

| Team | Philosophy | Starting point |
|------|-----------|----------------|
| **PROCESSION** | The runtime teaches. PLATO/TUTOR lineage: judgment is born in the interaction; a cellcore that explains itself, drills its operators, and fails pedagogically is better than a silent oracle | TypeScript, tutorial-first: the docs ARE the interface |
| **DEADBAND** | Perception-first. The dissertation lineage: audit schedules, drift prefilters, the rho*F floor as a design constraint rather than a theorem about someone else | Python on the quilt-verilog verifies corpus: the runtime schedules its own auditing |

## The long game (rounds R1-R7, multi-day)

- R1 BUILD (six teams, blind) → R2 CROSS-ATTACK (round-robin: every team attacks every
  rival, not one) → R3 RIVAL IDEAS (ecosystem-injected, incorporate-or-rebut) → R4 REBUILD
  under fire → R5 THE MEASURE (shared harness, cold-reads, devil pass) → R6 THE MERGER:
  the leading team must absorb the single best rival piece WITH PROVENANCE — a champion
  that cannot name what it took and from whom is not champion → R7 CASEY'S CALL.
- Nightly digest at 21:00 carries the tournament state; rounds advance as lanes dock.
  This runs for days, not hours. Rival ideas keep arriving until the champion survives
  everything six philosophies can throw at it.

## THE LONG WAR (Casey, 20:48: "dozens of rounds, scouts stir the pot each round")

R1-R7 as written are only the OPENING BRACKET. The tournament proper is the
CHAMPION'S GAUNTLET that follows:

- After the verdict, the champion does NOT retire. Every subsequent round, the champion
  must survive a DEFENSE: the scout network delivers a fresh rival idea (from the corpus,
  the other repos, the wider web — something the champion has never faced), the referee
  distills it into a STIR, and the champion must incorporate it or beat it with booked
  reasons while ALL other teams (including late entrants) attack with it as their weapon.
- A defense survived = +1 to the streak. A defense failed = dethroning; the attacker(s)
  who broke it enter a short ladder to name a new champion. The tournament ends only when
  one champion has survived **12 consecutive defenses** — dozens of rounds, no early crown,
  and a champion that has metabolized at least a dozen foreign ideas by the end.
- Every round, win or lose, gets its scout STIR — the pot is stirred BEFORE defenses,
  not after. Scouts are forbidden from proposing anything already in a team's own docs.

### Standing scout order (every round)
Scouts (rotating: flash+web, glm-turbo, qwen3.6, Seed-mini) hunt ONE rival idea per round
from outside the tournament: another repo's mechanism, a paper, a fishery practice, a
historical system (PLATO logs, COBOL shops, west coast cannery ledgers). Written to
scouts/STIR-NN.md with provenance. The referee books it to every team same-round.
No team may reject a stir without a booked reason the scout can publicly rebut once.
