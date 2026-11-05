---
name: verifying-dab-output
description: Use when checking DAB source-to-base-to-serving results, timelines, flow totals, relationship cardinality, duplicates, or post-operation reconciliation.
---

# Verifying DAB output

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

## Inputs and independent prediction

Read model meaning/grain, mapping expressions, DAS contracts and supplied or
authorized source evidence through **DAB bindings** in project context.
Derive expected keys, values, effective timelines and cardinality independently.
The implementer's prediction file is a comparison input, not independent evidence.
For a review, use fresh read-only context and retain that distinction in the report.

## Mechanism-scoped procedure

1. Name the changed mechanism and its evidence level. Read actual serving SQL
   and the **DAB evidence qualifications and refresh scope** in project context:
   latest/as-of ordering, equal-value history compaction, relationship latest sets,
   ties and atomic NULL handling are not interchangeable. Do not import one donor
   artifact's semantics as a release-wide guarantee.
2. Establish one comparable observation boundary across source, base and serving.
   Use frozen supplied rows or reproducible physical snapshots/build provenance.
   A reporting-date cutoff does not freeze late arrivals. Use
   [querying-warehouse](../../shared/querying-warehouse/SKILL.md) for authorized cloud
   work; otherwise complete local derivation and state live reconciliation NOT RUN.
3. Compare full key sets and base-row multiplicities, not just counts or distinct
   keys. A serving view can hide duplicate base rows. Compare serving value/time
   fingerprints too; an unchanged fingerprint alone does not prove the base or
   metadata was repaired. Exclude only explicitly understood technical timestamps.
4. Derive effective transitions, same-time ties, repeated equal observations,
   clearing/deletion and unmatched relationships. A missing all-NULL atomic row
   and a NULL member in an otherwise populated group are different cases. Check
   the tested strategy/load phase before judging expected absence or clearing.
5. For N:1, reconstruct active target sets at an effective instant, including
   tied targets; multiple targets over all history are not themselves a violation.
   After an entity rebuild inspect incoming relationships from other entities and
   outgoing ones, including dangling identifiers and changed surrogate bindings.
6. For daily flows, reconcile every required day including zero/equal-value days
   and totals at the approved grain. Never sum a compacted change-only history
   as though it were a complete daily series.
7. For operations, inspect completed rows under canonical workflow/procedure
   identity and the established window semantics. Compare before/after rows and
   oldest version stamp for refresh characterization. Unexpected workflow identity
   or epoch starts need investigation; multiple workflow IDs alone do not prove
   duplicate data. State unchanged controls and all untested mechanisms.

## Artifact and stops

For a mapping replacement, compare historical key/time/value multisets as well as
latest outputs at the same boundary. Equal current values can conceal changed
earlier versions; bidirectional set differences alone can conceal multiplicity.
Classify the changed population and owning expression before choosing a remedy.
Neither latest equality nor a nonzero historical difference establishes incremental
safety or authorizes a full refresh.

Deliver findings by severity with queries/input artifacts, expected/actual values,
mechanism and affected scope, using the
[completion report](../references/completion-report.md).
Separate structural, synthetic-engine and deployment verdicts. Report substantive
YAML/source defects even when the task never executes an engine. A failed invariant
does not authorize a data repair, identity merge, deletion or broader refresh.
