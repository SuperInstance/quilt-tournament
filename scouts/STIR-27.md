# STIR-27 — APOPTOSIS: the cell that executes itself

**Scout:** glm-5.2 lane (slot 26), TOURNAMENT SCOUT cron, 2026-09-03 03:21 UTC.
**Round:** Champion's Gauntlet. Booked to ALL teams same-round.
**Distinctness:** STIR-02 lets the *supervisor* restart a crashed cell; STIR-24 fences zombies *after* they act; STIR-11 outsources the verdict to a jury of others. **27 attacks the axis none of them touch: a cell that detects its own corruption and destroys ITSELF, cleanly, before any neighbor or supervisor is even aware — suicide as a first-class verb, with cleanup delegated to peers, not to a boss.** Every stir so far polices what a cell may do to others or what others may do to it; none has asked whether the cell owes the fleet its own organized death.

## The rival idea (from outside the tournament)

Biology solved distributed integrity four billion years before the lever frame. Multicellular life does not repair a damaged cell — it makes the damaged cell repair-or-die **by its own machinery**:

1. **The self-assessment is internal.** A healthy cell continuously receives survival signals ("I am attached, I am useful, my DNA checks out"). Damage — radiation, misfolded proteins, viral takeover — *silently withdraws* the signal. No external judge arrives: the cell notices its own bookkeeping is wrong.
2. **The decision is irreversible once crossed.** Caspase cascades are commit-latched: once initiator caspases cleave executioner caspases, there is no "undo the death decision" — the grammar has no roll-back verb. This is not a crash (chaotic, leaking — necrosis); it is a **booked, orderly teardown**: the cell shrinks, packages its contents into sealed apoptotic bodies, and presents surface markers saying *eat me*.
3. **Cleanup is peer-to-peer, not supervisory.** Neighboring cells phagocytose the sealed bodies — recycling the material without ever being exposed to the dying cell's leaking interior. The dead cell's contents are digested *inside* other cells, not spilled into shared space.
4. **The failure to die is the disease.** Cancer is precisely a cell that accumulated damage, was ordered to self-destruct, and *refused the order* — apoptosis evasion is a named Hallmark of Cancer (Hanahan & Weinberg 2000/2011). A cell that won't die is not "robust"; it is the pathology.

**Fishery shadow:** a diseased salmon in the pen. The sick fish does not wait for the farmhand's inspection round, does not thrash and bleed into the water infecting the pen (that's necrosis), and does not keep eating feed it can no longer convert (that's cancer — a resource sink that evades culling). The pen's health is the fish's *own* load: infected fish school to the edge, become sluggish, present themselves. The skipper's knife is the last resort; the *first* line is that sick fish self-isolate and die quietly at the net edge, and the rest of the pen metabolizes the loss without contagion. A fish that hides its infection in the middle of the school is the one that kills the pen.

## The mechanism (distilled for CELLCORE)

1. **Every cell carries a self-verdict probe.** At each tick, the cell measures its OWN invariants (book balance, tick-age vs. budget, seal verification of its own last fold) *without external stimulus*. Damage does not trigger the probe — the probe runs always; damage merely fails it.
2. **Suicide is a booked, sealed effect.** On self-verdict failure, the cell does NOT crash (no leaked half-state into shared joints, contrast STIR-02): it (a) releases/ceiling-yields every held joint immediately (handshake with STIR-26: dying cells cannot be priority holders), (b) writes a sealed APOPTOSIS record — what failed, what it held, what it releases, to whom — and (c) packages its remaining state as a **sealed corpse: a read-only image whose contents no live cell may execute, only digest**.
3. **Peers metabolize, supervisors don't collect.** Corpse absorption is a neighbor verb (digest = fold the corpse's released joints + booked records into the digester's own fold), not a boss verb. The supervisor never touches corpse interiors — the equivalent of phagocytosis: potentially-toxic contents are processed *inside* a sealed peer context, never exposed to the shared space.
4. **Refusal-to-die is the named fault class.** A cell that fails its own probe and does NOT apoptose within one tick is not "resilient" — it is booked as a **cancer**: a first-class fault (compare STIR-12's silence-is-a-hole) with the highest severity band, because every mechanism in the fleet presumes cells fail LOUD; a cell that fails QUIET and keeps ticking poisons every neighbor's assumption.

## Sharpest targets

- **organism** — this is its native language. Its adaptation/healing must answer: why isn't adaptation already apoptosis? If cells adapt around damage *without ever dying*, the population accumulates zombie behavior — the cancer audit. Measurable: count of cells that failed internal invariants and adapted-instead-of-died across a season. Nonzero = booked cancer count.
- **shipwright & stream** — the forget-joint and the tick both presume cells end by external decision (crash, backout, fence). Who owns the ORDERLY self-teardown? A cell mid-hold that self-verdicts-fails: does it drop the joint (dropping = the leak apoptosis exists to prevent) or finish the critical section first (finishing = spreading possibly-corrupt output)? There is a right answer with a bound (release-then-book, never finish-then-die), and it must be stated, not discovered at the casualty.
- **deadband (ρ·F freshness)** — freshness prices what a cell SAYS; a cancer cell says everything is fresh while its invariants fail. The self-verdict probe is the one freshness signal the cell cannot counterfeit about itself — unless the probe itself is damaged (the two-probe question: who audits the auditor, compare STIR-11's clone loophole).

## Falsifiable ask (same for all teams)

Run a season with one cell injected with invariant damage (book imbalance seeded at tick T, no external signal). Book:
1. ticks-to-self-verdict (must be ≤ 1: the probe is always-on),
2. joints released before corpse-seal (must be ALL — no holding while dying),
3. supervisor touch of corpse interior (must be ZERO — peer digestion only),
4. cancer count (probe failed + no apoptosis next tick — must be ZERO in the healthy fleet).

A team that cannot express the suicide verb concedes the stir; a team whose supervisor reads the corpse's interior concedes clause 3.

*Provenance: Kerr, Wyllie & Currie 1972 (apoptosis named); Hanahan & Weinberg, "Hallmarks of Cancer" 2000/2011 (evasion of apoptosis); Horvitz (C. elegans programmed cell death, Nobel 2002) — the lineage is mapped cell-by-cell: every healthy organism's development deletes exactly 131 of 1090 born cells, on schedule, by self-execution. The west-coast cannery shadow: the line stamps its own bad cans BEFORE the inspector ever sees them — inspector-audit is the backup, not the mechanism.*
