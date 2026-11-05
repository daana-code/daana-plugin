# Analytics playbook

- **Status:** durable operating standard
- **Source review:** 2026-08-27
- **Scope:** business questions, DAB semantic modelling, DAR requirements, and model review

This document records the analytics method distilled from the Daana blog and
Daana CLI documentation. Read it before adding or changing a business question,
business concept, analytical requirement, metric, or presentation.

The short version: good analytics is not a collection of dashboards. It is a
repeatable path from a decision-relevant business question to a defined,
time-correct, testable answer whose limitations remain visible wherever the
answer is shown.

## 1. Start with the decision, not the data

The question-led procedure below governs agreed business meaning and published
answers. When explicitly asked to draft a first model from typed sources or an
existing transformation project without approved meaning, use the source-led
candidate mode of the existing DAB authoring workflows. Legacy dbt/Dataform
projects also use the
[reconstruction procedure](.agents/skills/dab/references/legacy-reconstruction.md).
Inspect available definitions, source/schema evidence and implementation to
produce a bounded, evidence-labelled candidate model **and mappings** for later
review, outside the selected model and workflow. This is an exception to discovery
order for drafting, not permission
to redefine approved concepts, claim business approval or publish an answer.
Missing owner input limits promotion; it need not prevent a useful draft.

Before querying anything, establish:

1. What decision will this answer change?
2. Who owns that decision?
3. What is the exact business question?
4. What would we do differently for each plausible answer?

If no action follows from the answer, the report is probably not worth building.
Do not begin from a convenient table, an available event, or a requested chart.
Those prematurely constrain the question to what is already easy to measure.

Business discovery comes before source mapping. During discovery, listen for:

- nouns: entities such as user, medication, app, pharmacy;
- verbs: relationships and events such as installs, takes, follows, buys;
- adjectives: attributes or classifications such as active, billable, new.

The business explains what must be understood. Data and engineering then explain
what can currently be observed. A gap between the two is a finding, not an excuse
to silently substitute a different question.

## 2. Make every question answerable

A question must identify all of the following:

- **aggregation:** count, sum, average, rate, distribution, survival estimate;
- **measure or event:** exactly what is counted or calculated;
- **population:** who or what is eligible;
- **dimensions:** how the answer may be sliced;
- **time window:** the observation or attribution window;
- **grain:** the unit represented by one row or observation;
- **definitions:** every term a reasonable reader could interpret differently.

A useful pattern is:

> What is the **aggregation** of **measure** for **population**, by
> **dimensions**, during or as of **time basis**?

Force statements such as “monthly active users by country” into actual questions.
Split compound questions when their measures, grains, populations, or visual forms
differ. “Active,” “install,” “customer,” “conversion,” “retention,” and “churn”
are not definitions by themselves.

### Question presentation contract

Every question records five distinct things: a readable business question;
its interpretation (population, time and observability); whether measurement is
exact, proxy or unavailable with explicit limitations; required reusable DAB
concepts; and required question-specific DAR outputs. A proxy has its own readable
question and interpretation. Keep natural-language copy separate from stable
semantic identifiers.

The register owns the question and required identities; the DAB model owns concept
names/definitions; mappings own source connections; DAR owns analytical outputs.
Presentation owns none of them. Resolve actual field names, registry schema and
presentation rules through **Architecture and presentation bindings** in the task
repository's Project context. Do not copy a project's registry implementation into
this general method.

### Presentation state

Project progress from authoritative artifacts, not manually maintained labels.
Keep semantic publication, source mapping, analytical declaration and operational
verification distinct: existence in a model or a compiled output is not deployment
or correctness. The project's presentation binding defines actual checks/states;
this method does not prescribe a UI, a combined readiness score or a scheduler.

## 3. Definitions are part of the data product

Define business concepts before relying on their names. Two teams using the same
word differently is information that must be recorded, not smoothed over.

In the declarative model:

- `definition` says what a business concept **is**, concisely;
- `description` provides the business context needed to interpret it correctly;
- the reviewed DAB model YAML owns entities, attributes, relationships, definitions,
  and descriptions;
- DAR requirement YAML owns the decision-relevant question and the analytical shape
  required to answer it;
- DAS contracts and implementation evidence own source provenance, mechanics,
  incidents, and reconciliation results.

