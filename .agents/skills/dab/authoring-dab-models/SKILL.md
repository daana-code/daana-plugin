---
name: authoring-dab-models
description: Use when authoring DAB business entities, attributes, relationships, identity or time definitions, or drafting a first candidate from typed sources or legacy dbt/Dataform code without a business owner present.
---

# Authoring DAB models

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.
Read [Daana authoring mechanics](../references/daana-authoring.md) for field
choices and validate its applicability against the bound compiler.

## Inputs and decisions

Choose the mode from the task: **governed authoring** starts from approved
meaning; **source-led candidate** drafts from available source/schema evidence
when explicitly requested without approved meaning. Legacy dbt/Dataform
reconstruction is one such case; for it, also read
[legacy reconstruction](../references/legacy-reconstruction.md). Use this
workflow together with the mapping skill. Do not demand an interview before
drafting, or present candidate decisions as owner-approved. The identity/grain
approval gates below govern promotion, not the ability to propose alternatives.
Existing approved entities do not approve proposed additions. Keep the coherent
candidate model and mappings in a separate draft location, outside the selected
model and workflow. Validate those draft paths explicitly; do not add candidates
to active configuration merely to make its checks green. Promotion is a separate
owner decision, even when all checks pass.

Read the **DAB bindings** in project context,
approved question and definitions (or available definitions for a candidate), relevant DAS contracts and supplied source
evidence. Build a source-support matrix: concept, one-row meaning, candidate input,
key, time basis, coverage and gaps. A file in the graph is not proof of an active,
approved input. Preserve meaning when evidence is missing.

Write decisions before YAML: entity grain/identity; attributes and definitions;
relationships with N:1 cardinality at an effective instant; event, acquisition
or reporting-day time; deletion/clearing semantics. Identity policy, redefinition
and a changed analytical grain belong to the model owner, not an inferred mapping.

## Procedure

1. Make the smallest model change supported by that matrix. Decide each
   attribute's `type` using the supported DMDL vocabulary; use an explicit numeric
   1/0 definition for boolean concepts where BOOLEAN is unsupported, not a new type.
2. Decide `effective_timestamp` explicitly for the changed attribute: is its
   history timed independently of entity time? Check the
   **DAB offline commands and DMDL fields** binding for selected capabilities;
   the package reference explains companion timestamps and checker requirements.
   Do not copy a
   neighbor's false value or a donor's blanket true policy. For `group`, check
   at-most-one-member-per-storage-type and author time on the parent, not children.
3. Record `allow_multiple_identifiers` as a mapping-group decision if needed;
   it is not a model-field or compound-key shortcut. Require the approved policy
   for collisions, historical ordering and reversibility before linking identities.
4. Distinguish state history from daily flow. A campaign-keyed entity with day as
   effective time is a change-history design; repeated equal days may disappear.
   A campaign-day key preserves each day, including zero, but changes grain.
   Present both with the required reconstruction semantics; only the owner chooses
   a different grain. Do not silently manufacture a daily concept.
5. Run the bound offline model check against the intended model path, then hand affected time/type/identity choices
   to [authoring-dab-mappings](../authoring-dab-mappings/SKILL.md). Source/schema
   inspection may support local authoring without any engine execution. A new
   attribute requires deploy to establish structure before first execute; whether
   that execute backfills is artifact-specific, not automatic full-refresh grounds.
   Use a newly allocated task-local scratch directory if needed, never clear a
   guessed shared temporary path. Capture and inspect command output and errors,
   not only exit codes; retain warnings in the completion report.

## Artifact and stops

Deliver model YAML/diff, source-support matrix and the bound
[completion report](../references/completion-report.md):
files, agent decisions, owner requests, structural/synthetic/deployment evidence
and not-tested list. An unsupported concept gets a specific evidence/owner request,
not a constant-NULL mapping or quiet redefinition. Continue independent supported
changes; a correctly scoped decision request can complete the blocked portion.
