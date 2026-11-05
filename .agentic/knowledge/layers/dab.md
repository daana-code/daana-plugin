# DAB knowledge map

DAB integrates source evidence into reviewed, reusable business concepts. Start
with the [architecture](../../../ARCHITECTURE.md) and
[playbook](../../../ANALYTICS_PLAYBOOK.md); mandatory constraints live in
[`dab/AGENTS.md`](../../../dab/AGENTS.md), not this optional map.

## Artifact ownership

| Question | Read the owner |
|---|---|
| What does this concept mean, and at what grain? | Bound business model and reviewed question evidence |
| Which values and time expressions implement it? | Bound authored mappings and DAS contracts |
| Which mappings run under which identity? | Bound workflow |
| Which namespaces and connections are selected? | Bound connections and exact invocation |
| Which question needs the concept? | Bound question register |
| Who owns a prepared interface? | DAS boundary and its bound source contracts |
| Which checks actually exist? | Bound command/gate owners |

Resolve these through **DAB bindings** in the task repository's Project context.

Authored configuration is not a deployed inventory. Compare it with the target
and execution record before operating; legacy coordinates in a checked-out file
are not permission to create or use that estate. Daana's internal staging and
metadata namespaces are not DAS staging. Resolve each connection field separately.

Existing mappings are evidence to inspect, not automatically good templates.
In particular, an unresolved source, a false-filter placeholder or a reference
to a restricted action does not establish a usable capability. Follow mandatory **Operational restrictions** in project context before source
selection; a mapping reference cannot override them.

## Source clocks and strategy

FULL and FULL_LOG express different source histories: a current snapshot and a
sequence of historical observations are not interchangeable. Determine the
entity grain, each source row's meaning and effective-time semantics before
choosing a strategy. Verify the selected engine's implementation rather than
inferring behavior from a mode name.

Incremental processing needs an acquisition boundary that arriving observations
cannot fall behind. A valid event timestamp can be arbitrarily late at landing.
Even a watermark advanced only over observed data does not capture a later row
whose timestamp is below that watermark. Read the bound DAS physical-source and clock semantics before treating a
canonical metadata column as a cursor guarantee.

Deleting NULL observations can erase real clearing transitions. Conversely,
preserving an unmapped/cast-failed NULL can invent one. Compare source presence,
typed projection and attribute history, and examine relationship target handling
independently. A table filter and an attribute filter may enter different SQL
branches; prove that the intended exclusion survives the actual generated query.

## Generated relationships and filters

Read complete generated SQL/DDL, not just validate output or a SELECT fragment.
Record key types, scalar expression placement, time expressions, combined filters
and target resolution. An expression that works in SELECT may be invalid in the
generator's WHERE context; dry-run that context and then the full action under
the approved read protocol. Unknown accepted YAML fields may be ignored rather
than supported; inspect whether they influence output.

For N:1, count active targets per source at a common effective instant, including
ties. Do not count distinct targets over all history and call that cardinality.
Likewise, do not assume a serving relation contains only one row per historical
pair: establish the engine's latest-set/history behavior first.

## History and operation verification

For physical-row-to-workflow diagnosis, use
[investigating DAB lineage](../../../.agents/skills/dab/investigating-dab-lineage/SKILL.md)
and its artifact-scoped reference. Keep general cross-layer triage in the shared
diagnostic workflow; do not duplicate physical metadata recipes here.

Write predictions before execution: expected keys, grain, values, additive totals
where meaningful, clearing/deletion transitions and unchanged controls. Reconcile
source, base and serving data against the same observation boundary. A count can
match while keys or timelines are wrong; repeated equal daily measures can vanish
from a change-only history without violating its storage rules.

Deploy creates structure; execute processes data. Whether a new attribute's first
execute backfills, and what a scoped refresh removes, are artifact-specific claims
to test. Record rows before/after, oldest post-run `ver_tmstp`, generated statements
and exact pipeline windows. Counts alone cannot distinguish retained history from
clear-and-re-emission. Confirm the metadata column meanings before using them.

Once established, check a `row_st = 'C'` completion for every affected pipeline
under the canonical `workflow_num_id`, alongside procedure identity and window
boundaries. Completions only under another workflow identity are a lineage warning;
multiple IDs alone do not prove duplicate data. Compare duplicate populations and
load/version stamps before proposing a repair. No diagnostic recipe grants repair
authority, and no new workflow is a harmless selector until that behavior is proven.

Use the smallest checks that exercise the changed mechanism. Record what was not
tested. Structural, synthetic-engine and actual-deployment evidence are separate
levels; report each rather than promoting one to another.

## Engine evidence and re-verification

Resolve the dated inventory through **DAB evidence qualifications and refresh
scope** in project context. Record observation date, full executable/image hash
(including embedded engine/override), generator mode, configuration revision,
command, result and omissions. Empty development version stamps do not identify
an executable. Re-verify the affected mechanism when any of those inputs or source
semantics change; one local candidate does not establish another deployment.

Keep source inspection, synthetic execution and actual deployment reconciliation
separate. Incident counts and workarounds stay in their evidence records, not
evergreen business definitions. A reported defect has its own scope/owner;
instruction maintenance does not authorize its repair.
