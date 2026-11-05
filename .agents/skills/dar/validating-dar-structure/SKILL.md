---
name: validating-dar-structure
description: Use when checking DAR declarations, local generated SQL or dependency/schema readiness, including cases where a successful compile may conceal missing deployed columns or invalid published object shape.
---

# Validate DAR structure without overstating it

Read [project bindings](../../shared/references/project-bindings.md) and
[Daana DAR command boundaries](../references/daana-dar.md). Resolve the selected
artifact, config, layout and restrictions before choosing a lane.

## Lane 1: local, credential-free

1. Establish the baseline, expected diff classes and approved design. Run the
   bound shape/graph check, lint and offline compile, capturing exits and complete
   output. Compile once per candidate/configuration to a fresh output path.
2. Inspect all published objects and dependency closure: actual source/target
   coordinates, expected columns/types/names, grain-sensitive joins, order/ties,
   interval endpoints, descriptions and whether declared checks are emitted.
   Do not accept an unclassified large diff as mechanical.
3. Compare pre-existing versus introduced failures using isolated baseline
   evidence. Disclose pre-existing issues without expanding the PR to fix them
   or stashing another person's changes. Missing local model binding is a
   finding; a co-located fixture pass does not certify the real layout.

## Lane 2: connected catalog resolution

Only with resolved identity/access and the applicable read authority, use the
selected compiler's catalog path. Verify invocation-specific principal and
targets; do not change shared defaults. Record this separately from offline
compilation. A named but absent/parked input is not ready merely because declared.
Do not repair missing substrate by install/reset or a model relocation.

## Lane 3: warehouse SQL and published shape

Prepare or perform the permitted analysis using the shared
[warehouse workflow](../../shared/querying-warehouse/SKILL.md), preserving its cost
and authorization rules. Compare referenced columns against current catalog
evidence. A query-body dry-run does not prove CREATE VIEW accepts its output
schema: inspect duplicate aliases and object restrictions explicitly. Do not
quietly create an object to prove a read-only claim.

Classify each check as pass, named missing dependency, not analyzed/not run, or
failure; distinguish introduced from pre-existing issues. Missing credentials
stop only connected lanes; offline work should still finish.

## Deliver

Use the [per-claim report](../references/analytical-design.md#completion-evidence):
commands/artifact and invocation context, saved plan, changed objects, actual
passes/findings, omissions and next action. Catalog-shaped synthetic input is not
DEPLOYED_DATA. No syntax/compile green proves business meaning, history, values
or grain; hand those claims to [result verification](../verifying-dar-output/SKILL.md).
