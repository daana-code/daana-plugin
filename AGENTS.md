# AGENTS.md

Shared entrypoint for agents working in an analytical stack. This file is an
index, not a manual. The task repository's root `AGENTS.md` binds this collection
and its own Project context. Read the nearest task-layer instructions before
changing that layer, then use the task routing below. Relative links in this
shared file resolve within the complete collection, not to a company's runtime.

For initial orientation, read [ARCHITECTURE.md](ARCHITECTURE.md): layer purposes,
artifact ownership, tool boundaries, and the distinction between source evidence
and business meaning. The [playbook](ANALYTICS_PLAYBOOK.md) owns the working method.

## Repository in one paragraph

This analytical stack has four layers. Ingestion acquires source observations into
landing. DAS makes that evidence typed, source-faithful, and structurally
usable. DAB owns reviewed business meaning. DAR owns outputs for a specific
question or decision. Fix a defect in the layer that owns it; do not conceal it
in a downstream layer.

## Project context

**Project context:** follow the explicit binding in the **task repository's root
`AGENTS.md`**, not this shared collection's checkout. No populated project context
ships in the collection. This binding is independent of where skills are installed.
Read its relevant sections for actual paths, commands, client identity, approval
authority, capabilities and evidence. Before preparing work on an affected source
or any external operation, read **Operational restrictions** there. Those
restrictions are mandatory, not optional background. Missing bindings block the
affected decision/operation, not independent local work; never guess another
project's defaults. Context indexes configuration; it does not replace it.

## Layer routing

| Layer | Read first | Explanatory context |
|---|---|---|
| Ingestion | [`ingest/AGENTS.md`](ingest/AGENTS.md) | [Ingestion knowledge](.agentic/knowledge/layers/ingestion.md) |
| DAS | [`das/AGENTS.md`](das/AGENTS.md) | [DAS knowledge](.agentic/knowledge/layers/das.md) |
| DAB | [`dab/AGENTS.md`](dab/AGENTS.md) | [DAB knowledge](.agentic/knowledge/layers/dab.md) |
| DAR | [`dar/AGENTS.md`](dar/AGENTS.md) | [DAR knowledge](.agentic/knowledge/layers/dar.md) |

## Task routing

Before answering or acting on an intent that matches a shipped skill row, read
that linked `SKILL.md` completely and explicitly state that you are using it.
Do not rely on the skill name or summary alone.

When a client exposes a skill through a directory symlink, resolve the skill
file's canonical filesystem path before following its relative links. Native
discovery aliases can be flatter than the package: their apparent parent is not
the reference directory. Project context still comes from this task repository.

| Intent | Route |
|---|---|
| Interview a business owner, clarify an analytics question, or facilitate an Agile Analytics loop | [facilitating-agile-analytics](.agents/skills/shared/facilitating-agile-analytics/SKILL.md) |
| Inspect or query a warehouse in any layer | [querying-warehouse](.agents/skills/shared/querying-warehouse/SKILL.md) |
| Answer a business question from approved reporting outputs | [answering-analytics-questions](.agents/skills/shared/answering-analytics-questions/SKILL.md) |
| Locate a failed pipeline's cause or reconcile a cross-layer discrepancy | [diagnosing-data-pipelines](.agents/skills/shared/diagnosing-data-pipelines/SKILL.md) |
| Add/change source acquisition or a landing adapter | [developing-landing-adapters](.agents/skills/ingestion/developing-landing-adapters/SKILL.md) |
| Backfill, load or recover pending landing packages | [running-landing-loads](.agents/skills/ingestion/running-landing-loads/SKILL.md) |
| Author or amend a DAS contract | [authoring-das-contracts](.agents/skills/das/authoring-das-contracts/SKILL.md) |
| Change DAS generation or validator vocabulary | [modifying-das-generator](.agents/skills/das/modifying-das-generator/SKILL.md) |
| Validate DAS locally or analyze compiled SQL | [validating-das-structure](.agents/skills/das/validating-das-structure/SKILL.md) |
| Prove DAS mapping, NULL-loss, keys or deployed parity | [validating-das-data](.agents/skills/das/validating-das-data/SKILL.md) |
| Prepare/run/retry a Dataform action | [running-dataform-actions](.agents/skills/das/running-dataform-actions/SKILL.md) |
| Author a DAB concept, or draft a candidate from typed sources or legacy dbt/Dataform code | [authoring-dab-models](.agents/skills/dab/authoring-dab-models/SKILL.md) |
| Bind reviewed DAB meaning or a labelled source-led candidate to source evidence | [authoring-dab-mappings](.agents/skills/dab/authoring-dab-mappings/SKILL.md) |
| Prepare/run/reconcile a Daana DAB operation | [running-dab-operations](.agents/skills/dab/running-dab-operations/SKILL.md) |
| Independently verify DAB source/base/serving results | [verifying-dab-output](.agents/skills/dab/verifying-dab-output/SKILL.md) |
| Trace DAB observations or hidden duplicates through execution metadata | [investigating-dab-lineage](.agents/skills/dab/investigating-dab-lineage/SKILL.md) |
| Settle a question's analytical grain, dimensions, reuse or runtime metric | [eliciting-dar-requirements](.agents/skills/dar/eliciting-dar-requirements/SKILL.md) |
| Author a supported DAR declaration from approved meaning | [authoring-dar-specs](.agents/skills/dar/authoring-dar-specs/SKILL.md) |
| Check DAR declarations, generated plans or schema readiness | [validating-dar-structure](.agents/skills/dar/validating-dar-structure/SKILL.md) |
| Independently reconcile DAR results and temporal/grain behavior | [verifying-dar-output](.agents/skills/dar/verifying-dar-output/SKILL.md) |
| Prepare/run/retry a Daana DAR operation | [running-dar-operations](.agents/skills/dar/running-dar-operations/SKILL.md) |