An approved concept has one stable identity in the DAB model. Its wording may be
improved through review in that one place. If a change alters identity, qualifying
behaviour, grain, population, time meaning, or historical interpretation, make the
change explicit rather than silently rewriting an older analytical result. DAR
requirements refer to the model instead of copying its definitions.

Do not copy source lineage into definitions. Do not let a dashboard invent a local
meaning for a shared term. Do not hide competing definitions behind one label:
publish distinct metrics with distinct names until the business chooses one.

Every prioritized question must be answerable from the information model. If the
model cannot express the measure, participant, relationship, or time basis, the
model has exposed a real gap.

## 4. Keep the layers honest

Daana's three-layer distinction is the architectural contract:

| Layer | Purpose | Boundary |
|---|---|---|
| **DAS — Data According to System** | Preserve source-shaped data for replay, audit, and debugging | Accept raw records, then enforce structural contracts at the staging boundary |
| **DAB — Data According to Business** | Integrate, conform, define, and historize reusable business concepts | Remain source-agnostic and independent of any one dashboard |
| **DAR — Data According to Requirements** | Shape dimensions, facts, metrics, and marts for a specific analytical use | Begin from a declared question and consume DAB, not operational source tables |
| **Review/presentation surface** | Make the question-led loop and its evidence visible | Project authoritative artifacts; never become a second definition, mapping, status or metric layer |

DAB is reusable truth. DAR is a purposeful view of that truth. Reusing definitions
does not mean forcing unrelated questions through one shared wide table. Each DAR
artifact may optimize for its consumer as long as its grain, semantics, and lineage
remain explicit.

## 5. Declare grain and time semantics

DAB discovery establishes reusable concepts; DAR elicitation establishes
analytical answerability. Use existing approved answers in both phases, not one
blended interview. Before proposing a new fact or dimension, inspect whether an
existing asset or compatible bounded extension already suffices. The dedicated
[DAR elicitation workflow](.agents/skills/dar/eliciting-dar-requirements/SKILL.md)
owns the analytical questions and handoff to specification authoring.

Before writing a metric query, write one sentence that begins:

> One row represents ...

Then state:

- the natural/business key;
- event time, effective time, and load time where relevant;
- whether the view is current-state, event history, cohort, or periodic snapshot;
- whether each measure is additive, semi-additive, or non-additive;
- which relationships can fan out the fact;
- the allowed dimensions and the expected cardinality after every join.

Express the declared grain as an output constraint, including key/NULL and
relevant temporal policy. An unassertable grain is a finding to resolve; neither
an arbitrary row number nor deduplication supplies missing business identity.
Whether the selected compiler emits/enforces that constraint is a separate check.

Historical questions require historical joins. A fact must join a Type 2 dimension
using the fact's event timestamp between the dimension's validity boundaries. A
current-state join can silently rewrite history—for example, attributing an old
event to a user's current status. Missing historical attributes may be the truthful
answer; fallback or imputation is a business decision, not a harmless technical fix.

Ratios, distinct counts, retention, survival estimates, and rolling windows require
special care because they cannot be freely summed or averaged. Their numerator,
denominator, censoring rules, horizon, and window boundaries belong in the metric
contract.

Runtime metrics preserve governed meaning while letting the reporting user
choose supported parameters. Daily, weekly and monthly distinct activity can
share sufficient underlying detail; daily distincts cannot simply be summed.
Conversely, fixed slices and genuinely additive measures can use a justified
rollup. Retain what the approved question needs, not every speculative future
capability. Record the runtime recipe and sufficiency argument in the existing
analytical artifact, not a new metrics registry.

## 6. Build a thin end-to-end slice first

Work on exactly one prioritized business question at a time. Keep one question
dossier that connects the canonical question, glossary terms, information model,
mappings, lineage, metric, evidence, decisions, and discussion. The dossier is a
view over those sources of truth, not another place to copy and maintain them.

The interview is a conversation, not a questionnaire. Ask one open question,
wait for the answer, restate what was heard, and ask the next narrowing question.
Begin with the decision and, once an initial understanding exists, ask what is
wrong in that understanding. Use why, what, who, how, where, and when only as
needed. Read authored material before asking factual questions, but do not measure
or let available data define the business meaning before the decision-maker has.

For each question dossier:

1. Establish the decision, its owner, and what would change for plausible answers.
2. Turn the request into one Stage-3 question: aggregation, measure or event,
   population, dimensions, grain, time basis, and definitions.
3. Derive the expected model from the question's nouns, verbs, and adjectives
   before inspecting implementation SQL.
