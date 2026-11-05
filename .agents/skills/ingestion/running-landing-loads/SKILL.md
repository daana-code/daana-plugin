---
name: running-landing-loads
description: Use when preparing, running, or recovering a dlt landing load, historical backfill, or persisted pending load package.
---

# Running landing loads

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read **Coordinates and identity**, **Operational restrictions**, and
**Ingestion bindings** in project context, then the selected provider's current
parser/README. This workflow distinguishes
provider acquisition, pending-package recovery and warehouse validation.

## Prepare

1. Identify provider/resource, immediate source, exact API dates or physical
   partitions, expected row grain/coverage and destination. Verify parser support:
   some providers traverse all historical instances and have no date selector.
   Do not invent flags or assume every script's `--help` avoids external work.
2. For recovery and fresh loads alike, verify principal/project/location through
   the credential mechanism the writer actually uses. Resolve destination,
   pipeline identity, `pipelines_dir` and `working_dir`.
   Verify durability; a variable setting or customary directory is not the resolved
   path. Inventory extracted, normalized and abort-marked packages without printing
   customer state or secrets. Check whether multiple writers share this queue.
3. If packages exist, prepare **recovery**, naming exactly those package IDs.
   Use the existing no-source resume path: `pipeline.run()` without fresh data.
   Never combine resume with a new resource/window. A successful resume does not
   prove the newly requested history was acquired. Non-resumable/aborted state
   needs inspection, not automatic abort/drop/reset or directory deletion.
4. If the queue is clear, prepare **fresh acquisition**. Pin client identity,
   project/location, durable state, source window, append/other reviewed disposition
   and expected load/package count. Recheck the queue immediately before running.
   Re-reading the source creates new acquisition observations, not a package retry.
5. Match the exact fresh authorization already given in this session, or request
   the missing scope. Fresh acquisition names source read, landing write and
   verification; recovery names pending-package writes/verification and performs
   no new provider read. Include commands and expected coverage/cost; provider API
   reads and billed queries are not covered by local-test permission.

## Execute and reconcile

After authorization, use only the reviewed invocation. Record returned package
IDs, completed/failed jobs and remaining queue. Recovery must account for all and
only the authorized pending IDs; fresh acquisition must identify its own new load.
Stop on extra IDs, partial failure, changed source boundary or an unexpected queue.

Verify schema/native JSON and no unintended child tables. Left-join observations
to successful load metadata so unmatched IDs stay visible; require zero
unmatched IDs. Compare captured/landed counts, multiplicities, source keys, history
coverage and provider-specific reconciliation under the approved read budget.
An empty source window needs separate coverage evidence, not a fictional row.

Deliver an operation record: authorization, commands, identity/destination/state,
windows or package IDs, actual completion, aggregates and omissions. No failure
authorizes re-extraction, replace/merge, broader history or a state reset. If only
preparation is authorized, the complete packet is the output; mark loads NOT RUN.
