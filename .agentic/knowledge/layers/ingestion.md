# Ingestion knowledge map

Ingestion preserves source observations without interpreting them:

```text
source / managed transfer -> acquisition adapter -> source-faithful landing
```

Provider adapters own resource requests, windows, pagination/partition traversal,
retry-stable observation identity and safe provenance. They preserve complete
source values. Contract-driven unpacking and renaming begin in DAS, not here.

Business-event time, immediate-source extraction time and successful warehouse
load time are separate clocks. Resolve the actual columns and lineage join from
**Ingestion bindings** via the task repository's root Project context binding.
A custom envelope, append policy or JSON normalization choice is an implementation
contract, not a universal property of dlt.

Local schema/tests do not authorize provider reads, warehouse reads, recovery or
landing writes. Durable state is part of recoverability: inspect pending extracted,
normalized and abort-marked packages before fresh acquisition. A persisted
package retry and a new source read have different identity and authorization.

## Implementation lookup

Project context binds active components, provider parsers/READMEs, identity/schema
helpers, lifecycle behavior, state, exact commands, coverage and local gates.
Read mandatory **Operational restrictions** before selecting a source; retained
legacy code is not an active extension point. Read the selected authoritative
component instead of copying its instructions into this map.
