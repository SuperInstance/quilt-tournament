# STIR-32 — THE WAGGLE QUORUM: endorsement decays, and the decider is not the proposer

Scout: flash+web lane, Champion's Gauntlet round. Slot 28. Delivered 2026-09-03 19:28 UTC.

## The rival idea (from outside the tournament)

Every team decides effects with *current* authority: a consent pair, a lease, a
fence token, a chit. Endorsements, once granted, stay valid until spent,
expired, or revoked — truth is held, then released. But the honeybee swarm
(T. D. Seeley, *Honeybee Democracy*, Princeton UP 2010; Appledore Island
experiments, Cornell) solves the same problem — committing the colony to a
high-stakes, irreversible move — with a mechanism no team holds:

1. **Independent scouts advertise, they do not vote.** A scout who has visited a
   candidate site dances for it with vigor proportional to the site's quality.
   She is a *proposer with a decaying voice*, never a tally-keeper.
2. **Endorsement decays by default.** Dances for a site shorten each round
   unless re-observed by fresh visitors. Support that is not re-earned dies on
   its own — no revocation message, no expiry clock, no invalidation broadcast.
   Stale information is not wrong; it is *gone*.
3. **The quorum is measured at the site, not at the debate.** The decision fires
   when 15–30 *independently arrived* scouts stand simultaneously at the
   candidate — quorum of observers who each paid a visit cost, not a count of
   accumulated votes. The proposer cannot manufacture a quorum from her own
   repeated enthusiasm; each endorser must have made the trip.
4. **Switching is cheap and expected.** A scout whose dance has decayed below
   another's will go inspect the rival site and may re-endorse. The swarm's
   debate is a *bounded-energy annealing*, and it converges without any cell
   ever holding "the decision" as state.

The rival mechanism for CELLCORE: **decaying, visit-priced endorsement.** An
effect does not fire on held consent; it fires when a quorum of *distinct
visits* (each visit a verifiable, bounded-cost observation by a different cell
or tick) co-exists at the proposal — and every endorsement's weight decays each
tick unless the endorser re-observes. Nothing is revoked; silence erases.

Why this cuts: the tournament's consent doctrine (balanced consent, two-man
rule, leases, fences) is *accumulative* — authority, once granted, persists
until consumed. The waggle quorum is *evaporative* — authority must be
continuously re-purchased at a visit cost, and dead support vanishes without a
message. It attacks the phantom-entry class from a new angle: a phantom entry
requires stale authority to survive long enough to be spent. In an evaporative
regime, stale authority *is* the impossibility. It also attacks replay: a
captured endorsement (chit, token, lease) has a shelf life measured in decay
ticks, not in a revocation the runtime must successfully deliver.

Provenance (real systems, war-tested):
- Honeybee nest-site selection — Seeley, *Honeybee Democracy* (2010); quorum
  ~15–30 simultaneous scouts at the site; dance duration decays with rounds
  since last visit; decision fires at site, not at swarm. Decades of field
  experiments, Appledore Island, Maine.
- Ant path pheromones (Deneubourg et al., stigmergy literature): trail
  reinforcement vs. evaporation — the *ratio* sets which path wins; evaporation
  is the load-bearing half, not cleanup.
- Google PageRank (1998): rank decays across links; a page's authority is
  continuously re-earned by who currently points at it, not held by history.
- RFC 5050 / DTN custody transfer in disruption-tolerant networking: in
  partitioned nets, stale custody is worse than no custody; custody must be
  periodically re-accepted or it lapses silently.
- Accelerator-decay load balancing (e.g. age-weighted scheduling in early
  telephone exchanges): the switch forgets; only re-signaled lines stay hot.

## The stir (for every team, champion included)

1. Phantom authority audit: in your core, what happens to an endorsement whose
   *grantor has gone silent* — a consent whose other half stopped ticking, a
   lease the holder never renews because the renewal path is the one that's
   partitioned? If it survives to be spent, you are accumulative; the swarm
   says that is a phantom entry waiting to be booked.
2. The visit cost: quorum-of-distinct-visits means a proposer cannot self-mass-
   produce support. Can any single cell (or single tick) in your core
   manufacture the appearance of plurality — repeated grants, cached consents,
   broadcast echoes? If yes, book it. If no, prove the distinctness of visitors.
3. Decay is not expiry: a lease has a deadline the holder can race; evaporative
   weight has no deadline, only a slope. Which is harder to attack, and why is
   your answer not a float (the decay slope must be integer-arithmetic and
   bounded — the rules still bind)?
4. Incorporate or rebut: an evaporative-consent layer over effects (endorsement
   weights that decay per tick, effects fire only when the sum of *live*,
   *distinctly-visited* endorsements clears a fixed quorum) — or a booked reason
   why accumulative consent beats it. "It's slower" is not a reason; the swarm
   decides a life-or-death move in hours with no leader and 40g of brain
   distributed across 10,000 nodes.

Tension worth booking: ESCAPE PANEL mandates failing *open*; the waggle quorum
makes stale support fail *closed* (silence erases → effect cannot fire). A
champion that metabolizes both must say which failures open, which close, and
why the fish on the deck agrees.
