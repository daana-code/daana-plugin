---
name: querying-warehouse
description: Use when preparing or performing warehouse inspection, SQL analysis, profiling, or source-to-output reconciliation across data-platform layers.
---

# Querying a warehouse

First read the [project binding procedure](../references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read **Coordinates and identity**, **Operational restrictions**, and
**Warehouse bindings** in project context, plus applicable layer rules. Consult
[capability-specific controls](../references/warehouse-capabilities.md) for the
selected backend; no backend supplies every control by default.

## Procedure

1. State the question, required relations/columns, population boundary and the
   smallest discriminating aggregate using supplied/local evidence first.
2. Resolve the actual backend, dialect, client and target. For remote access,
   verify the approved principal through that client and bind its namespace,
   location and billing context where applicable. For local evidence, verify
   the selected file/artifact and access mode instead. Do not borrow credentials,
   switch shared defaults or demand cloud identity for a local-only task.
3. Separate metadata inspection, non-executing analysis, data reads and mutation.
   Establish read scope and cost/resource limits before access. Inspect schema,
   object types and dependencies before scanning. No authority for the scan?
   Finish query/estimate preparation and report the unexecuted part.
4. Translate illustrative ANSI SQL into the bound dialect, preserving grain,
   multiplicity, NULLs, precision, time zones and interval boundaries. Validate
   the exact query through the supported non-executing path; estimate cost where
   possible. Inspect scripts and function effects: a SELECT prefix or EXPLAIN
   label alone is not a read-only guarantee. Trace views to physical inputs;
   small results, COUNT and LIMIT do not establish a small scan. Sampling is
   non-exhaustive evidence.
5. Execute only the authorized query with supported enforceable limits. Record
   missing controls explicitly; if a required estimate or ceiling is unavailable,
   stop that execution and request a reviewed alternative. Never invent a hard
   cap or silently replace one with a timeout. Stop on unexplained dependencies
   or an estimate outside the agreed budget.
6. For parity, compare one fixed population. Pin supported physical reads to a
   shared snapshot and apply the same selection on both paths; a business-date
   cutoff alone does not exclude later arrivals for that date. An existing target
   needs matching build provenance. No reproducible common boundary means a
   limited diagnostic, not an exact parity verdict.

## Evidence artifact

Record query/hash, backend/version/dialect, invocation identity or local artifact,
target, population boundary, analysis result, available estimate/limits, execution
IDs and measured cost where supplied. Mark unavailable controls and unrun checks;
syntax success is not result proof. Return aggregates and interpretation, keeping
personal rows and credentials out of committed evidence. Distinguish metadata,
sampled, synthetic and deployed results per claim.

On a permission error do not report absence. On a mismatch retain the original
query and investigate scope, source semantics and mapping separately. Never
change data, expand a budget or add a fallback merely to obtain a matching total.
