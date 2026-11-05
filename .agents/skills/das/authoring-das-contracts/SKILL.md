---
name: authoring-das-contracts
description: Use when adding or changing a DAS data contract, field description, source path, type, key, model, or materialization declaration.
---

# Authoring DAS contracts

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read **DAS authoring bindings** in project context,
the owning template, actual source schema and relevant payload evidence. Produce
a source-faithful contract and classified generated diff; business interpretation
belongs outside staging even if contract vocabulary could express it.

## Decisions before editing

Record source coordinates/shape, row grain, full key, source-event time, intended
outputs and lifecycle impact. Inspect actual source presence and types; do not
derive paths or units from target names. Child `source_path` stays fully rooted:
inside `settings`, a child is `settings.locale`, not `locale`.

| Decision | Discipline |
|---|---|
| Financial values | Use exact NUMERIC/BIGNUMERIC where supported, not floating approximation |
| Instants | TIMESTAMP; distinguish DATE/DATETIME and make timezone conversion explicit |
| Epoch values | Select seconds/millis/micros from source units; a wrong unit can silently yield the wrong year |
| Optional fields | NULLABLE only for genuine source optionality, never to hide wrong extraction or cast loss |
| Event time | Authored TIMESTAMP-producing expression; do not infer that a bare DATE resolves to TIMESTAMP |
| Lifecycle | Classify additive, breaking, semantic or description-only; use the bound version/validity policy and verify deployment/consumers before an exception |

Descriptions distinguish authoritative meaning from observed open values and
unknowns. Route unknown meanings to the bound **owner-question file**, with a
named answerer. Preserve its questions-only and delete-on-resolution lifecycle;
do not create another question store or present a guessed description as sourced.

## Change and prove

A supported path/type correction works from persisted landing observations through
local validation and generation; provider access, dlt execution and a re-fetch are
not prerequisites. Inspect the physical shape, not the writer's brand.
Missing or corrupted acquisition belongs to ingestion; do not repair it in DAS.

1. Make the smallest contract edit. Check supported type/mode/nesting and
   materialization combinations in the validator, not a donor's larger surface.
2. Enumerate expected file additions/deletions and property/SQL changes before
   regenerating through the bound generation command. Never edit generated SQLX.
3. Run [validating-das-structure](../validating-das-structure/SKILL.md).
   Inspect source declarations, casts, all canonical columns/order, full-PK
   latest ordering and only the expected output changes.
4. For output-set changes, clean generation may leave obsolete committed files.
   Remove an orphan only after all three hold: it is generator-managed (not a
   manual override), a clean generation does not reproduce it, and its deletion
   is user-approved within this PR. Otherwise list it for a scope decision.
5. Path/cast changes need [semantic proof](../validating-das-data/SKILL.md) once
   the relevant read scope is authorized. Compilation cannot prove non-NULL data.

## Handoff

Deliver contract/output paths, field-to-source evidence, lifecycle decision,
classified diff, structural results, semantic results or NOT RUN, owner questions
and unresolved scope. An unexplained generated change or source-present value
lost in projection stops that change; do not compensate with defaults.
