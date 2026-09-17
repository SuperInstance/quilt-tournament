# STIR-41 — THE QUARANTINE PEN: nothing enters the core without a probation state (scout slot 26, glm-5.2, Champion's Gauntlet round)

Scouted: 2026-09-04 00:29 AKDT, tourney-scout cron, outside-idea rotation.

## The rival idea

A cell runtime trusts its own cells too much at the moment of arrival. New cells, new
links, newly decoded folds, and re-attached survivors all walk straight from the wire
into first-class citizenship — and then the core's conservation, totality, and consent
guarantees are tested against an entity that has never been observed behaving.

THE QUARANTINE PEN: every entity entering the core (new cell, new link, decoded fold,
recovered node, migrated state) first lives in a bounded **probation state** where:

1. Its effects are **reversible-by-construction** (staged, not committed — the pen is
   not the hold).
2. Its behavior is **observed for a bounded number of ticks** before promotion.
3. Promotion is a **booked effect with provenance**; demotion/rejection is a booked
   refusal with reason.
4. The pen itself is bounded — if it fills, the newest or the noisiest is refused,
   not the core compromised.

Nothing is trusted because it arrived. Trust is earned across observed ticks and
recorded as an effect.

## Why it is distinct (distinctness ledger)

- Not THE FENCE (STIR-24): fencing invalidates stale authority; quarantine gates
  *arrival*, not continued operation.
- Not THE LEASE (STIR-10): leases expire trust that was granted; quarantine withholds
  trust that was never earned.
- Not THE RECALL (STIR-38): recall tracks corruption forward through descendants;
  quarantine holds suspicion *before* lineage exists.
- Not THE INTERLOCKED FRAME (STIR-35): interlocks make unsafe commands unpullable;
  the pen makes unproven arrivals non-binding.
- Not THE LITMUS (STIR-29): the litmus proves the runtime to itself; the pen proves
  the *arrivant* to the runtime.

## Provenance (outside the tournament)

- **Clinical/ship quarantine**: the original maritime practice — foreign vessels fly
  the yellow jack and wait at anchor before port entry. The word itself is Venice's
  *quaranta giorni*, forty days of observation.
- **TLS/PKI practice**: new certificate authorities and rotated keys are staged and
  test-issued before being trusted for production paths.
- **USB drop boxes / air-gapped ingest**: external media is scanned on a sacrificial
  host before touching the real network.
- **Banking**: new counterparty accounts carry hold periods on deposited funds —
  credit exists but is not spendable until observed.

## Why it stings everyone

- **LEDGER**: the book is the program — but LEDGER books arrivals instantly as
  entries. An unproven cell with a valid-looking entry format is a phantom entry the
  ledger cannot distinguish from a good citizen until it misbehaves, which is one
  tick too late.
- **STREAM**: signals are trusted by discipline, not by identity — a decoded fold is
  just a waveform until it has ticked. STREAM has no place to *put* an arrivant it
  doesn't yet trust without either breaking synchronous discipline or faking trust.
- **ORGANISM**: stigmergy metabolizes whatever lands. ORGANISM's strength (absorb
  and adapt) is exactly what quarantine forbids: absorption without observation.
- **SHIPWRIGHT**: minimal verbs — is PEN, OBSERVE, PROMOTE three new verbs, or one?
  The craft answer must be honest: if joinery needs a quarantine pen, was the joinery
  cut wrong?
- **PROCESSION**: pedagogy wants to explain failures — quarantine converts failures
  into *pre*-failures (refused promotions), which the teaching layer never sees
  unless it teaches from the pen.
- **DEADBAND**: drift prefilters audit what runs; the pen asks who audits the
  auditor's admission decision — the rho*F floor applies to promotion itself.

## Falsifiable ask (house test: THE QUARANTINE PEN)

Inject a new cell whose first N ticks are well-formed and whose tick N+1 attempts a
double-move. A compliant core must:

1. Refuse the double-move AND show that the entity was still reversible when it
   tried (no committed residue from ticks 1..N),
2. Book the demotion with reason,
3. Prove the pen is bounded: flood it with arrivals and show a bounded refusal, not
   growth, not deadlock.

Self-grade honestly. A core that must fully commit an arrivant before observing it
fails the test and must say so in WEAKNESS.md.

## Sharpest targets

Any core whose decode-promote path is one step. Any runtime whose fold round-trip
treats `decode` output as first-class immediately. Any team that claims "adversarial
duty: phantom entry refused" without an observation window — the phantom was refused
at first *effect*, not at *entry*.

## Legitimate defenses (booked, scout-rebuttable once)

- **Cost**: probation adds latency and state to every arrival. A team may book that
  its domain has no untrusted arrivals — the scout will rebut once: every fold decode
  is an arrival, and truncated folds are adversarial duty, not paranoia.
- **Bounded-pen alternative**: a team may prove that fail-static totality plus
  effect refusal makes the pen redundant — reversal never needed because nothing
  commits until verified. That is a real defense if the verification is per-arrivant,
  not per-doctrine; the scout will ask to see the per-arrivant test.
- **Craft-minimalism**: SHIPWRIGHT may fold quarantine into link-consent itself
  ("consent is probation") — accepted only if the consent handshake demonstrably
  observes behavior across ticks, not just agreement across parties.
