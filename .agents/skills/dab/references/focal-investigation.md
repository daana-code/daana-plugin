# Physical DAB investigation: resolve before interpreting

A Focal-style engine can separate identifier bindings, attribute descriptions,
relationship storage, serving views and execution metadata. These are conceptual
roles, not guaranteed table/column names. Use bound artifact hashes, generator
mode, actual schema and generated SQL to locate them. Current/latest filtering,
tie order, NULL/row-status semantics and refresh behavior are version-scoped.

## Evidence chain

| Start | Resolve through the actual schema |
|---|---|
| Business attribute or relationship | Model definition and authored source expression/filter |
| Physical type/context key | Metadata that names the concept; opaque keys are not self-describing |
| Base observation | Business identifiers, effective time, knowledge/version time, value, row status and producer instance where available |
| Producer instance | Process/procedure identity, workflow identity, status and input window |
| Executed procedure | Captured SQL/configuration and its predicates, tied to that run/artifact |
| Serving result | Generated selection/compaction semantics, not an assumed one-row-per-pair view |

Do not use a fixed surrogate-key decoding algorithm or import an identifier-table
layout. Preserve many-to-one and one-to-many metadata joins where present and
report unresolved lineage. Keep sensitive payloads and procedure text out of git;
use bounded aggregates/redacted evidence under the project's read policy.

## Clocks and multiplicity

Effective time concerns business validity; version/knowledge time concerns when a
fact became known to this system. Establish actual column semantics and retained
history. A first-seen stamp is not automatically business creation. Equal values
at two times may be legitimate history, while identical effective/value tuples
from two run instances may be replay/lineage duplication. Serving compaction can
make both situations look identical in a latest view.

Dialect: ANSI SQL — illustrative; translate only after resolving the bound schema
and backend. This is a multiplicity diagnostic, not a project command:

```sql
SELECT entity_key, effective_time, value, COUNT(*) AS occurrences
FROM supplied_history
GROUP BY entity_key, effective_time, value
HAVING COUNT(*) > 1;
```

That result is a population to investigate, not proof that every repeated row is
wrong. Join it to producing instances and completed workflow/procedure windows;
then compare canonical and alternate paths and their actual SQL. Status meanings
and numeric versus NULL windows must come from the selected strategy/artifact.

A read-only diagnosis ends with evidence and a bounded handoff. Recovery requires
the operation workflow's backups, exact scope and fresh authority; metadata
deletion and a fresh database are never automatic duplicate remedies.
