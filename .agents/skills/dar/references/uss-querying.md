# Querying a Unified Star Schema output

This reference applies only when the bound approved output is USS. A compiler's
support for USS does not make every output USS; flat facts, snapshots and other
patterns retain their own consumption contract. Inspect the actual generated
schema and publication metadata for the selected artifact, not a donor's names.

## Establish the measure's owner and usable slices

Resolve measure meaning, units, owner entity/grain, aggregation, query-at guidance,
sliceability, related dimension entity and any required temporal policy. Metadata
field names such as owner_entity, query_at or is_sliceable are examples of
concepts to resolve, not required portable column names. Missing metadata is a
scoped support gap, not permission to infer joins from similar identifiers.

A UNION-style bridge may contain rows for several owners. Measures/counts can be
populated only on their owner branch while unrelated owner rows carry NULL.
COUNT(*) over the whole bridge is therefore not an entity count. Use the declared
count measure or owner-grain key population and prove uniqueness for the selected
slice. SUM of an additive measure is valid only when joins/branches preserve that
measure's multiplicity; neither a measure name nor a bridge guarantees this.

## Missing versus inapplicable

Inspect the bound sentinel values and semantics; do not assume literal names.
An inapplicable key on an unrelated branch and an unresolved key on the correct
branch represent different populations. Exclude both from a *known-identity*
distinct count, but retain unresolved-owner amounts when the approved total
includes them. Report unknown coverage separately. A sentinel filter suitable for
a dimension count can silently discard valid money if reused as a whole-row filter.

## Query and reconcile

- Confirm each requested dimension is supported at the measure's grain. An
  unsupported slice needs a targeted handoff, not a guessed cross-owner join.
- Calculate identity-distinct metrics over the requested window. Daily distincts
  need not add to a longer-window distinct.
- Verify temporal semantics in the actual serving output. A latest-only bridge
  does not answer a historical knowledge-time question.
- Check total and slice partitions plus owner counts/keys. Measure any fan-out
  before aggregating. No DISTINCT, arbitrary winner or allocation to hide it.

Return the resolved metadata, calculation and coverage with the consumer skill's
per-claim evidence labels. Reading metadata proves declared support; numerical
results and deployed behavior require their own evidence.
