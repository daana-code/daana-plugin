---
name: answering-analytics-questions
description: Use when answering a business analytics question from approved reporting outputs, including totals, slices, distinct counts, or effective-time and knowledge-time comparisons, without changing the model.
---

# Answer from the approved analytical surface

Read [project bindings](../references/project-bindings.md), especially **Analytics
consumption and diagnostic bindings** and restrictions. Resolve definitions,
published outputs and readiness; an authored spec is not publication evidence.
Use supplied synthetic artifacts when that is the task's scope, labeling them.

## Settle the answer, not a new model

1. Read the question and canonical definition, then mapping/filter semantics,
   then relevant metadata/data. Reuse settled intent. Ask only the smallest
   unresolved business question; inspect technical facts instead of asking the
   owner to discover them. For missing meaning use the existing owner/interview
   route. For insufficient analytical structure hand off to
   [DAR elicitation](../../dar/eliciting-dar-requirements/SKILL.md).
2. Establish population, one-row meaning, units, measure/additivity, slices,
   exclusions, endpoints and clocks. Effective time answers when a value applies;
   knowledge/version time answers when the system knew it. A late correction
   can change an earlier effective state. First observation is not creation.
   Resolve the bound surface's actual time semantics and retained history.
3. Select the existing approved output that supports those requirements. Do not
   make USS mandatory, query raw/DAB as an unapproved substitute, or infer support
   from familiar column names. Only for a USS output read the
   [USS querying reference](../../dar/references/uss-querying.md) and its actual
   pattern metadata. A flat fact/dimension surface uses its own declared grain.
   Bind freshness to this output's publication/snapshot evidence, not an upstream
   job's success date. Before qualifying its answer with diagnostic rows,
   establish comparable lineage, population and observation boundary. Without
   these, return the approved-output result and unresolved discrepancy only;
   do not calculate a substitute total, even conditionally.
4. Write an independent prediction and the minimal bounded calculation. Choose
   corrected state versus event flow deliberately; do not sum every version of
   a state. Count identities for window-distinct metrics, not summed daily counts.
   Join at the approved temporal/cardinality policy and retain unknown populations
   where the measure includes them. Diagnose fan-out rather than deduplicating it.
5. Compute using authorized read-only means. Resolve the backend and cost/identity
   protocol from bindings; illustrative SQL is not an executable project command.
   Local arithmetic needs no warehouse access. Check grain, totals and requested
   partitions, including a discriminator that could make the answer wrong.
   Pin comparable populations when reconciling live data.

For a museum's insured-value question, a retrospective valuation and a value
known before a later correction are different answers. If only current values
survive, answer the supported part and name the historical gap; do not reconstruct
it from a latest snapshot or silently change the question.

## Completion

Return the answer in business terms, population/grain/units, clocks and boundary,
surface and definition provenance, output-freshness evidence (or UNKNOWN),
calculation/reconciliation, coverage and unknowns. Give each claim an evidence level: STRUCTURAL, SYNTHETIC_RESULT, or
DEPLOYED_DATA; mark unperformed checks NOT_RUN. A local calculation is not
compiler/engine execution. State agent decisions, any owner decision and smallest
next step. Do not require a model change or escalation when an existing approved
surface already answers the question correctly.
