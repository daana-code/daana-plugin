---
name: diagnosing-data-pipelines
description: Use when an analytics pipeline fails or layers disagree and the task is to locate the owning boundary, explain the evidence, and prepare a safe next step rather than perform recovery.
---

# Locate the failure without expanding the operation

Read [project bindings](../references/project-bindings.md), **Analytics consumption
and diagnostic bindings**, restrictions and the affected layer instructions.
Resolve the actual workflow/recipe, invocation, target, backend and evidence scope.
A command with a familiar name is not a verified recovery procedure.

## Investigation

1. Preserve the failure, timestamp/run identity, exit status, logs and last known
   successful boundary. Distinguish a failed connection/permission/catalog check
   from a successfully checked absent relation. A locked local database does not
   prove the pipeline's tables are missing.
2. Read the recipe and current supplied/authorized state before proposing another
   run. Identify concurrency, credential, source/schema, projection, model/mapping,
   generation, execution and serving boundaries. Test the cheapest discriminating
   hypothesis first; do not run the whole stack to find where it breaks.
3. Compare adjacent boundaries at one reproducible population: acquired batches,
   persisted landing, projection, DAB base/serving and analytical output as relevant.
   The first demonstrated divergence localizes investigation; it is not itself
   proof of root cause. Equal final totals can hide wrong keys, history or slices.
   A successful downstream check cannot certify upstream acquisition.
4. Route the finding to its existing workflow:
   [DAS mapping proof](../../das/validating-das-data/SKILL.md),
   [DAB verification](../../dab/verifying-dab-output/SKILL.md),
   [DAB lineage](../../dab/investigating-dab-lineage/SKILL.md), or
   [DAR verification](../../dar/verifying-dar-output/SKILL.md).
   For source acquisition use the ingestion workflow. Preserve approved business
   meaning; a NULL or empty result may reflect semantics, filtering, unavailable
   input or failure, so inspect evidence before choosing a fix.
5. Separate diagnosis from intervention. A database lock requires identification
   and coordination with the writer's owner, not killing its process. Inspect what
   a proposed fresh/reset recipe deletes, whether other work depends on it and
   whether backups exist. Never retry, delete files/WAL, reset metadata, change
   client defaults or broaden selectors on the strength of a failure.

## Completion and repair handoff

Report symptom, supplied versus newly observed evidence, hypotheses tested,
demonstrated boundary/cause, business impact, remaining uncertainty and smallest
next check. Label each claim STRUCTURAL, SYNTHETIC_RESULT or DEPLOYED_DATA, with
NOT_RUN checks separate. Record agent conclusions and owner decisions distinctly.
When the cause is known, name the owning layer and scoped proposed repair; hand
writes to its operation workflow for a fresh exact authorization. Diagnosis may
complete without execution, and a useful supported result should not be blocked
by an unrelated missing credential.
