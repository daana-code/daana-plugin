---
name: running-dataform-actions
description: Use when preparing, executing, retrying, or verifying an explicitly scoped Dataform materialization or rebuild.
---

# Running Dataform actions

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read **Coordinates and identity**, **Operational restrictions**, and
**DAS commands and credential mechanisms** in project context.
With those bindings resolved, preparation can finish without execution.
Prior review, yesterday's run and a successful dry-run do not authorize a write.

## Prepare the operation packet

1. Record revision, installed CLI, target project/location, actual principal and
   credential mechanism. A `--credentials` descriptor can still rely on ADC;
   verify that path rather than assuming the file selects an account.
2. Capture one compiled graph. Read exact action/assertion names, dependencies,
   materializations and protected flags from it. Inspect `preOps`, `postOps` and
   applicable `incrementalQuery` variants too: the SELECT is not the whole run.
   Resolve each selector to its
   intended target. No wildcard, tags or dependency/dependent expansion unless
   the added actions are explicitly in the reviewed scope.
3. Inspect target existence/schema and build order. Dry-run the identical
   compiled SELECTs under [querying-warehouse](../../shared/querying-warehouse/SKILL.md).
   Include assertion cost. An assertion reading an absent target needs a reviewed
   create-then-analyze sequence; do not claim it passed before creation.
4. Classify ordinary build versus refresh/recreation. Schema changes on existing
   incrementals, view-to-incremental transitions, partition-policy changes and
   history re-bootstrap can require a fresh rebuild design. Verify the actual
   engine/target requirement; knowing the trigger is not authorization, and a
   refresh flag may not implement a partition-spec change safely.
5. Present exact command, selectors, credentials path without secrets, estimates,
   expected rows/types/partitions, assertions, parity boundary, unchanged controls
   and retry/rollback limits. State execution-cap support honestly: a dry-run
   estimate is not a hard run cap. Obtain fresh authorization for this packet.

## Execute and verify after authorization

Run only the approved invocation. Save timestamps, jobs, action results and
processed/billed bytes. On failure stop the affected operation and preserve
evidence; do not broaden selection or turn a retry into an automatic full refresh.
An idempotent operation still requires the repository's authorization for a rerun.

After **every** run, verify target/schema, materialization and partition/cluster
policy, assertion emptiness, and source-to-output reconciliation using
[validating-das-data](../validating-das-data/SKILL.md). Inspect protected and
unchanged surfaces. A CLI success without those checks is an executed operation
awaiting validation, not accepted data.

Deliver the approved packet plus append-only execution/reconciliation evidence,
deviations and omissions. If only preparation was requested or authorized, deliver
the concrete packet and mark execution NOT RUN; do not ask for incidental writes
merely to finish the documentation.
