# STIR-30 — THE WEIGHBACK: two instruments count the same fish, and the gap is a first-class state

Scout: flash+web lane, Champion's Gauntlet round. Slot 26.

## The rival idea (from outside the tournament)

Every system so far verifies itself with instruments of its own kind. The fold checks the
encode. The tally checks the stick. The litmus checks the verdict function. But west coast
canneries never trusted one instrument: the counter's tally board, the scale's weight slip,
and the packer's tote count were **three structurally different measurements of the same
fish**, and the day ended only when they reconciled — in integers, with the gap written down
and someone's name on it. A tally that matches the tally is nothing; a tally that matches
the *scale* is a fact.

The rival mechanism: **dual-path mass accounting with booked reconciliation.** Every
conservation claim (fish in the hold, hooks paid out, totes landed) must be measurable by
at least two structurally independent enumeration paths in the core — e.g. the effect
ledger's booked count AND a state-walk that physically enumerates hold/tote contents from
serialized state alone, neither path derived from the other. The reconciliation is a
periodic tick artifact: gap = booked − enumerated, an integer, a first-class state
(WEIGHBACK-CLEAN / WEIGHBACK-VARIANCE with booked reason). Non-zero gap never blocks
operation silently and never self-heals without a booking; it ages.

Provenance (real systems, war-tested):
- Cannery weigh slips vs. tally boards vs. tote counts — daily reconciliation, signed
  variance lines (columbia river packhouse practice, 1900s–present).
- Bank reconciliation statements: ledger vs. independent statement, variance items are
  first-class, never edited away.
- Inventory cycle counts vs. perpetual book (Toyota kanban / retail cycle counting):
  the book is *expected* to drift; the cycle count is what makes honesty measurable.
- ADF&G fish tickets vs. port sampler biosamples: two agencies, two instruments, one fish.
- COSO/SoX control framework: independent reconciliation is the control; self-report is not.

## The mechanism (distilled for CELLCORE)

1. **Two enumeration paths, structurally distinct.** Path A: replay of booked effects
   (the book's arithmetic). Path B: independent fold-walk of live serialized cell state
   (count what is actually there). Path B must not consume Path A's accumulator. A core
   whose "hold count" IS the effect ledger total has only one instrument and fails this
   stir by construction.
2. **Weighback tick.** On a booked cadence (bounded ticks, no float), both paths run; the
   integer gap is emitted into the fold as state. ZERO is a measured result, not an
   assumption.
3. **Variance is a citizen.** WEIGHBACK-VARIANCE carries the gap, both totals, the tick,
   and a booked reason-class. It cannot be overwritten by the next clean weighback —
   variance retirement is its own booked effect (like STIR-21's as-pairs retirement).
4. **Fail-static on widening drift.** A gap that grows across consecutive weighbacks past
   a booked integer bound refuses new effects until reconciled. Containment, not crash.

## Why this hurts every team

- **LEDGER**: the book is the program — but a book reconciled against itself is a tally
  checking a tally. Their conservation law is single-instrument by philosophy. They must
  either add a second instrument (conceding the book alone is not ground truth) or rebut
  with a booked reason the scout will attack.
- **STREAM**: wavefront FIFO discipline guarantees delivery order, not that delivered
  effects and cell state agree after partial failure. Freshness ≠ mass conservation.
- **ORGANISM**: "conservation emerges from metabolism" — emergence is unfalsifiable until
  something independent *measures* it. The weighback is the instrument that makes their
  central claim testable — or breaks it.
- **SHIPWRIGHT**: minimal verbs probably mean one counter. Two paths is twice the lines;
  craft says don't, the stir says must. Delicious tension.
- **PROCESSION / DEADBAND**: DEADBANG schedules audits of state vs. *specification* — the
  weighback audits state vs. *independently remeasured reality*. An audit that reads the
  same accumulator the writer wrote is not a weighback. Sharpest edge of the round.

## The falsifiable ask (house test: WEIGHBACK)

Inject a phantom entry (book +=1 with no cell change) and a lost tote (cell −1 with no
booked debit). The next weighback tick must surface BOTH as integer variances with booked
reasons, in the fold, without any test-mode hook. Then corrupt the fold mid-state: the
post-restart weighback must distinguish "book drifted" from "state drifted" — variance
names which instrument lied. Any core whose two paths share an accumulator, a helper, or a
cache line of provenance fails by construction.

## Rejection cost

Rebut only with a booked reason answering: **what in your design measures the same mass by
two structurally independent paths, and where in the fold does the integer gap live when
they disagree?** "Our invariant checker passes" is single-instrument self-report — the
cannery fired tally clerks for less. Scout rebuttal reserved.

## Distinctness ledger

... 24 fences the resurrected, 25 makes the record out-survive the machine, 26 bounds the
wait, 27 executes the cell, 28 fences the commons, 29 proves the core is itself —
**30 makes the book face a second instrument: reconciliation across structurally
independent measurement is the only honesty a self-reporting system cannot fake.**

Booked to ALL teams same-round; referee to deliver; no rejection without a booked reason
the scout may publicly rebut once.
