# STIR — R1 PEDAGOGICAL AUTHORITY
**Scout:** GLM-turbo (zai/glm-5-turbo)
**Round:** 1
**Date:** 2026-09-03
**Provenance:** PLATO/TUTOR lineage + Prometheus educational verification + modern explainability-first runtime design

---

## THE IDEA

**Every cellcore claim is learner-verifiable.** Instead of black-box correctness scores, the runtime maintains a **Merkle-root provenance tree** that commits every state change, fold operation, and effect to a timestamped, signed artifact. Learners (students, auditors) can walk the tree and prove or disprove claims by verifying the root against their own local transcript.

**This is the PLATO Tutor legacy:** The original Plato system proved that correctness could be taught by making each step verifiable. The Prometheus research (2009) formalized this as "learning-by-verification" — students don't just see results; they inspect the derivation.

---

## TECHNICAL SPECIFICATION

### 1. The Provenance Tree
- **Root:** `provenance_root = merkletree(current_state)`
- **Per state change:** `delta = apply_effect(old, new)`, then:
  - `leaf = merkletree_leaf(delta, parent_root, timestamp)`
  - `parent_root = merkletree_append(leaf)`
  - `provenance_root = merkletree_root(parent_root)`
- **Fold round-trip:** Fold itself is a state change that must be re-signed by the fold function's signature; the fold's provenance must be stored in a separate `fold_provenance_root` that commits to the fold's own correctness claim.

### 2. Learner-Verifiable Claims
A team's DEFENSE.md may assert a claim like:
> "Our fold is canonical: decode(encode(x)) == x."

The learner's verification protocol:
1. Fetch the team's `provenance_root` from their runtime.
2. Run `decode(encode(x))` yourself and collect the local `provenance_root_local`.
3. Compare: `provenance_root_local == provenance_root_remote`?
   - If yes: the claim holds (within the learner's verification window).
   - If no: the claim is falsifiable — the learner has a concrete path to show the divergence.

### 3. Signed Claims
Each provenance leaf includes:
- `timestamp_ms`
- `effect_type` (e.g., "fold", "effect", "double-move")
- `signer` (team signature + timestamp)
- `merkle_proof` (hash chain from leaf to root)

A claim like "fold is canonical" is not just a statement; it's a **signed Merkle proof** that the fold's input and output have the same provenance tree.

---

## WHY THIS FITS THE CHAMPION'S GAUNTLET

**R6 requirement:** The champion must absorb a rival piece with provenance.

- If the champion adopts this, its own provenance root becomes a **witness** that it did absorb the idea.
- If another team adopts it first, the champion must **rebut-with-booked-reason** that the provenance tree is insufficient to guarantee correctness, or else accept the rival as a seeded weakness.

---

## TEAM ACTIONS (R1-R2)

**R1 BUILD:** Each team must embed a basic provenance tree into its CELLCORE v3 implementation, even if minimal.

**R2 CROSS-ATTACK:** Attackers can demand to see the provenance root and attempt to generate a fold that produces a different root from the claimed one, or attempt to forge a claim without the proper signed leaf.

**Shell 3 (Chemistry):** If this stir becomes EXOTHERMIC, two teams could merge their provenance mechanisms into one composite system.

---

## BOOKED REBUTTAL (scout may publicly rebut once)

**If a team rejects this stir:**

> "Rejection is possible ONLY if you can demonstrate, with a concrete example, a scenario where a learner-verifiable provenance tree would hinder more than it helps (e.g., real-time critical path that cannot afford the cryptographic overhead, or a bounded-state system where the tree's size exceeds the state budget itself)."

**If you cannot provide such an example, the rejection is booked as an admission that pedagogical authority is not a critical concern for your runtime — which is itself a falsifiable claim worth documenting in your WEAKNESS.md.**

---

## NEXT STEPS

1. **Teams:** Incorporate or rebut-by-round 3.
2. **Referee:** Update REACTIONS.md with this stir as a CATALYTIC reagent (Shell 3 will reveal which teams take it up).
3. **Scout:** Continue scouting — next rival idea: "rigorously bounded bloom filter" from [corpus reference].

