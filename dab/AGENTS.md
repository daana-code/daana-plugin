# DAB agent instructions

These instructions apply to `dab/`. Read the root [router](../AGENTS.md),
[playbook](../ANALYTICS_PLAYBOOK.md), and task-relevant sections of the
[DAB knowledge map](../.agentic/knowledge/layers/dab.md).

## Meaning before mapping

The reviewed model owns entities, attributes, relationships, definitions and
grain. Mappings own source bindings, expressions and effective-time choices;
the workflow selects mappings and connections own physical coordinates. Change
the owning artifact, never generated SQL or an incidental consumer's definition.

For an explicitly requested first iteration without approved meaning, the existing
model and mapping skills support a source-led candidate from typed sources or
legacy code. Legacy code also uses the
[reconstruction procedure](../.agents/skills/dab/references/legacy-reconstruction.md).
Produce a candidate with documented meaning, observed implementation, inference
and unresolved questions distinguished. Owner absence does not block independent
drafting. Keep a coherent candidate model and mappings outside both the selected
model and runtime workflow; preserve existing approved configuration. An approved
subset does not approve its proposed extensions, and passing checks do not
authorize selecting those extensions. Review/promotion of meaning and authorization of operations remain
separate gates; legacy behavior is evidence, not approval.

Preserve approved meaning when a source is missing. Remove a fake mapping only
within the authorized task, report the missing evidence, and let the concept's
owner decide redefinition, deferral or removal. Do not manufacture a working
mapping with constant NULLs, false filters, invented keys or placeholder tokens.
Continue independent work whose meaning and inputs are established.

A change-only attribute history is not automatically a daily fact series.
Repeated equal observations, flow versus state, grain and time basis must follow
the reviewed question/model, not whatever an available table can express.

## Source and expression boundary

Choose FULL versus FULL_LOG from snapshot versus historical-version semantics
at the declared grain. Incremental additionally needs a proven arrival-monotonic
acquisition axis and verified boundary behavior; a timestamp's name or existence
is not that proof. Do not use business-event time as an acquisition guarantee.

Distinguish sparse-event absence, explicit document clearing, failed casts and
deletion. Do not apply a universal NULL filter or UNKNOWN fallback. Verify the
executing engine's attribute-NULL storage and relationship-NULL behavior
separately before relying on either.

Inspect relationship expressions in their complete generated context: scalar
placement, target types, effective time and combined table/attribute filters.
A focused WHERE-context dry-run is an early check, not proof of the whole action.
Static acceptance of a field does not establish that the generator uses it.

Source preparation belongs to its owning DAS boundary; request a narrow prepared
interface instead of repairing acquisition or generated staging from DAB.
Identity linking, collision handling and reversibility require an explicit
reviewed policy. Before choosing any source, read mandatory **Operational
restrictions** via the root router's Project context binding. A mapping reference
does not override restrictions or meet their reopening conditions.

## Operation boundary

Root rule 3 governs every warehouse write, including retries. Read the bound
operation restrictions and approval authority before preparation. Before presenting
one, verify the client principal, actual artifact hashes, workflow/configuration,
connection/namespace, target state and exact scope. Inspect current CLI support;
do not infer selector semantics from a flag's name or borrow a donor command.

Deploy, execute and destructive refresh/install are different operations.
Prove entity selection and refresh effects in an authorized isolated namespace
before relying on them. Preserve the canonical workflow while lineage behavior
is unverified; do not create a second workflow identity merely to select a subset.
No failure authorizes metadata deletion, truncation, a broader refresh or a
force/automatic-confirmation retry. Stop the affected operation and retain evidence.

## Evidence and completion

State predicted grain, keys, values, timelines, affected pipelines and unchanged
surfaces before execution. Reconcile source, generated base and serving results
at a common observation boundary. Scope checks to the mechanism; record omissions
instead of substituting a fixed query-count checklist.

For an N:1 relationship, prove at most one active target per source at an effective
instant, including same-time ties. Multiple targets across history are not by
themselves a violation. Establish serving/set semantics before interpreting rows.
Check clearing/deletion transitions, duplicate populations and unchanged controls
where relevant. Verify canonical-workflow pipeline completion and window lineage
using metadata semantics established for the actual artifact.

Report three distinct evidence levels: structural validation, synthetic engine
execution/reconciliation, and actual deployment reconciliation. Help text and
source inspection do not prove runtime effects; synthetic success does not prove
production. Missing operational evidence does not prevent local authoring, but it
prevents an operationally verified verdict.

## Local routes

Use `dab_specialist` for scoped DAB work and `data_platform_reviewer` in fresh,
read-only context for independent review. Follow shipped skill links in the root
router when present; do not invent a skill or paste a role to claim native discovery.

Resolve actual gates and CLI commands from **DAB bindings** and **DAB offline
commands and DMDL fields** in project context. A repository gate is not evidence
of Daana execution or data reconciliation. Check prerequisites before
calling it local-only: mapping/schema checks can access the warehouse. No local
gate authorizes cloud access, a write or a merge.
