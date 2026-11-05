# Warehouse capability checks

Read the task project's **Warehouse bindings**. Select only the relevant backend
section; this reference supplies no client identity, namespace, approval or
runnable project command. Verify capabilities against the selected client/version
and official documentation before relying on them.

## Distinguish the controls

| Need | Establish | Do not substitute |
|---|---|---|
| Syntax/catalog analysis | Whether the exact interface analyzes without executing; what it resolves and what remains unchecked | Fluent SQL, successful generation, or a query-body check for a published object's schema |
| Cost estimate | What input/target work the estimator includes, including views, scripts and cache behavior | Small output, LIMIT, COUNT, or plan cost units presented as billed bytes |
| Execution bound | The enforced limit, its unit and scope; fail before exceeding the approved boundary | A timeout described as a billing cap or an uncapped operation described as capped |
| Stable population | A supported snapshot/transaction or immutable input/load identity, with matching target build provenance | Independently timed reads or an event-date filter on continuously arriving data |
| Pruning | Actual partition/clustering support and the predicates used by the selected engine | A partitioned target assumed to make source reads cheap |
| Read-only effects | Every statement, invoked function and selected client mode | A SELECT prefix, dry-run flag or EXPLAIN spelling assumed safe across engines |

Unavailable controls are findings with explicit alternatives and authority, not
automatically blockers to local reasoning. An engine with no billing concept
does not need fictional billing credentials; its file access, resource scope and
side effects still matter. EXPLAIN ANALYZE commonly executes the query: establish
the actual interface's behavior rather than using it as a universal dry-run.

## BigQuery-specific controls

These apply to BigQuery, not every warehouse. Resolve actual SDK/CLI commands,
credential mechanisms, location and billing project in task context.

- Verify the session principal through the client used for the operation. A
  project flag alone does not select an account. Ambient ADC and gcloud defaults
  do not establish the approved identity.
- Dry-run the exact query with query caching disabled for the estimate. Inspect
  underlying views, script statements and target-side work; script estimates may
  be incomplete. Keep analysis-only requests distinct from billed execution.
- Apply the selected client's maximum-bytes-billed control to authorized SELECTs
  where supported. A wrapper that does not expose it is not capped. Record
  estimated bytes, cache setting, ceiling, job identity, actual processed/billed
  bytes and the affected physical population.
- For snapshot parity, verify table support, history bounds and target build
  provenance. Pin both compared populations consistently; a business-date cutoff
  does not exclude later arrivals for that date. Otherwise report a bounded
  diagnostic, not exact parity.
- A `__NULL__` partition contains null partition values. `__UNPARTITIONED__` can
  contain out-of-range values or transient streamed data; it is not by itself
  proof that the partition policy is absent. Inspect the actual specification.

Official references: [dry-runs and estimates](https://docs.cloud.google.com/bigquery/docs/running-queries#dry-run),
[query cost controls](https://docs.cloud.google.com/bigquery/docs/best-practices-costs),
[partition meanings](https://docs.cloud.google.com/bigquery/docs/partitioned-tables),
[write-optimized storage](https://docs.cloud.google.com/bigquery/docs/querying-partitioned-tables#query_data_in_the_write-optimized_storage),
[historical reads](https://docs.cloud.google.com/bigquery/docs/access-historical-data).

## SQL examples and real execution

Reusable SQL illustrations use a portable standard subset and carry
**Dialect: ANSI SQL — illustrative**. Resolve their example objects before use.
If a backend-only mechanism has no portable expression, explain its required
behavior in prose, then inspect the bound tool; do not invent ANSI syntax.

Translate into the actual dialect without changing meaning, including row
multiplicity, NULLs, numeric precision, time zones and interval endpoints. Test
results against an independent oracle. Actual test/project SQL names its real
dialect and evidence scope; generated SQL remains generator-owned. A local result
does not establish another backend's behavior or any deployed-data claim.