4. Walk the connected model one entity at a time: definition, description,
   relationships, and then every attribute. Mark each attribute as load-bearing,
   identity/grain/filter context, unrelated to this question, or missing. A
   dependency discovered from SQL is a lead, not the semantic requirement.
5. Map the agreed concepts to authored sources, mappings, lineage, and only then
   measured data. Record gaps instead of substituting an observable proxy.
6. Agree the metric contract before SQL: one-row grain, eligibility and
   exclusions, numerator and denominator, window boundaries, censoring,
   timezone, confidence, and falsifier.
7. Build the thinnest complete DAS → DAB → DAR slice, reconcile it across the
   layers, and project reviewed artifacts into the bound review surface.
8. Return to the decision-maker: does it answer the original decision, what is
   wrong or missing, and should we validate, refine, or pivot? Close the dossier
   before starting the next question.

A prototype is a learning instrument, not a smaller production dashboard. Its job
is to expose wrong definitions, missing data, broken identifiers, bad joins, and
misunderstood decisions early. Basic charts and visible caveats help stakeholders
react to the substance rather than the polish.

### DAR capability feedback loop

The DAR YAML declares the required analytical end state and generated SQL is a
build artifact. Use the current DAR compiler wherever it faithfully implements
that declaration.

When a business requirement is not yet expressible or the compiler output is
incorrect:

1. Keep the approved business meaning unchanged. Do not weaken the question or
   move analytical logic into DAB merely to fit current tooling.
2. Implement the smallest temporary DAR artifact that expresses the requirement
   correctly. It must consume DAB only, declare its grain and time semantics, and
   remain visibly temporary.
3. Test it with boundary fixtures, grain/cardinality checks, and reconciled real
   data. A compiling query is not sufficient evidence.
4. Give the DAR team the desired YAML shape, the executable reference result, a
   minimal failing fixture, and the acceptance criteria. This demonstrates the
   missing capability without prescribing compiler plumbing.
5. Replace the temporary artifact with generated output only after result parity
   is proven. Never repair generated SQL by hand.

Compiler limitations, fixtures, reconciliation results, and migration evidence
belong in implementation records. They never belong in evergreen entity,
attribute, or relationship definitions.

## 7. Treat uncertainty as first-class output

Every answer must separate:

- **measured:** reproduced from identified data with a known query;
- **derived:** calculated from measured inputs under stated rules;
- **assumed:** supplied by a person or scenario rather than observed;
- **inferred:** a plausible explanation not established by the data;
- **unknown:** not currently answerable;
- **blocked:** answerable only after a named dependency changes.

An unanswered question remains visible. A blocked question names its blocker. An
open question names the evidence route that could answer it. A claim names what
would prove it wrong. Confidence is capped by the weakest necessary source; adding
a strong source does not launder a biased or incomplete one.

Never type a live figure into prose when it can be projected from its metric. The
DAB model carries shared business meaning, the DAR requirement carries decision
context, and the computed metric carries the number.

## 8. Use the simplest truthful visual form

Choose the visual from the question:

| Question shape | Default form |
|---|---|
| One conclusion or KPI | Headline/card, often no chart |
| Trend over time | Line or area chart |
| Category comparison | Bar chart |
| Part-to-whole | Stacked bar; pie only for a few segments |
| Distribution | Histogram or box plot |
| Correlation | Scatter plot |
| Row-by-row breakdown | Table |

Importance and chartability are different. An existential question may deserve a
single sentence; a less important distribution may require a chart because its
shape is the result. If a chart needs a long explanation before it can be read,
simplify it or choose another form.

Any answer surface must put the question and answer before implementation detail.
Definitions, population, time basis, confidence, caveat, and evidence must travel
with any exported or externally quoted number. A review surface is not automatically
an analytical-answer surface; honor the project's explicit presentation boundary.

## 9. Validate semantics and data, not only code

For every non-trivial metric:

1. Read the reviewed definition, then its mapping; discover source schema and
   keys with the mapping's filters and transformations understood.
2. Profile cardinality, nulls, domains, outliers, and temporal coverage.
3. Test transformations against real rows before finalizing mappings.
4. Reconcile counts and values across each layer at the same cutoff time.
5. Test join cardinality and prove the expected grain survives.
6. Test boundary cases for windows, cohorts, time zones, and censoring.
7. Make every automated guard fail on a deliberately broken fixture.
8. Obtain domain review for semantic assumptions.
9. Run the project-bound local gates and report separately which semantic or
   deployment checks they do not perform.

