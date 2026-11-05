---
name: authoring-dar-specs
description: Use when translating an approved analytical design into a Daana DAR specification or changing an existing declaration without changing its reviewed business meaning.
---

# Author supported DAR declarations

Read the [project binding procedure](../../shared/references/project-bindings.md),
the task's DAR authoring/compiler bindings and restrictions. For syntax/mechanics
read [Daana DAR](../references/daana-dar.md); for definitions, naming and grain
read the relevant [analytical guidance](../references/analytical-design.md).

## Workflow

1. Identify the approved question/design and affected assets. Confirm grain,
   measures, dimensions, temporal interpretation and runtime requirements.
   Recheck reuse against actual declarations and consumers. Missing meaning
   routes to [elicitation](../eliciting-dar-requirements/SKILL.md); a routine
   technical correction does not restart a settled interview.
2. Resolve canonical definitions, approved fallback and gap owner. Use approved
   analytical requirements for derived measures; report canonical gaps. Undefined
   fields remain proposals, not plausible descriptions inferred from SQL. Continue
   approved independent outputs rather than blocking the whole task.
3. Check active input support, naming policy, executable/schema capability,
   model discovery and workspace. Distinguish fixture-only resolution from the
   actual project. Do not invent a YAML field, model copy or implicit substrate
   repair when the selected compiler cannot preserve the approved semantics.
4. Enumerate expected changes before editing: declarations, generated object set,
   public schema/names, dependencies, semantics and descriptions. Author only
   supported vocabulary; state grain constraints and their verification path.
   An accepted assertion field is not proof of an emitted/running assertion.
5. Apply the bound naming convention. Milestone-resolved values identify their
   milestone or current/latest policy in name, definition and join; an unqualified
   name needs established invariance. Do not import another project's prefixes.
6. Use [structural validation](../validating-dar-structure/SKILL.md): check, lint,
   compile once, inspect the full plan/output and classify every diff. Verify
   actual emitted source/target coordinates, columns and temporal mechanics.
   Never repair generated SQL manually. Proposed orphan removal needs ownership,
   non-reproduction and the project's deletion approval, not a directory cleanup.

## Deliver

Leave declarations and their reviewable generated-output evidence, including the
question-to-output sufficiency argument or a precise compiler/binding gap. Explain
whether the change is ready for local review, semantic verification or an operation;
these are different states. Apply the per-claim
[completion report](../references/analytical-design.md#completion-evidence), with
agent versus owner decisions, unresolved definitions, untested scope and next action.
Compilation is not a deployed-data verdict or permission to publish.
