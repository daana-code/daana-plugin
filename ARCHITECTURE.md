# Analytical stack architecture

The stack preserves source evidence, integrates it into reviewed business concepts,
and uses those concepts to answer specific questions. The durable assets are the
contracts, model, mappings and definitions; generated code applies them
consistently and remains inspectable for verification.

The established DAS staging surface is the foundation for fast DAB/DAR iteration.
Changing a business interpretation should not require rediscovering how ingestion
records metadata or how a source's JSON is unpacked. Stable source evidence also
allows downstream transformations to be rebuilt and reconciled against history.

Read [AGENTS.md](AGENTS.md) for working constraints and routing, and
[ANALYTICS_PLAYBOOK.md](ANALYTICS_PLAYBOOK.md) for the question-to-answer method.
This document is an architectural map, not an operations runbook or a second
store of business definitions.

## Layers and data flow

The conceptual layers describe what the data represents: **Data According to
System (DAS)**, **Data According to Business (DAB)**, and **Data According to
Requirements (DAR)**. Ingestion has separate implementation ownership;
the landing evidence it produces is part of the system-oriented foundation.

```text
Sources
  |
Source acquisition / managed exports
  |
Landing / raw changelog
  |
DAS staging ----------------> DAB ----------------> DAR
  |                            ^
  +----> post-staging ----------+
         (when needed)
```

The optional path is DAS staging → post-staging → DAB; it does not feed back
into DAS staging.

| Boundary | Responsibility |
|---|---|
| Ingestion | Acquire source observations and preserve values, context and lineage. Different acquisition systems can have different physical interfaces. |
| DAS staging | Unpack, safely cast, harmonize names to lowercase `snake_case`, add technical metadata, and apply generic historized/latest mechanics. Stay source-oriented. |
| DAS post-staging | Supply justified, reviewed preparation needed before a DAB mapping. It is optional and handwritten; it is not generated staging or a home for dashboard-specific metrics. |
| DAB | Define, integrate and historize reusable business concepts: entities, identities, attributes and relationships. Mappings connect source evidence to the reviewed meaning. |
| DAR | Shape DAB data for a particular analytical requirement, with explicit grain, population, time basis and limitations. Production data products consume DAB, not convenient raw sources. |

DAS also provides historical staging for aligning retained history when needed,
and an assertions dataset for validation outputs. Historical staging remains
part of the pattern when empty. Neither is a mandatory intermediate step for
every source.

DAB's generated internal staging area is distinct from DAS staging: the former
is engine working storage; the latter is the published source-faithful interface.

## Work from the question; build on the foundation

Data flows toward consumption, but development starts with the decision and
question. Agree the meaning and grain, identify the DAB concepts needed, map them
to available DAS evidence, and build a thin answer for feedback. An absent source
value is a gap to expose, not permission to redefine the question. The playbook
owns this method, including the distinction between an intended answer and a proxy.

The interview has two distinct phases. DAB discovery asks which reusable things,
attributes and relationships must exist; business questions expose conceptual
gaps. DAR elicitation asks whether a fact grain, dimensions and runtime
calculations can answer the question or its atomic components. Reuse approved
definitions and existing analytical assets before designing new ones. A missing
business concept goes back to DAB, not into an improvised analytical join.

Stored observations and runtime metrics are not interchangeable. Configurable
distinct windows need sufficient identity/time detail; fixed-slice additive
questions can legitimately use aggregates. The emitter implements the approved
analytical design and does not decide its meaning.

DAB is independent of a particular dashboard. DAR products can have different
physical shapes and life cycles while reusing DAB's definitions; they should not
depend on each other's output tables. For example, an account and its recorded
responses are reusable business concepts. A particular retention window belongs
to the analytical requirement that uses them.

