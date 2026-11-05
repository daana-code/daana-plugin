---
name: authoring-dab-mappings
description: Use when binding reviewed DAB meaning or a labelled source-led candidate to source evidence, authoring mapping YAML, or changing source strategy and effective-time expressions.
---

# Authoring DAB mappings

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.
Read [Daana authoring mechanics](../references/daana-authoring.md) for field
placement and check boundaries; bind applicability to the selected compiler.

## Inputs and decisions

Read the approved model (or explicitly labelled source-led candidate), source-support matrix, DAS contracts/schema and
**DAB bindings** in project context.
For a candidate reconstructed from legacy dbt/Dataform code, first read
[legacy reconstruction](../references/legacy-reconstruction.md). Draft supported
bindings alongside the model; preserve observed filters separately from proposed
semantic changes. Lack of owner approval blocks promotion, not candidate authoring.
The same boundary applies to drafts from typed tables without legacy code:
keep candidate model and mapping files together outside the selected model and
workflow. Run checks on their explicit paths. Do not select unapproved mappings
or extend the active model to satisfy a workflow check; report active coverage
separately. A validation request is not approval of the proposed business meaning.
Before writing expressions, establish whether the source is active and approved:
graph type, dependencies, guards, tags and actual materialization evidence. A
parked view remains unavailable even when its definition compiles. With supplied
synthetic input, label that scope rather than claiming a live interface exists.
Local candidate mappings may refer to declared inputs, labelled unverified and
excluded from the selected workflow. An unavailable input cannot support a ready
or executable verdict; partial mappings remain explicitly incomplete.

For each table record key/row grain, strategy, acquisition boundary, entity and
attribute effective times, filters, NULL meaning and relationship target type.

## Procedure

When a foreign key moves to a physical link table, preserve the approved conceptual
relationship. Inspect effective-time cardinality, target identity, interval endpoints
and source support, then rebind through the selected compiler's supported fields.
A relationship-only source may have no attributes; do not invent one to carry it.
Several targets over history do not imply M:N. Overlapping targets under an N:1
definition are a source/mapping finding or owner question, not permission to change
the model. Report proposed YAML separately from generated/executed evidence.

1. Choose `primary_keys` and mapping-group `allow_multiple_identifiers` from
   the reviewed identity, not available columns. Multiple identifiers teach
   identity; they are not equivalent to a compound business key.
2. Choose `ingestion_strategy` from snapshot versus historical-log semantics.
   Consider incremental only after proving a usable acquisition axis, delivery/
   replay behavior and the artifact's watermark predicate. An extraction timestamp
   is a candidate, not proof against delayed loads or equal-boundary arrivals.
   Without a safe axis, author the supported nonincremental strategy; do not stop
   all mapping work or smuggle in an event-time lookback.
3. Write `entity_effective_timestamp_expression` and, where the model enables it,
   `attribute_effective_timestamp_expression`. Supply `batch_expression` only for
   the strategy and proven boundary that actually use it. Verify units/types.
4. Evaluate each changed expression on supplied representative rows or authorized
   source queries; record values, exclusions and NULL cases. Distinguish table
   `where` from attribute `where`; inspect their combined generated placement where
   artifacts are available, otherwise record that omission. Classify source absence,
   explicit clearing, cast-loss and deletion
   per attribute. Use the **DAB evidence qualifications and refresh scope** in project context
   before claiming how NULLs become stored history or relationship changes.
5. Keep relationship target expressions scalar and type-matched to identifiers.
   Check their WHERE context as well as SELECT under the approved query protocol.
   Request a prepared interface from the owning layer for missing preparation,
   naming grain, columns and clocks; do not put an analytic expression in a
   generated scalar context or edit generated staging to make it work.
6. Run the bound offline `check model`, `check mapping --skip-schema-validation`
   and `check workflow` without `--source`. Connected checks are separate.
   Inspect output, not only validation: type-mismatched relationship targets,
   analytic targets in WHERE, unknown ignored fields and table-level relationship
   stanzas can evade static checks on affected compilers. Inspect the bound
   compiler's evidence for each; do not convert a source-level caution into an
   executed proof. Use its supported relationship location.
   Save and inspect stdout and stderr, including warnings, as well as exit codes.
   If workflow validation needs a candidate selector, keep it beside the draft
   and clearly unselected. No candidate check authorizes deploy or execute.

## Artifact and stops

Deliver mapping/workflow diff, source-to-output expectations including absent
rows, and the [completion report](../references/completion-report.md).
Static-only success says "Static checks passed; executability not established."
Missing source/owner meaning gets a narrow handoff, not a fake mapping. Remove an
authorized placeholder while preserving the approved concept for its owner's
decision. Do not deploy or refresh to obtain evidence for a local-only task.
