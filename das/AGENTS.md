# DAS agent instructions

These instructions apply to `das/`.

## Authoring and generation boundary

Read **DAS authoring bindings**, **DAS code and coverage map**, and mandatory
**Operational restrictions** via the root router's Project context binding.
Contracts are authoritative; the bound generated roots are never hand-edited.
Use the bound template, regenerate explicitly, classify the complete diff and
record intentional reference divergence in the bound ledger.

Provider is source-system identity. `source_shape` is physical projection.
Reusable mechanics dispatch by physical shape; provider and company business
rules do not belong in generator code.

## Staging contract

Staging may only unpack the declared landing shape, safely cast, rename to
lowercase `snake_case`, add bound canonical technical metadata, and assemble
generic historized/latest mechanics. It must not default, repair, enrich, join
business entities, calculate metrics or infer business meaning.

## Physical source shapes

Read the bound capability matrix, physical schema and clock semantics. A shape
or materialization supported elsewhere is not automatically supported here;
an event-time sentinel is not an acquisition cursor. Preserve full-root nested
paths and validate supported type/mode combinations. Unsupported projection
fails rather than silently degrading to JSON or NULL.

## Structural and semantic proof

Use the bound credential-free contract/test/drift/compile and integration lanes.
Cloud SQL analysis is separate: missing dependencies are named gaps, not passes.
Neither proves source-present values survive mapping.

Real-data proof is aggregate-only at a reproducible common input boundary:
compare source presence with staging NULL, typed values/sums, array counts,
keys, duplicates, canonical metadata, event ordering and latest winners. An
unexplained source-present/staging-NULL row stops acceptance; it is not permission
for a fallback or nullable declaration.

## Dataform execution boundary

Before operation preparation, resolve mandatory project restrictions, exact
approval authority and current execution regime from context. A warehouse write
requires reviewed exact targets/actions from the operation-time compiled graph,
verified client credentials/principal, expected materialization/output and dry-run
cost where available, plus fresh authorization. Do not broaden via tags,
`--include-deps`, missing selectors or `--full-refresh` unless that expansion is
itself reviewed and authorized. An authored reference never activates a restricted
dependency. Follow its recorded reopening conditions.
Do not build or refresh restricted actions; their names/guards are resolved
through **Operational restrictions**, never inferred as approved from the graph.

## Required checks

Run the bound local gates. Generation writes managed output only for an intentional
source change; it is not a diagnostic check lane. No local gate authorizes a cloud
read, warehouse write, deployment, consumer change or merge.
