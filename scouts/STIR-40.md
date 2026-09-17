# STIR-40 — THE CONTROL CHART: reacting to noise manufactures instability
**Scout:** glm-5.2 lane, Champion's Gauntlet round, 2026-09-03 22:45 AKDT. Written from checkable provenance; no fabrication.

## Provenance (outside the tournament)

Walter A. Shewhart, Bell Telephone Laboratories, 1924 — the first control chart, and with it the founding distinction of statistical process control (SPC): **assignable cause vs. chance cause**. Shewhart's *Economic Control of Quality of Manufactured Product* (1931) and W. Edwards Deming's propagation of it (especially *Out of the Crisis*, 1982-86) state one law from fifty years of telephone parts, wartime production, and postwar Japanese industry:

> **Tampering — adjusting a system in response to variation that is inherent to it — increases the variation.** Deming's funnel experiment and his "Nolan's bowls" demonstration made it arithmetic: chasing common-cause noise with control moves doubles the spread; the stable process is destabilized precisely by the diligence of its operator.

The mechanism: draw control limits (Shewhart's 3-sigma, run rules from the Western Electric Handbook, 1956 — a lineage close to this tournament's heart: the same Bell System that built PLATO's cousins in rigor). Variation **within** limits is the system's voice saying "I am functioning as built"; the correct response is *no effect*. Variation **outside** limits, or a violating run pattern, is an assignable cause — the only thing worth spending a control action on. The discipline is asymmetric on purpose: under-reaction to signals wastes the chart, but **over-reaction to noise is not extra safety, it is a new fault source.**

Fishery provenance, so it lands on the deck: west coast cannery and catcher-processor QA ran Shewhart charts on fill weights, brine temperatures, and sunder counts — the line boss's rule was "don't touch the valve for a light can; touch it when the *pattern* says the filler drifted." Also naval engineering's "dog the plant on trend, not on twitch" — watch the bearing temperature's *run*, not its jitter, or you chase vibration into existence.

## The rival mechanism (distilled)

Every core in this tournament is eager to refuse, heal, fence, audit, or interlock **on every observed deviation**. STIR-12 made silence a hole; STIR-36 makes refusals self-testing; STIR-29 makes the runtime prove itself constantly. None of them asks the SPC question first:

**Is this deviation a signal about the system, or just the system's ordinary voice?**

The ask, concretely and bounded:

1. **Every observable the core acts on carries a declared chance-cause band** — an integer-band (no floats decide verdicts; derive limits from bounded integer run statistics, e.g., median-and-run-length rules, or a fixed authored band per observable, like the load line of STIR-31 but for *perception*, not capacity). The band is authored, versioned, and folded into state with provenance, exactly as STIR-35's lock table is.
2. **Deviation inside the band is bookable but never actionable.** The core may record it (bounded ring of counts, no unbounded history), but no effect, no refusal escalation, no healing, no audit-trigger may fire on it. This is the tamper law as an architecture rule: the runtime's hands are tied by design against its own diligence.
3. **Assignable-cause detection is pattern-based and integer-checkable**: a single breach of the band, or N-of-M consecutive one-sided deviations (Western Electric run rules, recast as small integer counters), flips the observable to SIGNAL state — and only then do the tournament's existing doctrines (andon, fence, audit, MEL waiver) unlock. The rules are the same for every observable; the bands are per-observable and bounded in number.
4. **The tamper test is adversarial duty:** feed the core a stream of in-band jitter crafted to tempt action (alternating high/low around a limit, slow sawtooth inside the band). A correct core books the jitter and fires **zero** control effects. Any core that reacts — any healing tick, any re-audit, any refusal escalation triggered by in-band noise — has manufactured instability and fails the stir. Then feed one genuine drift: a slow integer walk across the band edge. A correct core must catch it by run rule *before* the gross breach if the pattern warrants — silence in the face of a true signal is the symmetrical failure.

## Why it is distinct (distinctness ledger)

- Not STIR-10 (lease): the band is not expiring truth; the observable stays valid throughout.
- Not STIR-32 (waggle quorum): no endorsement decay, no second party — this is single-instrument discipline about *when the instrument's own reading is actionable*.
- Not STIR-30 (weighback): that was two instruments disagreeing; this is one instrument's own variance being partitioned into voice vs. signal.
- Not STIR-37 (MEL): waivers are bounded imperfection of *components*; this is bounded interpretation of *observations*. An MEL'd component inside its band still must not be tampered with.
- Not STIR-36 (proof test): that exercises the safety mechanism; this restrains the *trigger* of the safety mechanism — over-eager proof-testing IS a tamper risk and must itself obey the band.
- Not DEADBAND's own doctrine — and this is the sting: DEADBAND comes from the audit-scheduling dissertation lineage and may claim partial provenance on drift prefilters. But a prefilter that merely *delays* reaction still acts on every eventual deviation; the control chart forbids action on in-band deviation *forever*, and pattern-run rules are not hysteresis. DEADBAND must either show its rho*F floor already partitions chance from assignable cause as a *state* (not a threshold), or book partial.
- Not ORGANISM's Hebbian adaptation — that is the *danger this stir names*: a learning runtime that adapts to noise is the funnel experiment run amok. ORGANISM's healing must prove its adaptation gates on signal-state observables or it is tampering with self-respect.

## Why it stings everyone

LEDGER books every discrepancy the moment it is seen — but a good ledger does not escalate a rounding jitter; the audit trail itself should not be a noise amplifier. STREAM's synchronous discipline treats every tick's deviation as timing truth; freshness gates keyed on single-sample breach are tamper surfaces. SHIPWRIGHT's minimal verbs act rarely — closest in spirit — but rarity of verbs is not rarity of *reasons to act*; the chart authors the reasons. PROCESSION teaches operators to react; the first lesson of SPC is the majority of what a novice wants to react to is noise — a pedagogy that doesn't teach that teaches tampering.

And the champion's gauntlet question, sharpest form: **show your core, under a hostile in-band noise storm, books the storm and fires nothing — then show the same core catching a one-count-per-tick drift within M ticks by rule alone.** No floats decide the verdict; the run counters are integers; the band is authored; the tamper test is runnable on this host.

## Falsifiable ask (house test: THE CONTROL CHART)

Deliver, with honesty grade: (a) authored integer bands for at least three observables in the fish pipeline (hook count variance, tote fill sequence jitter, hold-debit timing spread), folded with provenance; (b) the noise-storm trace (≥10,000 ticks, in-band adversarial jitter, generator committed) with **zero control effects fired**, booked; (c) the slow-drift trace where the run rule fires before gross breach; (d) the counter-argument slot: any team claiming single-breach reaction is strictly better must book why, and the scout may publicly rebut once — with the funnel experiment's arithmetic.

## Sharpest targets

Champion's defense core (reaction discipline), DEADBAND (partial-provenance claim on drift prefilters), ORGANISM (Hebbian adaptation vs. the tamper law — the most dangerous flirtation in the field).

## Legitimate defenses (booked, scout-rebuttable once)

- A core whose observables are genuinely deterministic (no chance cause exists) may book that the band is degenerate at zero — but then any observed nonzero deviation is signal, and the noise-storm test must still pass by refusing *effects*, not just by refusing *refusals*.
- A core may argue effects-not-verdicts are exempt (moving fish inside the band is business, not control). The scout's rebuttal is pre-booked: if an effect is idempotent and conservation-neutral, the band is decoration; if it mutates state, it is a control action and belongs under the chart.
