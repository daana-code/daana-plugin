---
name: eliciting-dar-requirements
description: Use when a reviewed business question needs a DAR fact grain, dimensions, temporal interpretation, reuse decision or runtime metric design, before choosing compiler output kinds.
---

# Elicit an answerable analytical design

Read the [binding procedure](../../shared/references/project-bindings.md), then
the task's DAR authoring and Agile Analytics bindings. Use the approved question,
model, prior answers and the existing design/review artifacts. Read
[analytical design](../references/analytical-design.md) for the decisions below.

## Workflow

1. Restate the decision, intended population and what an answer must distinguish.
   Separate DAB conceptual completeness from DAR analytical answerability.
   Return missing reusable meaning to its owner rather than inventing it in a fact.
2. Inspect definitions, then mappings, then relevant data. Check active support
   and restrictions before selecting sources. Investigate technical facts instead
   of asking the analyst to choose enums or explain inspectable columns.
3. Inventory existing facts, dimensions and relationships. Compare grain,
   population, definition, time, dimension variant, coverage and retained detail.
   Prefer sufficient reuse or a compatible bounded extension; state the unmet
   requirement before proposing a new output.
4. Settle one-row meaning and its testable constraint, including key/NULL policy
   and temporal uniqueness. Distinguish occurrences from restatements; history
   counts do not define grain. An unassertable grain is a finding, not permission
   to synthesize a key, arbitrary winner or DISTINCT away ambiguity.
5. Decide fact/dimension column roles, observed-history versus latest attributes,
   relationship cardinality/mutability and as-of policy. Inspect tracking-start
   evidence without assuming first-observed values held earlier. Label approved
   imputation; do not backdate to hide missing joins.
6. Decide stored measures/detail versus runtime calculations. Preserve identities
   when configurable distinct windows need them. For fixed slices and genuinely
   additive measures, justify and deliver the sufficient rollup; unrequested
   flexibility is not a reason to escalate or demand atomic retention.
7. Ask the fewest unresolved owner questions, one understandable question at a
   time, using examples and counterexamples. Reuse accepted answers. Present
   one coherent design checkpoint, not a mandatory questionnaire.

## Deliver

Use the existing analytical artifact to record reuse/extension/new-output choice,
assertable grain, analytical pattern, dimensions, temporal semantics and endpoints,
population, measures/units/additivity, runtime recipe and sufficient retained
detail. Explain how these answer the question or its atomic components. State
unsupported uses without blocking the approved use.

Apply [completion evidence](../references/analytical-design.md#completion-evidence):
per-claim evidence levels, agent versus owner decisions, omissions and next step.
Once meaning is approved, hand off to
[spec authoring](../authoring-dar-specs/SKILL.md). A technical correction with
unchanged meaning does not require reopening the interview.
