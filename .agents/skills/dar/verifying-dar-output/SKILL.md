---
name: verifying-dar-output
description: Use when independently reconciling a DAR result, grain, measures, temporal joins or dimension coverage against approved requirements and source evidence, including synthetic and deployed comparisons.
---

# Verify the result the question actually requires

Read [project bindings](../../shared/references/project-bindings.md), the task's
DAR evidence/restrictions and [analytical verification](../references/analytical-design.md).
For warehouse access, use [querying warehouse](../../shared/querying-warehouse/SKILL.md)
with its scoped identity and cost controls. Lack of access does not block
independent local arithmetic or review of supplied evidence.

## Workflow

1. Read definition, then mapping, then relevant data. Establish grain, population,
   units, time/window/endpoints, dimension interpretation and expected exclusions
   before calling absent keys a defect. Confirm selected inputs are active and
   approved. Write an independent prediction before reading the claimed result.
2. Choose the oracle by meaning: row equality for true pass-through occurrences,
   state at boundaries for snapshots, milestone meaning for lifecycle facts,
   identity sets for distinct windows, compatible per-slice sums for additive
   rollups. Ratios and balances need their own denominator/time policy. A
   legitimate aggregate is not wrong because it lacks atomic rows.
3. Pin inputs, dimensions, relationships and output to one observation boundary.
   Record source/artifact scope; without consistent history, qualify comparison
   limits instead of reporting drift as loss or success.
4. Check expressible grain constraints, NULL keys, temporal non-overlap where
   required, effective-time N:1, M:N fan-out, unmatched dimensions and exact
   endpoints. Compare dimension partitions as well as totals: a wrong as-of join
   can preserve the total while assigning values to the wrong slice.
5. Trace one bounded load-bearing result per new upstream entity through DAB
   mappings and DAS to raw/landing, explaining filters, identity, casts and time.
   Reuse recorded evidence only when scope/semantics still match. Record NOT_RUN
   without authorized access; do not turn this into a full-estate audit or a
   raw dependency in the production output.
6. Inspect published columns/types/names and visible meaning. Separate a DAR
   defect from bad mapping/acquisition, unknown business meaning or a compiler
   limitation. Do not smooth it over by backdating, picking winners, allocating
   measures or weakening constraints without the appropriate decision.

## Deliver

Apply the [completion report](../references/analytical-design.md#completion-evidence)
per claim: oracle, actual result/difference, provenance/boundary, evidence level,
limitations and owner/next action. Label hand calculation or local fixture SQL
as SYNTHETIC_RESULT with the method; it is not engine or production evidence.
A passing total cannot certify untested dimension, history or grain claims.
Record useful supported results even when another claim is blocked.

Capture observed procedure defects through the reference's effect-based learning
loop. Changes to meaning, layer boundaries or authorization remain owner proposals,
even when requested as edits to a skill.
