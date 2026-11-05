---
name: validating-das-data
description: Use when investigating DAS mapped values, source-present NULL loss, keys, latest winners, parity, or deployed table and partition behavior.
---

# Validating DAS data

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read **DAS authoring bindings** in project context
and use [querying-warehouse](../../shared/querying-warehouse/SKILL.md) for any cloud
inspection. Start with the changed mechanism and a prediction, not a blanket
column scan. Local synthetic evidence remains useful when live reads are unavailable.

## Establish a comparable population

Pin both paths to **one input snapshot** before any source/staging parity claim.
For live views, evaluate the reviewed projection over physical inputs at the same
AS OF instant as the source oracle; preserve the projection and record the query
as diagnostic, not deployed-output proof. A logical view is not itself a time-
travel table. Verify actual source support and retention before promising AS OF.

For materialized staging, use its recorded input snapshot/completed-load boundary,
and pin the target state representing that build. Using the same wall-clock AS OF
on two tables built at different times does not align their input populations.
An event-time cutoff alone is insufficient under late arrivals. Without build
provenance, limit the result to a bounded investigation and request a reproducible
comparison; do not label a racing count comparison exact parity.

## Check the changed mechanism

- Schema: reconcile paths/types and actual table/view type with contracts.
  Contract REQUIRED is asserted behavior, not proof of physical CTAS nullability.
- Loss: count `source IS NOT NULL AND projected IS NULL`, separating absence,
  explicit JSON null, empty value, parse failure and bad path. Parse both numeric
  sides into the intended type; do not compare floating renderings as strings.
  For money compare typed sums at the documented smallest unit and grain.
- Arrays/records: compare presence and element counts, inspect mixed element
  types, nested depth and timestamp formats. A nonempty parent proves no child.
- Keys/history: null keys, full composite grain, duplicate multiplicities,
  replay identity; re-rank under the exact event-time/tiebreaker ordering and
  delete policy, count winner changes and ties. Compare matched populations,
  not just totals.
- Physical policy: inspect partition spec, clustering and pruning estimates.
  `__NULL__` warrants investigation of null partition values; `__UNPARTITIONED__`
  can mean out-of-range values or streaming storage. Neither alone proves the
  spec is absent. Inspect object metadata and representative predicates.

## Interpret, then hand off

For independently acquired snapshots, reconcile history against the sum of actual
batch populations, preserving observation identities and multiplicity. Batch sizes
can vary: batch count × latest row count is not a historical oracle. Compare latest
separately at its declared key/winner grain. Observation-level sums are parity
checks, not automatically additive business measures. If persisted landing has the
missing observations, localize the loss to projection/history before requesting
another source fetch.

| Symptom | Hypotheses to test, not automatic diagnoses |
|---|---|
| Latest duplicates | Incomplete key, failed ranking, join fan-out; MERGE-key mismatch only if a MERGE exists |
| Stale acquisition maximum | Quiet/failed source, sentinel clock, stale build or cursor exclusion |
| Zero first-build rows | Empty source, narrow filter, wrong input or omitted action |

Return boundary, queries/jobs or synthetic inputs, expected/actual aggregates,
loss/duplicate/winner findings and not-tested list. Source-present projection loss
stops acceptance of that mapping; NULLABLE/defaults are not repairs. Report
out-of-scope acquisition/business defects to their owner without fixing them here.
