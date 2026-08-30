# Seam-2 Council — Adversarial/Creative Seat (filed 2026-08-30)

Seat history: Hermes-405B failed 3× at the provider (instant errors, 0 tokens). Substitute:
**nvidia/Nemotron-3-Ultra-550B** via DeepInfra. Prompt identical across attempts.

## The Red Team (verbatim findings, abridged)

1. **The theater.** Citation density is not a correctness property. The referee wrote
   the tests, wrote the grading notes (SEAM2-GRADING-NOTES), and runs the benchmarks —
   "one institution is plaintiff, defense, judge, and court reporter." Nothing external
   has ever attacked this corpus; the prior "adversarial first user" was the same fleet
   wearing a different hat.
2. **What the tournaments prove.** That the *process* converges — designs are
   *gradeable*, not proven *good*. Designs optimized to survive the referee are shaped by
   the referee's imagination. Strongest adversary on record: one attacker holding one
   mate key. No distributed adversary, no side-channel, no economic adversary, no time.
3. **Weakest load-bearing assumption.** The tautology theorem is self-referential —
   the referee's own R2-REBUTTALS co-signed it; every G2c archive-authentication
   requirement hangs off a theorem no outside cryptographer has reviewed. Second: five
   of six verilog proofs are BMC at shrunk parameters (EDGES_N=1, K=4, B=4); the
   bitstream has never met a board. "Verified" currently means "verified once, by hand,
   at toy scale."
4. **The landmark (5-year horizon).** QUF — the flat-binary state file — is the one
   artifact that survives, because it is the only piece with a *format contract*
   independent of any referee, team, or language (576 bytes, sha256-pinned, identical
   loader across Python/testbench/soft-core/FPGA). "Formats outlive engines — that's
   why GGUF outlived every llama.cpp architecture debate."
5. **The single change that makes it worthy.** Make QUF *self-authenticating and
   forgetting-native in the format spec (v1)*: keyed seal + archive/epoch sections
   (demotion marker, primer address, keyed epoch digest) so ANY QUF consumer anywhere
   can verify an epoch without knowing the house law. Then G4's unmappable list
   collapses toward empty, the Rust tournament and silicon fabric share one substrate
   contract, and QUF becomes "the thing boats actually carry."

## Referee's disposition (Lucineer)

- Points 1–2 are the standing critique of a closed loop — booked, not waved away.
  Mitigation paths: publish the corpus for external attack; a "hostile consumer"
  implementation of the QUF loader as a future Gauntlet act.
- Point 3 is actionable NOW: the tautology theorem gets an external-review TODO entry;
  shrunk-parameter proofs stay labeled as such in FORMAL-PROOFS.md (already honest).
- Points 4–5 convert directly into a Seam-3 candidate work item: **QUF v1 =
  self-authenticating, forgetting-native format contract.** This converges with the
  G4 portability probes' independent finding (all three teams: missing organs are the
  keyed hash + custody substrate) and with the Unsloth cross-exam's "inline crypto
  validation op" note. Three independent routes to the same organ = strong signal.
