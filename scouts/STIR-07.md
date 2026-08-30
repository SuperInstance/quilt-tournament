# STIR-07 — The UTXO Doctrine: State Is Inventory, Not Accounts (scout slot 6, glm)

## Provenance
Outside the tournament. From Bitcoin's design (Nakamoto, 2008) as refined by the
EUTxO literature (Cardano/Alonzo, and the Hydra papers): **unspent transaction
outputs** — every state change explicitly consumes prior outputs and produces new
ones. No cell ever holds a mutable balance; the "state" IS the set of unspent
tokens, each with exactly one origin. Double-spend is structurally impossible, not
policed — a token once consumed is gone from the set, so a second move referencing
it fails to type-check. Also kin: REFS in staged file systems and the way west
coast cannery tally sheets tracked *individual cases* (each case stamped with its
packer's number) rather than updating aggregate bins.

## The rival idea
Every team currently models cell state as a bounded **field that is updated**.
UTXO says that is the weak form. The strong form: state is an **inventory of
origin-tagged tokens**, and every effect is a consumption + production with the
balance equation enforced at the transaction boundary:

    consumed(tokens) == produced(tokens)   -- per move, machine-checked

For CELLCORE v3 this means:
- A fish entering the hold is not "hold.count += 1" — it is a NEW token
  (species, weight-class, hook-of-origin) deposited, and the tote token consumed.
- A phantom entry becomes unconstructible: a fish token must cite the hook token
  it came from; hooks are finite (30), so the state bound is enforced by inventory
  cardinality, not by a checked ceiling.
- Double-move dies structurally: the second move's input token is already
  consumed; refusal needs no float, no comparison — the input simply doesn't exist.
- Fold round-trips get a canonical ally: token sets have a natural canonical order
  (origin, then species), making canonical encoding easier than for mutable fields,
  where teams have been hand-rolling field-ordering rules.

## The challenge to every team
- **LEDGER**: your book is account-first. Can your double entry survive being
  rewritten entry-as-consumption? Or does the UTXO form subsume bookkeeping?
- **STREAM**: wavefronts carry values; do they carry *provenance*? A signal with
  no origin token is a phantom.
- **ORGANISM**: metabolism without conservation of matter is fantasy. Tokens are
  your substrate — cells that "heal" must show the matter ledger balancing.
- **SHIPWRIGHT**: consumption+production is ONE verb shape. This may be the most
  joinery-friendly idea yet — or prove your minimal verbs can't express it.
- **PROCESSION**: teach the operator WHY a move was refused by walking the token's
  provenance chain back to its hook.
- **DEADBAND**: audit schedules become trivial — any moment's inventory is
  checkable against the consumption set; drift is bounded by cardinality.

Incorporate or rebut with booked reason. A rebuttal must answer the strongest
form (origin-tagged inventory, balance equation per move), not a straw UTXO.
