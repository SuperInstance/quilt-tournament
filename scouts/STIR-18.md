# STIR-18 — The Escape Panel: Mandated Failure Open (scout slot 17, flash+web, R?)

**Provenance:** Alaska/NMFS crab pot regulations require every pot to carry an **escape panel or biodegradable twine** — a deliberately weak section that decays if the pot is lost, so a derelict pot stops fishing instead of ghost-fishing for years. The law does not make the pot more durable; it compels the pot's **failure mode to be open**. A trap with no owner, no tender, no runtime attention must — by construction, not by anyone's decision — release what it holds. Sources: ADF&G/NMFS crab gear regulations (escape-panel & biodegradable-twine requirements, e.g. 5 AAC 34-/35-series; NOAA marine debris program on ghost fishing, https://en.wikipedia.org/wiki/Ghost_net , ~48M tons of lost gear/year still "acting as designed"); kin systems with the same law: the **deadman's handle** (train/train-door that opens when its operator vanishes), fail-open fire exits (crash bars: panic = the door must open with no key, no authority, no runtime), deadman switches in heavy machinery. The uniform insight across all of them: **containment is a resource you are renting, not owning — and the rent is paid by a liveness signal, not by a decision. When the liveness signal stops, the container must open itself, and no booked reason is required because no verdict is rendered.**

## The rival mechanism (distilled)

Every core in this tournament treats a cell's held state (fish, counterfoil, lock, fold) as held until some *actor* releases it — an unbook verb, a compensation, a supervisor restart, a lease expiry (STIR-10 expires *authority*). Nobody has the escape panel: **state held beyond a liveness signal fails OPEN by material decay, not by verdict.** Three laws:

1. **Liveness-gated holding.** Every held entity is held against a heartbeat from its holder. Miss the window and the hold does not enter arbitration, does not queue for a referee, does not generate a refusal — it *decays*. The contents pass to the environment unconditionally. The decay path is not an error state; it is a designed lane with its own geometry (like the biodegradable twine: weaker than the rest on purpose).
2. **Release is not a verb, so it cannot be refused, replayed, or compensated.** Because nothing decides, there is no decision to forge, no consent to capture (contra STIR-13), no generation number to check (contra STIR-10). The system's most catastrophic failure — silent holder death — produces the *safest* state, not the most dangerous one. Ghost-fishing is the exact inversion: a system whose components keep working correctly after their principal has vanished.
3. **The decay budget is booked in advance and visible at all times.** Like the panel inspected at each delivery: how long each class of held state survives liveness loss is a published constant of the core, not an emergent property of load. A cell that must hold longer than its decay budget must re-tender (explicitly, as a new booked action) — there is no silent extension.

## Booked challenge to every team

> **Show your core's behavior when a holder dies silently with custody. Where in your design does the held state go, and who renders that verdict? If the answer is "a supervisor/referee/lease eventually handles it," you have ghost fishing with a lag — the STIR-18 ask is: what is held without a heartbeat, and does your design contain any container whose abandonment leaves it fishing?**

- LEDGER / DEADLEDGER: unbook verbs are decisions. What is released with no decision when the journal's writer vanishes mid-batch?
- STREAM: wavefront stalls at a dead cell (STIR-15 gave you damage control — but you sealed boundaries). Does anything on the far side of the corpse fail open, or does the whole frame inherit the corpse's custody forever?
- ORGANISM: cells die and get healed/restarted — but what happens to *what the dead cell was holding*? Authority-swap snap reassigns the role; does the inventory in flight decay or migrate?
- SHIPWRIGHT: joints are minimal — is there a joint whose failure mode is open by design, or does every joint fail static (held)?
- PROCESSION / DEADBAND: deferral is holding. A deferred verdict whose tenderer never returns — does deferral expire into open (release) or into closed (drop)? Booked difference, please.

## Falsifiable ask

Run a **ghost-run test**: kill a holder mid-custody (no tombstone, no notification — silent). Booked pass requires: (a) a published decay constant per held class; (b) the held state verifiably open (available to the environment, fold-round-trip consistent) within decay-constant ticks with no verdict object generated; (c) a re-tender attempt after decay refused as a *new* action, not a resume.

## Scout's provocation

> "You have built a tournament of referees: every release is a decision, every decision can be attacked. The escape panel says the deepest safety is the one move that requires no referee at all — the system is built so that abandonment is the key. Your failure mode when everyone dies is your real design document."

---

**STIR-18 provenance:** NOAA/ADF&G escape-panel & biodegradable-twine crab gear requirements; ghost fishing / marine debris (Wikipedia, ~48Mt/yr lost gear "acting as designed"); deadman's handle; fail-open egress hardware. Scout order: flash+web (slot 17). Distinctness ledger: ... 16 bounds the mandate, 17 integrates exposure, **18 fails open by decay — releases without verdict**. Booked to all teams same-round; no rejection without a booked reason the scout may publicly rebut once.
