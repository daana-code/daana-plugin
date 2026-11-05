---
name: developing-landing-adapters
description: Use when implementing or changing a dlt landing adapter, provider acquisition boundary, observation envelope, or landing regression tests.
---

# Developing landing adapters

First read the [project binding procedure](../../shared/references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

Read **Ingestion bindings** in project context,
the active component instructions, provider parser/README and official provider
and pinned dlt documentation for the changed mechanism. Retired ingestion code
is not a template merely because it names the same provider.

## Inputs and decisions

Establish the immediate source, resource grain, supported history/partition
window, pagination/completion signal, source key and duplicate semantics. Decide
acquisition scope separately from destination disposition: reading a full history
does not imply replacing its landing table. Record the complete envelope contract,
observation identity and extraction-versus-load clocks before coding.

## Procedure

1. Preserve the entire provider value, including unknown keys, nested values and
   duplicates. Add technical acquisition context outside it. Do not rename, cast,
   default, enrich or interpret source business fields at landing.
2. Sample aware UTC extraction time when reading the immediate source, including
   each bounded historical acquisition. Never set it to the requested business
   date or parse it from a load ID. Load completion comes from successful load
   metadata; source events remain inside the payload.
3. Use the bound landing interface and its existing identity helper. Where the
   interface preserves nested values as JSON, retain native JSON hints so an
   unfamiliar key cannot create an unintended child table. A custom envelope is
   not dlt's universal output schema. Preserve
   same-acquisition identity and distinguish a fresh read from package recovery.
4. Add credential-free regression cases before changing behavior: full payload
   preservation, pagination completeness, duplicate ordinals, stable identity,
   source-read time, exact schema and nested normalization. Include an optional
   new field and failed acquisition/load boundaries; do not require real secrets.
5. In the fresh-load path, check pending packages before source acquisition and
   require the verified captured
   batch before destination run. Inspect extracted and normalized package IDs;
   `has_pending_data` alone need not cover aborted packages. Do not introduce a
   second recovery ledger or reset pipeline state as an implementation shortcut.
6. Run the bound provider-local tests and complete landing gate. Inspect the
   diff for unintended source selection, disposition or schema changes. Prepare
   live proof using [running-landing-loads](../running-landing-loads/SKILL.md)
   only when required; local implementation does not authorize acquisition.

## Artifact and stops

Deliver adapter/test diff, envelope/schema proof, requested source scope,
clock/identity decisions and local results. List live coverage/reconciliation
as NOT RUN when unavailable. Unknown business meaning is not an adapter rule;
unsupported completeness, identity or destructive-disposition decisions require
owner direction. Continue safe local work rather than requesting a broad load.
