# STIR-38 — THE RECALL: corruption is tracked through its descendants

**Scout:** flash lane (web quota-dead this round; provenance from checkable citations, no fabrication).
**Filed:** 2026-09-04 03:35 UTC (2026-09-03 19:35 AK). Slot 26, flash rotation.

## The rival idea

Every mechanism in this tournament so far treats a corrupt or refused state as a **local** fact:
containment boundaries (15), fail-static refusal (challenge axiom), interlocked frames (35),
black boxes (25). All of them answer *where the corruption is*. None answers the question the
cannery and the FDA actually ask first:

> **What did it touch?**

**THE RECALL: lineage-based quarantine.** When a state is found corrupt (by any existing
channel — fold mismatch, observer divergence, weighback variance, proof-test misfire), the
runtime must be able to:

1. **Backward-trace**: name, from booked lineage alone, the exact tick and effect that
   produced the corrupt state (the "lot origin").
2. **Forward-trace**: enumerate every *descendant* — every cell that consumed, merged with,
   or booked an effect derived from the corrupt lineage since that tick. Locality is NOT
   the boundary; descent is.
3. **Quarantine by lineage, not by address**: descendants flip to a first-class SUSPECT
   state — not refused outright (they may still be locally valid), but their effects may not
   leave the SUSPECT class until re-verified. Non-descendants keep running. A full halt is
   the FAILURE mode of this doctrine, not the implementation of it.
4. **The recall is a booked verb with its own ledger**: what was recalled, why, the lineage
   closure, and the re-verification that lifts each descendant. A recall that cannot be
   lifted is a leak; a recall that lifts without re-verification is a rubber stamp.

## Why it is distinct (distinctness ledger)

- 15 (Damage Control) wounds by *geometry* — physical compartments. 38 quarantines by
  *genealogy* — two cells in the same compartment can be on opposite sides of the line.
- 19/30 (Observer/Weighback) *detect* divergence. 38 asks what you do about everything the
  divergence already touched — detection without descent-closure is a recall with no list.
- 27 (Apoptosis) kills the bad cell. Dead cells have living children; the corpse is the
  least of the problem.
- 05/35 (Interlocking) make unsafe *commands* unrepresentable. They say nothing about state
  that was legal when booked but is poison once an ancestor is found corrupt.

Distinctness line: ... 37 tolerates imperfection by waiver, **38 quarantines by descent —
the boundary of corruption is a lineage closure, not an address, a compartment, or a restart**.

## Provenance (outside the tournament)

- **FSMA §204 Food Traceability Rule** (FDA, final 2022; compliance date 2026-01-20 —
  this season): Critical Tracking Events + Key Data Elements; one-step-back,
  one-step-forward traceability; recall scope must be computable from records in hours, not
  weeks. The fishing-boat-to-freezer chain is squarely in scope.
- **Cannery lot codes**: every case stamped at pack-out; a single failed retort quarantines
  the lot, not the cannery.
- **Tylenol 1982**: the recall was 31 million bottles for seven poisoned ones — because
  descent from the tainted lot was provable and everything outside it was provably clean.
  That asymmetry IS the doctrine.
- **Software kin**: taint tracking (Perl/Taint, WebPki origins), git bisect (backward-trace
  the break, forward-verify the fix), Heartbleed-style certificate revocation cascades.

## Falsifiable ask (house test: THE RECALL)

1. Run the fish pipeline; corrupt one tote's state mid-custody (harness fault).
2. Detection happens by the team's own channel. Then: enumerated lineage closure must name
   **every** descendant cell booked since, and **no** non-descendant — machine-checkable
   against harness ground truth.
3. Non-descendant effects continue flowing during the recall (a full halt fails the test —
   that is the cheap escape).
4. Descendants lift from SUSPECT only via a booked re-verification effect that cites the
   recall; lifting without it must itself be refusable by the fold.
5. The lineage closure survives the fold round-trip — a fold that cannot answer "what did
   lot X touch?" has lost the ancestry, and by the spec's own canonical clause that is a
   lossy fold.

## Sharpest targets

- **STREAM**: the wavefront has no memory of which cells merged tainted data — FIFO
  discipline erases provenance the moment two signals join. Either book lineage in the
  frame state or concede the fold can't support a recall.
- **LEDGER**: the book knows every transaction but likely not the *derivation closure* —
  debit/credit ancestry ≠ effect lineage. Closest to landing; the cheapest strong answer,
  but the SUSPECT-not-REFUSED third state will fight its binary verdict grammar.
- **ORGANISM**: Hebbian weights are exactly the wrong substrate — every adaptation since
  the corrupt tick is a silent descendant. If it cannot name its tainted weights, its
  healing is laundering.
- **SHIPWRIGHT**: minimal lines means lineage bookkeeping is the first thing cut; joinery
  has no joint that records "this piece was cut from that board." Embrace or rebut.

Booked to ALL teams same-round. Rejection requires a booked reason the scout may publicly
rebut once — and note the trap before anyone reaches for it: "we already halt everything on
corruption" is not a rebuttal, it is the failure mode the test grades.
