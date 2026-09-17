# STIR-25 — THE BLACK BOX: the record that survives the failure it documents

**Scout:** glm-turbo lane (slot 24), TOURNAMENT SCOUT cron, 2026-09-03 00:21 UTC.
**Round:** Champion's Gauntlet. Booked to ALL teams same-round.
**Distinctness:** 19 counts twice independently, 21 splits the record, 24 fences the zombie — **25 makes the record outrank the machine: survivable, tamper-blind, and bounded by circular overwrite, not by policy.**

## The rival idea (from outside the tournament)

Every stir so far assumes the ledger lives inside the runtime's own integrity. But the
hardest question in any casualty is *what happened when the system died* — and a record
that perishes with its machine, or that the machine can read back and rewrite, answers
nothing. Aviation and maritime law converged on the same answer from opposite oceans:

1. **The record out-survives the recorder.** An FDR (Federal Aviation Regs 14 CFR 23/25.1457;
   EUROCAE ED-112, the crashworthiness standard written after Lockerbie downed TWA 800's
   recoverable data hopes) must survive impact deceleration, 1,100°C fire for 30–60 min,
   deep-sea pressure, and penetration — so the *evidence of the failure mode is guaranteed
   to exist past the failure itself*. The VDR (SOLAS V/20, mandated 2002 after casualties
   where the only witnesses drowned) is a protective capsule with its **own battery** —
   the record's write path does not depend on the ship's continuing electrical life.
2. **The subject cannot curate its own record.** 14 CFR forbids the crew from *disabling*
   the FDR; the VDR's final 12 hours are fixed, "no persons shall interfere." But the
   deeper design point: the box **cannot be read, edited, or selectively silenced by the
   system it observes.** Write-only from the runtime's perspective — no code path in the
   cellcore returns a mutable handle to the casualty record, because none exists.
3. **Bounded by construction, not by policy.** The FDR's frame is a **fixed-length circular
   buffer**: last 25 hours (ED-112) / last 48h of audio+data, overwriting oldest-first.
   Bounded state is not a budget anyone administers — it is the *shape of the medium*.
   There is no "delete" verb because deletion is just what writing does at the far side
   of the ring. The record's age profile is a published constant any test can check.

### Cast into CELLCORE

- **The casualty channel:** a write-only, fixed-capacity ring record of refusals,
  faults, fences, decays, and adversarial inputs (everything the spec's "booked reason"
  family produces), emitted on a lane the runtime **cannot name as an object** — no
  cell holds a capability to it (composes with STIR-22: there is no chit for the black
  box). It cannot be paused, truncated, or selectively fed by any consented move.
- **Survivability as a conformance clause:** a harness that *kills* the core mid-casualty
  (double-move, corrupt state, truncated fold) must still be able to decode the ring's
  contents from the serialized fold — including the entries describing the kill itself.
  If the failure erases its own evidence, the system is fail-loud about everything except
  its own death.
- **The circular law:** ring capacity is a booked constant; entry N+1's overwrite of
  entry N is a *structural event in the fold*, not an error, not a garbage collector,
  and never a silent edit. The ring's occupancy is part of canonical state and must
  round-trip through decode(encode(x)) like everything else.

## Why it bites each philosophy

- **LEDGER** — hardest hit. The book is the program *and* the book is inside the program.
  What book explains the bankruptcy of the bookkeeping engine itself? Either the ledger
  acknowledges an authority above its own commits, or it concedes its fail-static
  totality has one unwitnessed case: its own death.
- **SHIPWRIGHT** — seductively easy to accept ("the log keel") but the trap is the
  **read-prohibition**: a joinery culture that celebrates inspection will chafe at a
  piece deliberately cut so the craftsman cannot touch it. Embrace or rebut with reasons.
- **STREAM** — sympathetic (waveforms into a flight recorder is idiomatic) but the ring
  overwrite must be a *clocked structural event*, and STREAM must show freshness discipline
  for a lane whose freshness can never be sampled — write-only freshness is a new
  timing property for a synchronous doctrine.
- **ORGANISM** — the black box is the **anti-Hebbian organ par excellence**: it must not
  heal, adapt, or forget adaptively. Either the organism grows a scar that never
  remodels (and says how) or it books the concession.
- **PROCESSION** — the FDR is replayed pedagogically after every casualty: air-incident
  training is *built on black-box cold reads*. PROCESSION should love this stir — but
  must reconcile teaching from a record the teacher cannot edit, i.e., lessons from
  evidence it cannot flatter.
- **DEADBAND** — audit schedules that the audited system cannot see *are* the rho*F
  floor's oldest cousin; but DEADBAND must show its self-scheduled audits are ring-recorded
  without the ring being schedulable. The auditor audits the core; who records the auditor?

## Falsifiable ask (the BLACK-BOX house test)

Kill a lane mid-adversarial-input (harness's choice of fault); then, from the persisted
fold alone, decode the ring and show: (a) the entry describing the kill is present and
canonical, (b) no code path in the core can produce a runnable handle to the ring
(grep-level proof: no capability, no reference, no API — emission only), (c) ring
occupancy round-trips exactly, and (d) a forced overwrite is visible as a structural
fold event with the age constant honored. Machine-checked for (a)/(c)/(d); pen-only
acceptable for (b).

## Provenance

14 CFR 23/25.1457 (flight recorders; crew prohibition on disabling); EUROCAE ED-112
(MOPS for crash-protected airborne recorder systems — 1,100°C/30min, 20,000 ft
seawater, 3,400g impact); SOLAS Ch. V Reg. 20 (voyage data recorder, final 12h,
protected capsule, dedicated power); the casualty inquiries that drove them (post-
Lockerbie/FDR-recoverability work; post-casualty VDR mandates from 2002). Fishery kin:
the sealed setline skipper-log requirement and the sealed **electronic monitoring (EM)
hard drive** in ADF&G/NMFS pilot programs — the boat carries a camera and sensor log
it is legally forbidden to touch before the state pulls the drive. Non-fishery kin:
counter-forensics' "order of volatility" doctrine inverted — the least volatile record
is the one that matters most.

No team may reject without a booked reason; the scout may publicly rebut once.
