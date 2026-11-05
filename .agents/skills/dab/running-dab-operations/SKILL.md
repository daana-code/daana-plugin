---
name: running-dab-operations
description: Use when preparing, executing, refreshing, or recovering a Daana DAB workflow or deployment, including scoped operations and lineage investigation.
---

# Running DAB operations

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

## Inputs and classification

Read **Coordinates and identity**, **Operational restrictions**, and
**DAB evidence qualifications and refresh scope** in project context, resolving
the selected tool's credentials before operation-packet preparation.
Identify the exact outer/inner artifacts, generator mode, configuration revision,
canonical workflow path/id and each connection namespace. Version text, selectors
and a flag named dry-run do not establish behavior or a read-only boundary.

Classify deploy, ordinary execute, refresh level or install. Derive refresh scope
from the actual invocation and generated behavior, not the selected entity's name.
Read the artifact's model-level (no entity), entity-level and any attribute-level
evidence separately; do not extrapolate one tested level to another.

## Preparation packet

1. Inventory target/base/serving tables, distinct physical relationship tables,
   pipeline metadata and concurrent writers. Preserve canonical workflow identity;
   a second identity or same-id trimmed workflow is not a harmless selector.
2. Before refresh, include a recoverable metadata table snapshot plus appropriate
   affected-data backups, destination, retention and restore procedure in the
   authorization packet. Snapshot creation is a write too. Capture baseline rows,
   base multiplicities, serving fingerprints and version timestamps; identify
   incoming relationships from non-refreshed entities as well as outgoing tables.
3. Write a prediction artifact before execution: per source/pipeline, strategy,
   watermark semantics/current value, pending row count and maximum acquisition
   stamp, expected window/end, expected changed keys/rows/totals and unchanged
   controls. Use authorized bounded queries or explicitly label supplied evidence.
   Unknown live values remain prerequisites, not invented numbers.
4. Present exact binary/command, workflow path/id, connections, scope, cost,
   backups and confirmation mechanism for fresh authorization. State metadata
   deletion scope and whole-workflow follow-on effects. Route untested selection
   or attribute-refresh behavior to focused evidence, not a production experiment.

## Execute and reconcile

After authorization, perform only the approved operation, retaining jobs, principal,
timestamps and results. Do not treat `--dry-run` as a safety barrier where evidence
shows it can write. A failure ends the affected operation: no automatic confirmation,
retry, broader refresh, metadata deletion or repaired configuration rerun.

Use [verifying-dab-output](../verifying-dab-output/SKILL.md). Compare actual jobs,
inserted rows and source/base/serving data to predictions. Reconcile canonical
completed pipeline rows and procedure identity; for watermarked strategies verify
windows against prior completions and detect unplanned epoch restarts. Do not
impose numeric-window continuity on strategies with legitimate NULL audit windows.
Verify incoming and outgoing relationship effects independently; the refresh's
deletion selection and its following execution need not share the same scope.

## Artifact and stops

Deliver preparation packet, prediction artifact and, only if run, append-only
execution/reconciliation record using the
[completion report](../references/completion-report.md).
Unexpected lineage, scope, NULL behavior or count/key changes stop acceptance and
require a named decision. Preparation-only tasks end with execution NOT RUN; they
do not need a warehouse experiment to count as useful completion.
