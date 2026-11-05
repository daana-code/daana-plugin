---
name: running-dar-operations
description: Use when preparing, executing, retrying or reconciling a Daana DAR warehouse operation after analytical meaning is approved. Local-only check, lint and compile use structural validation instead.
---

# Prepare the exact operation, then respect its gate

Read the [binding procedure](../../shared/references/project-bindings.md), root
authorization rules and the task's operational restrictions, identity, DAR
compiler/operation bindings and dated evidence. Read
[Daana command effects](../references/daana-dar.md). A previous approval or proof
is not authority for another run.

## Prepare

1. Identify the approved spec and question, affected objects/dependencies,
   outer/inner executable identity, config, invocation principal, connection,
   namespace and selected catalog/install mode. Check support against current
   evidence, not a local source checkout's promise. Missing or parked inputs
   block the affected operation, not independent authoring.
2. Capture the candidate plan once through the permitted lane. Inspect every
   resolved source/target coordinate and object type, public schema, temporal
   mechanics and proposed change. Workspace names are not proof of emitted
   coordinates. A command that reads a catalog is not credential-free merely
   because it is called compile or delegates to an inner executable.
3. Derive exact command and scope from the selected artifact's help and task
   bindings. Confirm effects, including metadata writes and replace/create
   behavior. Do not assume `--dry-run` is safe, a reset is a prerequisite fix,
   or a retry is automatically idempotent.
4. Prepare an inspectable packet: artifact/spec/plan identities, exact invocation,
   resolved principal/connection/targets, baseline and preservation evidence,
   expected schema/grain/measure changes, predictions, read/cost estimates and
   their limits, stop conditions, recovery and post-run checks. Separate missing
   prerequisites from completed local work. A fictional packet or unresolved
   identity is not an executable real-project approval request.

## Authorization and execution

Present the exact packet to the bound authority and wait for fresh approval.
Do not change machine defaults or copy credentials into the repository. The
approval covers only that command/scope; a changed plan or artifact needs its
applicable renewed review. Install/reset, historical refresh, retry or rollback
is not silently included. If effects or recovery are unclear, stop before writing.

Once separately authorized, record the approval, timestamp, command and actual
result in the bound operation record. Execute only the reviewed scope. A failure
does not authorize an automatic rerun or expanded repair.

## Reconcile and report

After any executed run, inspect actual objects and schemas, required constraints,
grain, temporal coverage, dimension partitions and pattern-appropriate measures
using [output verification](../verifying-dar-output/SKILL.md). Compare with the
pre-run predictions and disclose anomalies before another operation.

Use the [per-claim completion report](../references/analytical-design.md#completion-evidence).
State prepared versus executed explicitly, actual evidence/omissions and the
smallest next action. A successful local plan does not prove ledger readiness,
deployed data or authorization to publish.