A presentation projects reviewed questions and artifacts; it does not invent
business definitions, operational readiness or answers. The playbook owns the
[question presentation contract](ANALYTICS_PLAYBOOK.md#question-presentation-contract).
Resolve actual register/presentation implementation via **Architecture and
presentation bindings** in the root router's Project context.

## Authoritative artifacts and tools

| What changes | Authoritative place |
|---|---|
| Question, desired answer, observable proxy and limitations | Bound question register and its review evidence |
| Provider requests, backfill windows and landing interface | Bound ingestion components and source-owner documentation |
| Source paths, names, types, keys and event semantics | Bound DAS contracts and template |
| Reusable projection and generic history | Bound DAS generator and its tests |
| Business entities, attributes, relationships and definitions | Bound DAB model |
| Source transformations and effective time | Bound DAB mappings |
| Mapping selection and physical coordinates | Bound workflow and connection configuration |
| Requirement-specific output | Authored DAR specifications and reviewed compiler capability |
| Working method, constraints and checks | Playbook, root/layer routers and bound gate owners |

These are artifact roles, not mandatory client filenames. Find their actual
locations, tools and capabilities through the task repository's Project context.
A generator may emit SQLX compiled/executed by Dataform; Daana can implement DAB
and supported DAR declarations. Do not infer availability from this architecture.
An unsupported pattern follows the playbook's reference/parity route, never a
hidden edit to generated output.

Declarative does not mean that every layer is implemented by the same tool, or
that the model alone supplies source mappings. Generated output is inspected to
understand behavior, not hand-edited to make it agree with an intended result.

## Physical boundaries and proof

Physical project/dataset topology is a project binding, not the definition of a
layer. Resolve actual coordinates, naming policy and source ownership from
context/configuration. A file's presence does not prove deployment. Legacy and
source-owned objects are not implicitly renamed or deleted by a new convention.

Business-event/effective time, source extraction time, warehouse arrival and
transformation execution time are different clocks. Their source-specific mapping
must be documented and verified. A timestamp's name alone does not make it a safe
incremental cursor; partitioning a target does not prove efficient source reads.

There are three distinct kinds of evidence:

- Local validation and compilation establish structural properties.
- Real-engine execution on synthetic fixtures establishes the behavior exercised
  by that fixture on the identified artifact.
- Reconciliation against actual sources and deployed output establishes measured
  correctness for that data and observation boundary.

Neither of the first two substitutes for the third. A permitted NULL is not proof
of correct mapping when the source contains a value. Likewise, a successful load
does not establish complete history, correct identities or agreed business meaning.

## Decisions are not capabilities

Read mandatory **Operational restrictions** before selecting an input or
preparing an operation. Authored mappings do not activate parked dependencies;
a proposal does not establish a cursor, scheduler, supported materialization or
identity policy. This overview grants no warehouse authority or business decision.

## Reference practice and provenance

Use the project's selected proven implementation reference where its physical and
business assumptions match. Preserve working patterns with minimal necessary
adaptation; label and prove improvements and retained divergences separately.
Another project's credentials, coordinates, schedules and source-specific rules
are not defaults.

Dated consultations and incident reports live behind project-context pointers.
Runtime claims need executable/image identity, observed generated behavior and
re-verification triggers. A closed ticket does not establish a deployed fix.

For the architectural rationale, read [The Design of Analytical Data Storage
Systems](https://blog.daana.dev/blog/design-of-analytical-systems),
[Contract-Driven Data Transformation](https://blog.daana.dev/blog/contract-driven-data-transformation)
and [The Rise of the Model-Driven Data Engineer](https://blog.daana.dev/blog/the-rise-of-model-driven-data-engineer).
The question-led method is explained in [From Business Question to Working
Prototype in Hours](https://blog.daana.dev/blog/from-business-question-to-prototype-in-hours)
and [The Anatomy of a Business Question](https://blog.daana.dev/blog/anatomy-of-business-question).
These explain the approach; implementation behavior is established from the
actual tools and data, not inferred from article examples.