A successful compile or zero exit code is not evidence that the answer is correct.
Syntax validation cannot determine whether “active” means the right activity or
whether the denominator matches the decision.

## 10. The question contract

Before a question is presented as answered, its authored and derived artifacts must
make these fields recoverable:

| Field | Required content |
|---|---|
| Decision | What changes depending on the answer, and who decides |
| Question | A complete, interrogative business question |
| Status | Answered, open, or blocked—with route or blocker |
| Claim | The shortest defensible answer |
| Definition | Exact meaning of every ambiguous concept |
| Population | Eligibility, exclusions, and identity basis |
| Numerator/denominator | Explicit components for any rate or ratio |
| Grain | What one row or observation represents |
| Time basis | Event time, window, cohort, horizon, timezone, and as-of date |
| Metric | Canonical DAR artifact that computes the figure |
| Evidence | Sources and their limitations |
| Confidence | No higher than the weakest load-bearing source |
| Caveat/falsifier | What changes interpretation or would disprove the claim |
| Owner/next action | Who can close the remaining uncertainty |

## 11. Failure patterns this repository must prevent

- Building a dashboard before agreeing on the decision and question.
- Letting the available source event redefine the business concept.
- Publishing “active users” without the qualifying behavior and window.
- Treating download, install, first open, signup, onboarding, and activation as
  interchangeable funnel stages.
- Mixing populations, time windows, grains, or modelling constructions in one
  headline ratio.
- Joining historical facts to present-day attributes.
- Hiding missing data with fallback values that look observed.
- Treating telemetry from a self-selected sample as complete population volume.
- Allowing a many-to-many join to multiply a measure.
- Copying a number into question prose, presentation copy, or documentation.
- Encoding business meaning only inside SQL or a chart component.
- Showing a confident visualization for an open causal question.
- Adding a check that has never been demonstrated to fail correctly.

## 12. Definition of done

A scoped source-led drafting task can finish with a useful candidate and explicit
gaps under the mode above. It is not a completed analytics product; the following
publication criteria still apply.

An analytics change is done only when:

- the decision and question are explicit;
- the relevant domain terms have reviewed definitions;
- the metric has a declared grain, population, and time basis;
- lineage exists from DAS through DAB to DAR, and the bound review/presentation surface matches
  the reviewed artifacts;
- real-data tests and layer reconciliations pass at a common cutoff;
- historical joins and join cardinalities are verified;
- assumptions, caveats, confidence, and falsifier are visible;
- the visual form matches the question;
- automated checks have proved they catch representative failures;
- the decision-maker confirms that the result answers the intended question.

## Sources reviewed

Daana blog:

- [From Business Question to Working Prototype in Hours](https://blog.daana.dev/blog/from-business-question-to-prototype-in-hours)
- [The Anatomy of a Business Question](https://blog.daana.dev/blog/anatomy-of-business-question)
- [Why Definitions Are the Foundation of Every Data Warehouse](https://blog.daana.dev/blog/definitions-for-integration)
- [The Design of Analytical Data Storage Systems](https://blog.daana.dev/blog/design-of-analytical-systems)
- [The Consumption Layer Should Generate Itself](https://blog.daana.dev/blog/consumption-layer-generates-itself)
- [Contract-Driven Data Transformation](https://blog.daana.dev/blog/contract-driven-data-transformation)
- [Context Isn't Enough: Agentic Analytics Eventually Has to Fix the Data](https://blog.daana.dev/blog/context-isnt-enough)
- [The Work Before the Answer](https://blog.daana.dev/blog/the-work-before-the-answer)

Daana CLI documentation:

- [Data Warehousing Fundamentals](https://docs.daana.dev/docs/concepts/data-warehousing-fundamentals)
- [Daana Model Description Language](https://docs.daana.dev/docs/dmdl)
- [Model](https://docs.daana.dev/docs/dmdl/model)
- [Understanding Daana Output](https://docs.daana.dev/docs/guides/understanding-daana-output)
- [Chapter 7 — Building Your Analytics Layer](https://docs.daana.dev/docs/tutorial/07-analytics-layer)
- [Chapter 6 — Going to Production](https://docs.daana.dev/docs/tutorial/06-going-to-production)

This playbook is a reusable synthesis, not a replacement for those sources. When
the Daana guidance changes materially, update this document and record the review
date at the top.
