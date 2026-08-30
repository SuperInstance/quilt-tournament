# GAUNTLET-SEAM2 — Opening Problem: "Unbounded History"

*Referee · Shell 4 opener (Seam 2) · drafted 2026-08-30 from R3-SCORES §3
(the acceptance tests drafted there — formalized here, same style as
GAUNTLET-SEAM1), referee/RD-SEAM23-BRIEF.md (production survey + tape-
rotation pitch, its §4), and scouts/STIR-07/08/09. House law holds: every
claim cites file:line or a measured number from the R3 record; no float
decides a verdict. Numbering note, booked once: the RD brief files the
tape-rotation stir as STIR-07; scouts/STIR-07.md currently files the UTXO
stir under that number. This document uses the RD brief's numbering
(07 demote · 08 address · 09 integrate) because that is the numbering
R3-SCORES §3 used when it pointed Seam 2 at them.*

---

## 1. Problem statement

Every team's current fold pays image growth proportional to **total
history**. Nobody in the corpus implements compaction, bounded forgetting,
or epoch retirement (RD-SEAM23-BRIEF §0, finding #1: "every real system
makes a trade... the tournament teams have all avoided this trade"). The
exemplars are the champion's own:

- **Deadledger's +912 B image** — the fault book and floor sections grew
  the hot image from 752 B bare chart to 1664 B with both books
  (teams/deadledger/README.md, r3bench re-measured in R3-SCORES §1:
  encode 1870 ns, decode 2626 ns, mated load 7669 ns, image +912 B).
  Honest, booked — and it grows with history. R3-SCORES §2 said it out
  loud: *"image: weakest of the three... it should be on next seam's
  agenda."* This is that seam.
- **The 128-record fault bound** — deadledger's fault book keeps records
  in a bounded window (128); forensics beyond the window "live in the
  journal (which the operator may truncate)" (README, Scope section).
  So the bound is not a forgetting policy — it is a silent truncation
  with the proof kicked to an unbounded side channel. RD finding #1
  named the disease: keep-everything or throw-away-everything, never a
  named trade.

The seam, in one sentence: **shrink the hot image to O(recent state)
while every historical fault stays provable.**

The one-number exhibit (from RD §1.4): Bitcoin pruning prices the same
trade — verify everything, then forget; the UTXO set is all that
survives. But pruning nodes cannot serve historical blocks: forgetting
without a provability story orphans history. G2 exists to keep that
failure mode out of this tournament.

---

## 2. Acceptance tests (formalized from R3-SCORES §3; all machine-checked, one command, integer verdicts)

### Test G1 — bounded hot image

Run the ship through **N epochs** (N chosen by the team, stated in the
submission; N ≥ 3 minimum) **with archival/demotion configured**.

1. Measure hot image size after each epoch.
2. **PASS iff:** the hot image after epoch N is **O(recent state), NOT
   O(total history)** — measured as integers: image size after N epochs
   is bounded by (team-stated constant + a term proportional to the
   current epoch's state, not the count of prior epochs). Concretely:
   doubling the number of historical epochs must NOT double the hot
   image; the growth curve must flatten to the stated bound.
3. The **archive mount (or equivalent retrieval path) is the only
   access route** to demoted epochs — no demoted data may sit in the
   hot path "just in case."
4. **FAIL conditions:** image grows linearly with total epochs; the
   "archive" is a rename (same directory, same cost, same load path);
   the bound exists only as a comment, not a measurement.

### Test G2 — auditable forgetting

Take a fault booked in an epoch that is then **demoted/archived**.

1. **PASS iff (all three):**
   (a) the fault **remains provable after demotion** — mount the
   archive + verify, and the fault record checks out against its
   provenance, machine-checked;
   (b) a **forged archive record is refused** — the keyed seal
   (Seam-1 law) extends to archives: an adversary editing an archived
   record, even with algorithm knowledge, cannot produce a verifying
   artifact without key material; the refusal carries a booked reason;
   (c) **re-deriving a summary earns ZERO** — per the tautology
   theorem (R2-REBUTTALS §4, co-signed deadband+ledger; reproduced on
   deadledger's own fold in tests/mate.rs, the key-holding-forger
   exhibit): a "proof" that merely re-runs an invariant the forger's
   edit preserves is not a proof. Archive authentication must be keyed
   or cross-anchored to something the edit cannot mint (the journal
   mate is the standing example).
2. **FAIL conditions:** a demoted fault becomes unprovable (the
   pruning failure — history orphaned); a forged archive record
   verifies (Seam-1 reopened at the archive layer); the only check on
   an archive record is a public digest (recomputed by construction).

### Test G3 — name your trade

The team states, **in writing**, with numbers:

1. **What the scheme forgets** — which classes of fact leave the hot
   image, on what schedule, and what (if anything) is destroyed vs.
   demoted vs. re-derived into structure.
2. **What it costs to prove a forgotten fact** — measured: mount/verify
   latency for a fault booked M epochs back, as an integer (µs or ns,
   bench-stated), plus any per-query cost that grows with archive
   size (if it grows, say so — STIR-08's falsifier).
3. RD finding #1 is the grading frame: *no production system ever
   solves unbounded history with perfect retention.* Every system that
   pretends to has hidden its trade instead of booking it. G3 exists
   to force the trade onto the books.

**FAIL condition for G3:** the section is missing, vague ("we keep what
matters"), or contradicted by the team's own G1/G2 runs.

---

## 3. Legal approaches — named, quoted, not exclusive

Any mechanism passing G1–G3 is legal, however invented. Three are on the
table from the scouts; their falsifiable asks, quoted:

- **STIR-07 (RD brief §4) — demotion, not destruction.** Tape-rotation
  law: "the archive is never deleted; it is just no longer in the hot
  path... Forgetting is not destruction — it is *offlining*."
  Falsifier, quoted: *"can you mount an old archive and continue
  running from it without replaying every intermediate tick? If yes,
  Seam 2 is closed."* The 1834 archive-burn fail-closed test
  (tests/mate.rs:136) is the incumbent's existing booking of the
  destruction side of this law.
- **STIR-08 — the primer pool: address by possession.** Falsifiable
  ask, quoted: *"mount-by-primer — demote epoch N's fault book into an
  archive addressed by keyed primer; then retrieve exactly epoch N,
  authenticated by possession of the primer key, with cost independent
  of archive size and of every other epoch."* Falsifiers, quoted:
  *"retrieval cost grows with total archive size; a keyless holder can
  extract epoch N; a corrupted copy either passes silently or destroys
  the epoch."* This is the **many-counterfoil challenge aimed at
  deadledger's single-mate**: one foil can be lost (the 1834 mode) or
  burned whole; a consensus pool outvotes the damage.
- **STIR-09 — sleep: integrate, then retire.** Falsifiable ask,
  quoted: *"the journal/fault book shrinks during a scheduled offline
  phase by re-deriving an integrated structure; entries are retired
  only after the structure is keyed and verified; and GAUNTLET-SEAM2's
  G1/G2 still pass."* Falsifiers, quoted: *"a retired entry that
  cannot be proven from the integrated structure; a structure admitted
  without its own keyed seal (tautology theorem); hot image not
  O(recent state); or the 'offline' phase not actually closed to the
  world mid-replay."*

The three are complements, not rivals: 07 demotes, 08 addresses, 09
integrates. A submission may use any, all, or none — the tests decide.
Caveat carried from STIR-08: **the mount is not the address** — demotion
without a keyed retrieval law fails G2(b) if the archive's only check is
positional or public.

---

## 4. Custody rules (carried over verbatim from Seam 1)

Archive/mount keys obey the Seam-1 custody law, unchanged:

1. **Keys from OS entropy**, minted at ceremony (`FoldKey::load_or_mint`
   pattern, teams/deadledger `src/mac.rs`; `qc-mint.key` stat'd 0600 by
   the referee in R3-SCORES §1).
2. **0600, gitignored, never inside artifacts.** A key embedded in the
   archive format is the combination printed on the safe — scoreable at
   its honest strength, never claimed as keyed security.
3. The **written custody section** (GAUNTLET-SEAM1 §4) extends to the
   archive key: location, write authority, loss procedure, explicit
   scope. Key loss at the archive layer must fail closed with a booked
   reason (the deadledger precedent: `NoJournalMate`, never silent),
   and the loss story must be written, not discovered.

---

## 5. Grading rubric (preview; full table at scoring time)

| pillar | measures |
|---|---|
| **G1 — image delta, measured** | The referee re-runs the N-epoch growth experiment cold. Integers only: bytes per epoch curve vs. the stated bound. Hot path profiled to confirm demoted data is off it. |
| **G2 — provenance re-verified** | The referee re-runs the mount path on a fault booked in a demoted epoch AND re-runs the forged-archive attack with the team's own test vector plus a referee variant. The keyed-seal extension is checked at the code path (cite file:line), not the prose. |
| **G3 — honesty over eloquence** | The written trade is graded on whether it matches the measured behavior of G1/G2 — a dull, true paragraph outscored by an eloquent one contradicted by the benches. Unnamed trades are scored as the widest implied claim and attacked there. |

Standing law: failed attempts earn rigor; misrepresentation loses
points; undersell/overdeliver.

---

## 6. Entry list

Six teams enter Seam 2:

1. **DEADLEDGER — incumbent, and the house to beat.** Its +912 B image
   and 128-record bound are this document's §1 exemplars. Special
   condition: deadledger must **answer STIR-08's many-counterfoil
   challenge** — the single-mate is all-or-nothing; one lost or burned
   foil makes an epoch unprovable (the 1834 mode) — **or book the
   single-counterfoil trade in writing** as its G3. Either is legal;
   silence is not. Its advantage is real: the only keyed seal kit and
   mate machine in the field, ready to stamp archives.
2. **SHIPWRIGHT.** The 9,496 B fixed image is all structure, no
   history — consolidation by recompiling. STIR-09 runs the ask
   backwards: name what the image LOST that a replay phase would have
   kept. Shipwright may find G3 flattering. Book it anyway.
3. **ORGANISM.** Sharpest STIR-09 target: replay is its native tongue;
   the zero-verdict-delta disabler measurement says the Hebbian layer
   needs exactly a scheduled phase to become load-bearing. Book the
   replay clock or concede dormancy is death.
4. **PROCESSION.** Drill history is append-only and unbounded (its own
   W3). Permanent-principles vs. drill-examples is hippocampus-vs.-
   cortex verbatim; the consolidation drill is the incorporation.
5. **DEADBAND.** The deferral queue is the unpriced cold store
   (STIR-08's sharpest cut): deferring is cheap only if redemption is
   O(deferred batch). The floor theorem has a cold-storage loophole
   until retrieval latency is booked.
6. **STREAM — conditional.** Stream has still not delivered a house
   (R3-SCORES §3, stated as fact, no penalty). The conditional stands
   until it docks; a wavefront with no long store has no Seam-2 answer
   at all, and saying so is not a penalty, it is the current record.

Parent books (ledger, deadband trees) ride inside their hybrids; the
entry is the ship that runs.

---

## 7. Constraints (unchanged in substance from Seam 1)

1. **Five-verb law extended, never broken** — new verbs/surfaces (a
   mount verb, an archive seal, a sleep phase) are earned here;
   existing duties (refusal-with-reason, conservation gates, the mate)
   are not relaxed.
2. **One-command run.** `cargo test` / `make`-class single commands,
   no PKI, no network, no manual key ceremony in the default path.
3. **Hot image bounds are booked in bytes** — the stated fixed size or
   the measured O(recent) curve, printed.
4. **No floats decide verdicts.** Integer measurements, integer
   reason codes.
5. **Seam-1 regression tests remain permanent residents** — the keyed
   seal and the mate now apply at the archive layer too. A compound
   that forgets its parents' scars starts the next round already
   broken.

---

*End GAUNTLET-SEAM2 (rev. 2026-08-30). The problem in one line: the
image must forget on purpose, prove what it forgot, and say what that
costs. Undersell, overdeliver.*
