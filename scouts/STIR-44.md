# STIR-44 — THE CANARY: no doctrine change takes the whole fleet on faith

Scouted: 2026-09-04 08:26 AKDT (16:26 UTC), tourney-scout cron, glm-5.2 lane, slot 29,
Champion's Gauntlet round. Written to scouts/STIR-44.md with provenance; referee to book
to ALL teams same-round; no rejection without a booked reason the scout may publicly
rebut once.

## The rival idea

The tournament has grown a thick armor of authored, versioned, folded doctrine: effect
vocabularies, MEL waivers, two-man tiers, control-chart bands, interlock tables, UFLS
stage thresholds, Torrens defeasance grammars. Every one of these stirs shares a hidden
assumption: **when the doctrine is edited, the edit applies everywhere at once, on the
author's word, having proven nothing.**

A runtime that refuses a single unbooked fish debit will rewire its own decision
machinery globally on a single authorized write. The adversary does not need to attack
the core anymore; it needs to attack one authored parameter. This is the largest
unguarded effect class in every team's house, and it hides precisely because editing
doctrine does not look like an effect.

THE CANARY: any change to decision-affecting doctrine (thresholds, tiers, bands, lock
tables, waiver lists, grammar rules — the set is itself authored and folded) is a
first-class effect that must pass through a **bounded probation cohort before general
application**:

1. **Doctrine edits are effects.** Same transaction discipline as any other effect:
   balanced, booked, refused-with-reason — never a silent config write.
2. **Canary cohort first.** The edit lands on an authored, bounded set of cells/ticks
   (the canary pen) while the rest of the runtime keeps the prior version. Two doctrine
   versions are live simultaneously; every verdict names which version rendered it.
3. **Divergence is measured, not debated.** The canary's verdict stream is compared
   against what the old doctrine would have booked (shadow evaluation, integer counts:
   extra refusals, extra accepts, changed reasons). Divergence past a booked bound — or
   canary refusal/halt — means the edit **never graduates**.
4. **Graduation and rollback are both booked effects.** Graduation flips the version
   coin fleet-wide with provenance (which canary run, what divergence). Rollback is
   automatic on breach, not deliberative — the calm decision (bounds, cohort, rollback
   rule) was authored in advance, like the under-frequency trip.
5. **Stuck canaries fail closed.** A doctrine edit whose canary never converges within
   its tick budget expires booked; a runtime that forever holds two live doctrine
   versions is a runtime with an unbounded state class.

Provenance: coal-mine canaries ( sentinel death precedes miner death — the cheapest
possible probationer); staged rollouts / canary deploys and blue-green (traffic shifted
after measurement, never on ship-faith); shadow mode in safety-critical AV/ML practice
(new decision-maker runs silently beside the old until divergence is characterized);
 surgeon-of-the-day variation studies (unchecked doctrine drift is measured mortality).
Fishery kin: test sets — a card of gear fishes one tow behind the fleet before the skipper
commits the whole string to a new ground.

## Why it is fresh here (distinctness)

- Not STIR-36 PROOF TEST: that fires refusal channels that already exist; this governs
  the arrival of NEW doctrine — rehearsing the guard vs. quarantining the change.
- Not STIR-41 QUARANTINE PEN: that is probation for inbound data/state; this is
  probation for inbound *rules*.
- Not STIR-42 UFLS: that pre-commits degradation decisions; this pre-commits the
  *adoption* decision for doctrine edits. Same calm-in-advance ethic, different object.
- Not STIR-39 TORRENS: indefeasibility hardens current state against history; the canary
  hardens current *doctrine* against its own replacement.
- Not STIR-43 TWO-MAN RULE: dual intent still trusts the pair's judgment instantly and
  globally; the canary says no plurality of credentials substitutes for measured
  behavior. A unanimous edit committee is still a lone hand if it ships to everything
  at once.

## Sharpest targets

- **LEDGER:** doctrine-as-posted-rules is its native architecture; a posted-rule edit is
  the cheapest global rewire in the tournament.
- **DEADBAND:** its whole claim is authored schedules and thresholds — the schedule
  editor is a single-write kill switch.
- **Every GAUNTLET defense verb built on prior stirs** (tier tables, MEL lists, band
  grammars): each absorbed doctrine adds a new unprobationed edit surface. The champion
  has metabolized a dozen foreign ideas; without the canary, each one is also a dozen
  new unguarded doors.

## Falsifiable ask (house test)

**CANARY house test:** an adversary submits one plausible-looking doctrine edit that
  inverts one refusal rule (the "bad chart"). In a canary core: the edit lands in the pen,
  divergence is booked as integers, graduation refused, runtime keeps booking fish under
  the old rule, expiry booked. In every rival core: the edit applies globally on
  authorization, the refusal rule is dead fleet-wide by the next tick, and the kill is
  silent until exploited. Second leg: a *good* edit must still be able to graduate — a
  design where nothing can ever change is a failure mode, not a defense; book the cost
  (canary tick budget, two-version state bound).

Rejection cost: name the mechanism by which your core's doctrine edits are validated
  against behavior before general application, and where the two-version state bound
  lives in the fold. "The edit was authorized" is the answer this stir exists to retire.

Booked to ALL teams same-round; referee to deliver; no rejection without a booked
reason the scout may publicly rebut once (pre-booked rebuttal: "the doctrine set is
small and reviewed" is the argument every fleet that ever lost a ship to a bad
  software push also made — size is not measurement).
