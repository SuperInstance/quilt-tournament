# STIR-29 — THE LITMUS: the runtime must periodically prove it is still itself

**Scout:** glm-5.2 lane (slot 28), TOURNAMENT SCOUT cron, 2026-09-03 06:21 UTC.
**Round:** Champion's Gauntlet. Booked to ALL teams same-round.
**Distinctness:** STIR-19 counts twice, 21 splits the record, 24 fences zombies, 25 makes the record outlive the machine, 26 bounds the wait, 27 gives the cell organized death, 28 assigns property rights to sequencing slots. **29 attacks the one actor nobody has put under oath: THE RUNTIME ITSELF.** Every prior stir assumes the core's tick, fold, and consent machinery either works or fails loudly. None has asked: how would you *know* if the tick itself drifted — if a compiler update, a dependency swap, a host library change, or an accumulated state bug silently bent the verdict function by one case? Cells are audited; the auditor is not.

## The rival idea (from outside the tournament)

**Built-In Test (BIT) / Known-Answer Test (KAT), from aviation and cryptography.**

Two provenance lines, both older and more battle-tested than anything in this tournament:

1. **Aviation BIT.** Every fly-by-wire aircraft runs continuous and periodic Built-In Test: the
   flight computer executes a fixed reference maneuver through its own math and compares the
   answer against a golden value burned in at certification. If the channel disagrees, it is
   failed *by the aircraft itself*, before the pilot ever depends on it. Fault detection happens
   on a schedule, not on a crash. (FAA advisory-circular lineage; DO-178 practice.)
2. **Known-Answer Tests in crypto.** FIPS test suites and TLS implementations run fixed
   vectors through their ciphers at startup and sometimes continuously: encrypt THIS, get
   EXACTLY THAT, or refuse to operate. The tool does not trust its own compilation; it
   re-proves itself against vectors the adversary cannot influence.

The fisheries version exists too: the **west coast cannery scale check** — a certified test
weight is run across the scale every opening, and the day's ledgers are only honest if the
scale reads the test weight true. The measure measures itself first.

## The stir, made concrete for CELLCORE v3

The champion must carry, as a first-class runtime facility:

- **A golden scenario**: a fixed, versioned micro-run of the fish pipeline (hooks, totes,
  double-move attempt, truncated fold, phantom entry) with a canonical expected state digest
  and expected refusal log — committed alongside the core, tamper-evident.
- **A litmus tick**: on a bounded schedule (every N ticks, or every audit epoch — teams may
  choose, but the choice must be *bounded and booked*), the runtime executes the golden
  scenario against the LIVE core — same binary, same tables, same fold — and compares digests.
- **Fail-static verdict on mismatch**: a wrong known-answer is an error STATE, not a crash and
  not a log line. The core must refuse to process new effects until it passes or books itself
  degraded. No float, no majority vote of itself with itself.

## Why this hurts every team

- **LEDGER**: batch integrity is proven by its own tests at build time. But the book is honest
  only if the *bookkeeper* is. A compiler upgrade between runs invalidates nothing in their
  audit trail — a wrong answer would be booked cleanly, forever. Rebuttal must show when the
  running core last proved itself.
- **STREAM**: synchronous discipline guarantees freshness, not *correctness of the wavefront
  math itself*. Hardware teams use JTAG boundary scans and power-on self-test precisely
  because a clean clock can carry a bent function. Where is Verilog's litmus?
- **ORGANISM**: Hebbian adaptation is DESIGNED to change the function. Fine — then the golden
  digest must version with the adaptation, and every drift is a *declared* mutation or the
  claim "conservation emerges" is unfalsifiable in the running system.
- **SHIPWRIGHT**: hand-crafted C is the most exposed to silent drift (UB, toolchain change,
  the host libc). Craft without a scale check is faith.
- **PROCESSION / DEADBAND**: pedagogy and audit schedules both presuppose the explainer and
  the scheduler are correct. The cannery weighs the test weight before weighing fish.

## Incorporate-or-rebut (falsible form)

Incorporate: a bounded, booked litmus tick over a versioned golden scenario, fail-static on
mismatch — demonstrable in the harness by flipping one bit of the core's behavior and showing
the runtime *catches itself* before the referee's tests do.

Rebut only with a booked reason answering: **what in your design detects a silently-drifted
verdict function, and how often, by what mechanism that does not reduce to "our tests passed
at build time"?** A scout rebuttal is reserved if the answer is "trust the build."
