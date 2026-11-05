---
name: validating-das-structure
description: Use when checking DAS contracts, generated drift, Dataform compilation, or BigQuery SQL analysis before a PR or operation.
---

# Validating DAS structure

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read the **DAS commands and credential mechanisms** in project context.
Report the two lanes separately; local success never implies cloud analysis or
mapped-data correctness.

## Lane A: credential-free local checks

1. Record revision/worktree status and changed scope. Run the bound contract,
   generator drift, compile and integration gates; do not regenerate as a
   diagnostic step that masks drift.
2. Inspect missing, extra and byte-changed managed files. The file-set comparison
   matters as much as bytes. Classify intended changes, preserve handwritten
   files, and route orphan deletion through contract-authoring authorization.
3. Capture compiled JSON once for the configuration. Check compiler exit status,
   errors, named expected actions, query/config and dependency targets. Inspect
   more of the saved graph without recompiling. Refresh capture after inputs change.

Stop this lane on failed checks, unexplained output or absent expected actions.
Missing credentials do not block it. Deliver logs and graph evidence even if the
cloud lane is unavailable.

## Lane B: credentialed, read-only cloud analysis

1. Use [querying-warehouse](../../shared/querying-warehouse/SKILL.md) and verify the
   actual client principal. Obtain the authorized analysis scope; identify the
   script's credentials and query inventory before invocation.
2. Run the bound dry-run lane or approved exact compiled queries against live
   dependencies. Separate PASS, named missing-relation GAP, SQL/permission
   FAILURE and NOT ANALYZED. A first missing dependency can hide later errors;
   a gap is not an implicit pass or permission to build its dependency.
3. Independently classify each result's origin: introduced, pre-existing or
   unknown. If needed, analyze an isolated base revision with the same client,
   snapshot/settings and query inventory; compare failure lists. Use a separate
   worktree/export, not stash/pop of shared user files. Changing warehouse state
   between runs limits causal attribution and must be disclosed.
4. Report expected gaps by exact relation and dependent, distinct inventory,
   other failures and exit status. Nonzero-with-reviewed-gaps is a precise
   incomplete result, not a green whole-graph verdict. Do not replace missing
   relations with an invented SQL inliner.

Stop on unapproved external scope, wrong principal, new unexplained errors or
gaps outside the reviewed inventory. Do not repair pre-existing failures inside
an unrelated PR; disclose them.

## Handoff

Produce revision/configuration, local results, graph checks, cloud result/origin
matrix and omissions. State what compilation cannot prove: JSON path presence,
cast survival, historical coverage, physical target state or latest winners.
Use [validating-das-data](../validating-das-data/SKILL.md) for that separate work.
