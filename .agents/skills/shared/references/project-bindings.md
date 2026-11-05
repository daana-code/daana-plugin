# Resolve the task project's bindings

These skills may be installed outside the repository they operate on. Read the
**task repository's root `AGENTS.md`**, follow its explicit **Project context**
binding, then read the named sections needed by the selected workflow. Resolve
links inside that context relative to that document, not this installed package.
Never walk up from a skill's installation directory to guess the client checkout.

Before project-specific source/target selection or operation-packet preparation,
read **Coordinates and identity**, **Operational restrictions**, and the selected
tool's credential bindings. These are mandatory operation inputs even when the
calling router does not repeat this requirement. Ambient ADC/gcloud identity is
not a binding. A graph reference, example, successful check or prior approval
does not activate a parked source or authorize another operation. Root/layer
authorization rules remain mandatory; context supplies the actual restrictions
and approval authority, not permission to bypass them.

## Binding contract

The project context is a searchable Markdown index, not executable configuration.
It supplies these sections as applicable, linking to existing authoritative files:

| Section | Resolve before relying on it |
|---|---|
| Coordinates and identity | Client, project/location, namespaces and invocation-specific identity |
| Operational restrictions | Client-identity constraints, approval authority, parked/retired inputs, forbidden operations, conditions and owner for reopening |
| Architecture and presentation bindings | Layer/tool ownership, question/analytical artifacts and presentation contracts |
| Warehouse bindings | Selected backend/dialect/client, approved credential or local-artifact mechanism, validation/cost/limit/snapshot capabilities, read authority and evidence home |
| Ingestion bindings | Active components; provider account/tenant and approved source credential/identity-verification mechanism (separate from warehouse identity); parser/window commands, payload/identity/clock interface, disposition, durable state/recovery and local tests |
| DAS authoring bindings | Contracts/template/owner questions, lifecycle policy, supported shapes/types/materializations and canonical metadata |
| DAS code and coverage map | Projection, vocabulary and assembly owners; supported and rejected cases, fixtures and gaps |
| DAS commands and credential mechanisms | Local gates, generation, graph capture, cloud analysis and exact execution interface |
| DAB bindings | Model, mappings, workflow, connections, questions and source-support evidence |
| DAB offline commands and DMDL fields | Selected compiler capability/version evidence and actual local/connected command bindings; reusable field/check mechanics travel in the DAB package reference |
| DAB evidence qualifications and refresh scope | Artifact/mode provenance, dated behavior, operational scope, omissions and re-verification triggers |
| Agile Analytics and interview bindings | Playbook, active question/model, chronological ledger, continuity handoff and review role |
| DAR authoring bindings | Analytical inputs/model/workspace/output locations, canonical definitions, designated fallback/gap owner and naming convention |
| DAR compiler and operation bindings | Selected artifact and verified local/connected command forms, dialect/backend, catalog mode, invocation identity, operation authority and unresolved capabilities |
| DAR evidence | Dated compiler/layout/result observations, artifact scope, omissions and re-verification triggers |
| Analytics consumption and diagnostic bindings | Approved published outputs and readiness evidence, definitions/grain/time policy, pattern metadata where applicable, backend/read authority, lineage metadata and artifact scope, failure records/recipes, and the owner of a support gap |

If the context, Coordinates and identity, Operational restrictions, or relevant
credential binding is missing, stop project-specific source/target selection,
operation-packet preparation and external access. Report the missing prerequisites;
do not substitute a conceptual recovery/deployment packet for resolved bindings.
Continue independent local contract/model authoring from supplied artifacts.
For other missing bindings, name the affected artifact/decision and stop only the
work that depends on it. Do not import another client's defaults, guess a command,
invent source availability or demand cloud credentials for local authoring. If the
router itself is absent, ask for the task repository/context location; do not use
an unrelated ancestor repository. A stale observation is not current deployment
proof.

Internal links between skills/references resolve inside this package. Distribute
the selected workflows with their linked dependencies; do not satisfy a broken
package link by copying private project evidence into the installed skills.
When a skill is exposed through a directory symlink, resolve these internal links
from the canonical target file, not the flat discovery alias. This does not change
the task-root rule for project context.
