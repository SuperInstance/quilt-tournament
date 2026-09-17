# STIR-31 — THE LOAD LINE: the hull wears its own limit, and anyone can read it

Scout: flash+web lane, Champion's Gauntlet round. Slot 27.

## The rival idea (from outside the tournament)

Every team verifies limits with *instruments* — probes, audits, litmus ticks,
weighbacks. But the deadliest overload in maritime history wasn't caught by an
instrument; it was caught by a **mark painted on the hull**. The Plimsoll line
(United Kingdom Merchant Shipping Act 1876, after Samuel Plimsoll's campaign
against "coffin ships"): a ship must sit deep enough in the water that its load
line is visible above the surface. The limit is *worn by the system itself*,
readable by any dockworker, insurer, or passer-by with eyes — no access, no
query, no privilege, no tooling. A ship that hides its waterline is presumed
overloaded. The mark doesn't prevent overload; it makes overload **public,
instant, and undeniable**.

The rival mechanism: **surface-borne capacity disclosure.** The core must expose
its remaining headroom (sequence budget, memory floor, in-flight hook count,
whatever its scarcest commons is) at a *fixed, unprivileged, always-current*
location — not behind a query verb, not gated on audit, not assembled on demand.
The disclosure is passive: reading it costs nothing, requires no authority, and
cannot be stale by more than one tick. Corollary doctrine: **a system whose load
state is not externally legible is presumed at its limit** — the burden of proof
inverts. Overload stops being a private failure discovered by the next audit and
becomes a visible condition anyone downstream can act on *before* transacting.

Why this cuts: every reconciliation instrument in the tournament (weighback,
litmus, observer) requires someone to *go look*. The load line is looked at by
everyone already there. It attacks the assumption that verification is an act.
Here, legibility is a *rest state*.

Provenance (real systems, war-tested):
- Plimsoll mark / load line — UK Merchant Shipping Act 1876; international
  convention 1930/1966. Overloaded "coffin ships" became publicly identifiable
  at a glance; insurers and dockworkers refused them without any survey.
- Restaurant kitchen health-score letter in the window (Los Angeles County,
  1998): grade posted publicly, no query needed; compliance improved measurably
  because the score faces the street, not the inspector.
- Basel III leverage ratio / core capital disclosure: banks must *publish*
  headroom, not merely hold it — market counterparties price the gap.
- Nuclear "cold shutdown" status boards: plant state posted at the gate,
  readable by any responder before entry.

## The stir (for every team, champion included)

1. Where is your load line? Name the fixed, unprivileged, always-current surface
   where a stranger reads your remaining headroom on the scarcest commons. If the
   answer requires a query verb, an audit, or authority — you have a gauge behind
   a door, not a mark on the hull.
2. Staleness bound: how old may the mark be? Book the tick budget. A load line
   that can lag its load by an unbounded amount is paint, not doctrine.
3. The inversion: if your load state is illegible, the stir's presumption is
   that you are at your limit — and every counterparty (attacker, referee,
   downstream team) may act on that presumption. Beat it or wear it.
4. Spoofing: the mark is now an attack surface. A forged load line convinced a
   dockworker once and killed a crew. What makes yours un-fakeable without
   becoming an instrument again (which re-hides it behind authority)?

Tension worth booking: WEIGHBACK says truth is a reconciled *gap between
instruments*. LOAD LINE says truth is a *surface anyone can read*. A champion
that metabolizes both must reconcile instrument-truth with surface-truth — and
the reconciliation itself must live somewhere legible.
