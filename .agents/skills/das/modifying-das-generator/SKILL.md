---
name: modifying-das-generator
description: Use when changing DAS generator behavior, source-shape mechanics, contract validation rules, or generated-output regression tests.
---

# Modifying the DAS generator

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read the **DAS code and coverage map** in project context
and current shape restrictions. Contract authors express source structure;
physical adapters extract it; shared assembly owns generic history. A provider
business rule belongs in neither adapter nor assembly.

## Procedure

1. Reproduce the defect and locate ownership: acquisition value, authored path,
   physical extraction, validator vocabulary, or shared model assembly. Fix only
   the requested owning layer. Record the donor mechanism and adaptations rather
   than porting unrelated provider branches.
2. Capture the base revision, clean generated file set/bytes and compiled graph
   outside managed roots. Declare expected diff classes and invariant outputs.
   Do not stash, reset or overwrite someone else's work to obtain a baseline.
3. Add a focused fixture/test and observe the expected failure before production
   code changes. Vocabulary changes need valid and invalid examples with stable
   rule IDs. List every removed/retained/added ID and each fixture's disposition;
   flip formerly-invalid accepted vocabulary rather than quietly deleting proof.
4. Use the code map: registry for physical defaults, rule collection for allowed
   vocabulary, shared emitter/resolvers for common SQL. Keep full-path child
   resolution, explicit overrides and canonical metadata order intact. Remove
   dead symbols only after per-symbol caller checks, not a file-level guess.
5. Select tests from a coverage matrix for the actual changed mechanism:
   each bound shape, supported and rejected materializations, nested depth and
   repeated modes, filters if touched, composite/nullable keys, replay identity
   and the bound latest/history relationship. Do not import one project's
   incremental rejection or history assembly into another implementation. A gap gets a focused
   test; an unsupported combination gets rejection, not advertised support.
6. Make the narrow change, run focused tests, regenerate and run
   [structural validation](../validating-das-structure/SKILL.md). Compare output
   set and bytes against the saved baseline, normalizing only the predeclared
   substitutions. Unexpected residue is a finding to investigate, not another
   normalization rule. Perform semantic proof separately where values can change.

## Handoff and stop conditions

Deliver ownership/donor decision, fixture/rule ledger, coverage matrix with gaps,
failure-first evidence, classified generated diff and structural/semantic results.
State repair status separately from validation status: a working example is
INCOMPLETE when required regression tests or routed structural checks are missing.
Name each missing check and next action; mark unperformed checks NOT_RUN. Do not
claim missing-value preservation from an untested path or an exception. Without a
tracked baseline, include untracked files and before/after manifests rather than
claiming an empty Git diff proves no changes.
Record untested paths explicitly. Stop if the fix requires provider-specific
business interpretation, unsupported source physics or unreviewed semantic
changes. Narrow the patch instead of refactoring adjacent scheduled-for-deletion
code. New incremental support also needs the separately approved cursor and
target-pruning evidence; a timestamp column alone is not that approval.
