---
name: investigating-dab-lineage
description: Use when tracing DAB physical rows, hidden duplicates, effective/version history or unexpected processing windows to the producing pipeline and workflow using metadata.
---

# Trace a DAB observation to its producer

Read [project bindings](../../shared/references/project-bindings.md), **DAB
bindings**, **DAB evidence qualifications and refresh scope**, **Analytics
consumption and diagnostic bindings**, and the
[Focal investigation reference](../references/focal-investigation.md).
Resolve the actual artifact/mode and physical schema. No donor's table names,
opaque-key interpretation or serving policy is a universal engine contract.

## Procedure

1. State the symptom, semantic attribute/relationship, observation boundary and
   independent expected population. Establish what source, base and serving rows
   mean before comparing them. Read definition, mapping, metadata and generated
   serving behavior; a compacted serving result can hide extra base observations.
2. Count key/time/value multiplicities in base and serving, preserving duplicates.
   Identify the precise excess or changed population, not just an aggregate
   difference. Distinguish legitimate versions/compaction from repeated identical
   observations; exclude technical columns only with an explicit reason.
   Report both row counts and, where meaningful, typed value totals as diagnostic
   checksums. A sum across stored versions is not itself a business measure.
3. Resolve physical type/context keys through actual metadata to model meaning.
   Follow each relevant row's producing instance key to its process/pipeline,
   workflow identity, completion status, input window and captured procedure SQL
   where available. Record every branch of the implicated lineage, not just the
   suspicious one. A missing join is a finding, not a guessed identifier.
4. Compare the canonical lineage with the alternatives. Test whether an unexpected
   epoch window overlaps already processed observations; correlate the duplicate
   population, instance/version stamps and procedure predicates. Multiple workflow
   IDs alone do not prove a fork. A supplied export can support a diagnosis, but
   cannot prove a real engine reproduced the failure under a particular command.
5. Bound the next diagnostic or repair handoff. Check affected incoming and outgoing
   relationships, metadata ownership, backup/recovery needs and artifact-specific
   refresh scope through [running DAB operations](../running-dab-operations/SKILL.md).
   Do not execute a refresh, delete history, invent a new workflow selector or
   treat a flag named dry-run as permission to experiment.

## Completion

Use the [DAB report](../references/completion-report.md): affected tuples/counts,
both concrete lineage paths, metadata/SQL evidence, cause versus hypothesis,
business impact and smallest next step. Label local fixture calculation
SYNTHETIC_RESULT and explicitly not synthetic *engine* execution; retain separate
STRUCTURAL/DEPLOYED_DATA claims and NOT_RUN checks. Distinguish agent conclusions
from owner authority. Independently verify any proposed repair before accepting
it; this diagnostic workflow grants no repair authorization.
