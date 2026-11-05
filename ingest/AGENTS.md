# Ingestion agent instructions

These instructions apply to `ingest/`. Read the more specific instruction file
before changing a nested active component.

## Boundary

Ingestion acquires source observations and lands source-faithful evidence. It
owns provider access, request windows, extraction state, observation identity,
and landing schemas. It does not own source interpretation, business entities,
metrics, or presentation.

## Routing

Read **Ingestion bindings** and mandatory **Operational restrictions** through
the root router's Project context binding before choosing a component. Current
component routes are repository scaffolding, not portable provider defaults.

- Find active component paths and acquisition tools in **Ingestion bindings**;
  read their nearest instructions and the
  [Ingestion knowledge map](../.agentic/knowledge/layers/ingestion.md).
- Resolve retired or frozen components through **Operational restrictions**;
  their presence is not an active flow or implementation template.
- An `ingest/` directory does not itself establish an implemented adapter. Read
  the bound documentation and establish support before changing a component.
- DAB and DAR concerns route back through
  [`ANALYTICS_PLAYBOOK.md`](../ANALYTICS_PLAYBOOK.md), not into landing.

## Hard constraints

- Preserve complete provider values. Do not rename, default, repair, enrich, or
  interpret provider fields in landing.
- Keep provider/resource identity, source endpoint or key, historical window,
  and provenance explicit.
- Distinguish business-event time, source-read time, and warehouse-load time.
- Use lowercase source-system datasets and reviewed pipeline identities; do not
  group unrelated sources because their products look similar.
- Keep credentials and signed URLs out of code, metadata, fixtures, logs, and
  commits.
- External reads and landing writes are separate authorization boundaries.

## Proof floor

Add or update provider-scoped, credential-free tests and run the bound landing
gate. Local schema and envelope proof does not authorize a
provider read or BigQuery write. Live work requires fresh exact authorization
and post-load source, row-count, schema, lineage, and coverage reconciliation.
