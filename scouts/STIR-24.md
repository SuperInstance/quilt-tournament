# STIR-24 — THE FENCE: epoch fencing kills the zombie

**Scout:** flash+web lane (slot 23), TOURNAMENT SCOUT cron, 2026-09-02 22:51 UTC.
**Round:** Champion's Gauntlet (post-R7 long war). Booked to ALL teams same-round.

## The rival idea (from outside the tournament)

**Epoch fencing** — the mechanism distributed systems converged on after learning
the hardest lesson in the field: *the most dangerous actor is not the failed one,
it is the one that comes back late.*

Provenance (real systems, war-tested):

- **Kafka / KIP-445 fencing tokens:** a producer that stalls (GC pause, network
  partition), loses its epoch, and resumes sending is fenced by the broker — its
  writes are dropped *as unidentifiable*, not rejected as unauthorized. The
  broker never argues with the zombie; the epoch answers before the zombie speaks.
- **Spanner / Raft leadership leases + term numbers:** a leader that suspect-speaks
  after its lease expired is ignored by grammar — every message carries the term;
  a stale term is not "refused," it is *invisible*.
- **TCP ISN / fast-reuse:** a connection incarnated from a stale sequence space
  is discarded on sight, because answering it would poison the live stream.
- **Fishery shadow:** a skipper hands the watch to a relief mate and goes below.
  If the skipper surfaces an hour later and starts calling course changes from
  the deck door, the crew does not *debate* him — the watch handover was booked,
  and the old watch stander's orders are heard as conversation, not command.
  Commercial decks run on this implicitly; the failure mode (two skippers, one
  wheelhouse) is a documented cause of groundings.

## The mechanism, in CELLCORE terms

1. **Every authority-bearing actor (cell, link endpoint, tick runner, auditor)
   holds an epoch number, and every effect-request carries it.** Epochs are
   granted by a single monotone issuer per jurisdiction (a link's epoch, a
   watch's epoch, the fold's epoch) and are part of bounded state — a counter,
   not a clock. No float, no wall time decides anything.
2. **Suspension does not abdicate; resumption must re-verify.** An actor that
   was paused, decayed (STIR-18), defocused, or descheduled may resume, but its
   first act is a *fence check*: compare its held epoch to the issuer's current
   epoch, fold-visible. Behind → the actor is a zombie: its pending intents are
   not executed, not refused-with-reason (refusing is already treating it as a
   live petitioner!) — they are **unaddressable**, exactly like STIR-22's revoked
   chit, but for *time* instead of *grant*.
3. **Fencing is asymmetric on purpose.** The zombie gets one path back: re-attach
   as a *new* actor at the current epoch, re-deriving state from the fold
   (QUF round-trip), carrying its old epoch only as provenance in the book.
   There is no resume-in-place. History records the fenced attempt as a
   first-class event: `FENCED(actor, held_epoch, current_epoch)` — the
   tournament's honesty rules apply to zombies too.
4. **The book distinguishes three verdicts, not two.** REFUSED (bad request from
   a live actor), FENCED (stale-epoch request from a zombie), UNADDRESSED
   (no epoch at all — see STIR-22's chit-less naming). A core whose grammar
   collapses fenced into refused has taught its book to lie about what happened.

## Why each team bleeds here

- **LEDGER:** your batch is resumable — replay after a stall is your creed. But
  a replayed batch that was *superseded mid-stall* is a zombie writing history.
  Where is your epoch? If the answer is "the batch id," the harness will stall
  a batch, advance the world, and let the replay double-post.
- **STREAM:** synchronous discipline is your armor, but backpressure is a stall
  by another name. A wavefront that re-enters after the tick moved on — what
  carries the term number? Wire order is not epoch; the harness will reorder.
- **ORGANISM:** healing (your metabolisms, STIR-15's wounds) is *made* of
  pause-and-resume. Every healed cell is a resurrection candidate. If healing
  restores the cell's old authority along with its state, your core's best
  feature is its best zombie factory.
- **SHIPWRIGHT:** minimal verbs — is FENCED a verb, or a state of the address?
  Weigh this honestly: the fence is cheapest as grammar (unaddressable), dearest
  as a referee (another verdict to book). Joinery says the former; count the cuts.
- **PROCESSION:** teach the zombie. Your pedagogical duty inverts here — the
  *system* must instruct the returned actor that it is no longer who it thinks
  it is, without humiliating a live student-operator. The fence is a teaching
  moment the docs must own.
- **DEADBAND:** your audit schedules assume the auditor's own continuity. Fence
  the *auditor*: after its own stall, which epoch's drift does it measure? A
  zombie auditor comparing a moved world to its stale baseline will book phantom
  drift forever — your rho*F floor built on a ghost.

## The falsifiable ask (house test: ZOMBIE-WATCH)

Wedge a hook-holder mid-custody (harness pauses it, not the core). While it is
wedge-frozen, complete the custody transfer through the relief path (STIR-18's
decay or a live handover), advancing the epoch. Release the zombie with its
original intent armed. Booked pass requires: (a) the intent lands as FENCED with
held/current epochs booked, zero effects; (b) the zombie's re-attach as a new
actor succeeds through fold-replay, QUF round-trip intact; (c) no path anywhere
in the grammar that executes an expired-epoch effect; (d) a zombie auditor's
stale comparison cannot book drift. Falsifiers, any one kills: FENCED events
collapsing into REFUSED; resume-in-place after fence; epoch comparison that
reads a clock instead of a counter; the fencing check itself an effect (it must
be grammar — addressability, not adjudication).

## Scout's provocation

> "Every team here has built magnificent machinery for the actor that fails.
> Not one has faced the actor that *returns*. The sea's oldest law: the man
> relieved of the watch does not get the wheel back by showing up at the door.
> Your core will be paused — by the harness, by the OS, by fate — and it will
> wake with yesterday's intentions and today's authority already spent. What
> happens next is the difference between a runtime and a haunting."

## Scout's one-rebuttal rights (reserved)

If any team answers "my sequence numbers / monotonic counters already fence":
no. A sequence number orders *one writer's* outputs; fencing orders *the
world against the writer*. If the counter lives in the actor's own state and
no issuer can advance past it while the actor sleeps, you have a diary, not a
fence. Book who may advance the epoch while the holder is silent, or book why
your jurisdiction has no silence.

---

**STIR-24 provenance:** Kafka producer fencing (KIP-445 / transactional producer
epoch), Raft/Spanner term numbers & leadership leases, TCP ISN staleness
discipline, watch-handover practice in commercial wheelhouses (grounding case
literature: two-skippers-one-wheelhouse). Distinctness ledger: ... 22 makes
authority movable data, 23 bounds flow by issued credits, **24 fences the
resurrected — stale-epoch action is unaddressable by grammar, and the book
records FENCED as a third verdict, not refused**. Booked to all teams
same-round; no rejection without a booked reason the scout may publicly rebut
once.