Ship skills for recurring, useful workflows, with passing cold-session discovery
and task-application evidence. A failing baseline is not an admission requirement
under the current admission policy. Add a routing row only when its file
exists; remove the row if the file is withdrawn. Do not fabricate RED results or
claim improvement from an unmeasured baseline. A task without a shipped skill
remains governed by its layer instructions.

Follow the [file organization](.agentic/README.md#file-organization) when adding
an earned skill or specialist; do not create placeholder trees.

## Specialist routing

| Need / canonical role | Codex registration | Claude Code registration |
|---|---|---|
| Interviewing: [agile-analytics-facilitator](.agentic/agents/agile-analytics-facilitator.md) | `agile_analytics_facilitator` | `agile-analytics-facilitator` |
| Ingestion: [ingestion-specialist](.agentic/agents/ingestion-specialist.md) | `ingestion_specialist` | `ingestion-specialist` |
| DAS: [das-specialist](.agentic/agents/das-specialist.md) | `das_specialist` | `das-specialist` |
| DAB: [dab-specialist](.agentic/agents/dab-specialist.md) | `dab_specialist` | `dab-specialist` |
| DAR: [dar-specialist](.agentic/agents/dar-specialist.md) | `dar_specialist` | `dar-specialist` |
| Independent review: [data-platform-reviewer](.agentic/agents/data-platform-reviewer.md) | `data_platform_reviewer` | `data-platform-reviewer` |

Specialists are thin scope bindings, not alternate manuals. They follow this
router and the applicable layer instructions. Use the reviewer in fresh,
read-only context; an implementer's reasoning and claimed results are not review
evidence.

**Reviewer dispatch gate:** check the effective launch restrictions before
dispatch, not just the role registration. The tested Codex workspace-write parent
override defeats the reviewer's read-only setting: that launch is unsupported.
Restricted native Codex reviewer selection is **NOT_PROVEN**; do not dispatch it
as an enforced read-only reviewer. The tested fallback is a separate fresh
read-only session with approval `never`, loading the canonical role **manually**.
Claude's tested native reviewer is limited to Read/Grep/Glob, so shell verification
is NOT_RUN through that role. Never broaden tools, escalate, or use writable
delegation to get around either boundary. If effective restrictions cannot be
verified, stop reviewer dispatch. Read the versioned
[launch instructions and accepted reviewer support scope](.agentic/README.md#runtime-evidence-and-reviewer-launches)
before selecting a mode; successful manual loading is not native activation.

The facilitator owns the conversation and handoffs, not business decisions or a
second model. Read **Agile Analytics and interview bindings** in project context
before resuming an earlier loop. Historical prompts and their provenance remain
history; retired operational rules are not active guidance. The DAR interview
settles analytical answerability separately from DAB conceptual completeness;
its implementation and operation readiness still require the bound evidence.

Role files declare intended bindings; they do not prove runtime availability.
Select them natively when the interface supports it, subject to the reviewer
dispatch gate above. If it exposes no project-role selector, report that
limitation; reading or pasting a role is not native
activation evidence. The layer instructions still govern the task.
When reporting role activation, cite available launch metadata (invocation or
runtime dispatch/startup record). If unavailable, report UNKNOWN, not an inferred
native/manual mode. Reading a canonical role neither proves nor disproves native
selection; activation evidence does not establish permission enforcement.

## Active local gates

Resolve the credential-free landing, contract/generator/compile and integration
commands from project context. Do not substitute a similarly named provider or
connected check. A missing cloud identity does not prevent these local lanes.

## Always-loaded rules

1. Work on a branch and make each PR one reviewable invariant.
2. Review or approval does not authorize merge. Merge only after the user gives
   an explicit merge instruction.
3. Every warehouse write needs fresh authorization for the exact operation:
   landing names the provider, resource, window or pending package IDs;
   Dataform names the target and exact action selectors; Daana names the
   workflow, connection/namespace, affected entities and exact command. Prior
   proof or authorization never authorizes a rerun.
4. Before external access, read **Client identity** under **Operational
   restrictions** in the bound project context and verify the invocation's
   principal. Never use another client's account, credential, project or local
   configuration, or switch shared machine defaults to service this task.
5. Never commit credentials, tokens, signed URLs, personal payloads, or
   row-level customer data.
6. Landing and DAS staging contain no business logic. Landing preserves source
   values; staging only unpacks, safely casts, renames to lowercase
   `snake_case`, adds canonical technical metadata, and applies generic history
   mechanics.
7. Never hand-edit generated files. Change the owning contract or generator,
   regenerate, and review the output.
8. Compilation proves structure, not mapped values, historical completeness,
   materialized state, or business correctness.
9. Enumerate every expected generated-diff class before accepting a large diff;
   never dismiss it as merely mechanical.
10. Repair a defect in its owning layer. Do not smooth over bad acquisition in
    DAS or bad source mapping in DAB/DAR.
11. Prefer the smallest change supported by a real consumer and evidence.
    Technical success and sunk cost do not justify unused machinery; delete or
    park work whose business premise has vanished.
12. A change that alters a documented boundary updates or deletes the
    instruction stating it in the same PR.

## When guidance is missing

Stop before inventing a framework or operational claim. Inspect the owning
code, tests, contracts, current evidence, and the project's selected proven
reference where its physical assumptions match. Record proven ports, necessary
adaptations, retained divergences and decisions for the relevant owner separately.
