---
name: facilitating-agile-analytics
description: Use when interviewing a business owner, clarifying an analytics decision or question, reviewing business definitions conversationally, or facilitating a question-led Agile Analytics loop. Technical model/mapping implementation uses the layer skills after meaning is reviewed.
---

# Facilitating Agile Analytics

First read the [project binding procedure](../references/project-bindings.md); use the task
repository's context, even when this skill is installed elsewhere.

## Establish the current conversation

Read the **Agile Analytics and interview bindings** in project context,
working playbook, active question, reviewed model and interview README. Read the
selected current interview ledger chronologically through its latest record;
resolve later corrections and explicit supersessions before using an approval.
Check the continuity handoff when resuming earlier work. Historical prompts are
provenance, not current operational instructions.

Use existing answers before asking factual questions again. Explain a material
conflict and seek the owner's resolution only for the affected meaning. Do not
import a different branch's model or assume the latest timestamp approves every
proposal. Keep confirmed, proposed, inferred, measured and unknown separate.

## Interview posture

Ask one short, understandable question and wait for the owner's answer. Begin
with the decision or pain; narrow according to what the answer reveals. Restate
what you heard and its consequence, then ask the next question that reduces
uncertainty. Do not answer on the owner's behalf or append a questionnaire.
If a question is unclear, explain a concrete business example before asking again.

Listen for nouns (entities), verbs (events/relationships) and adjectives
(attributes/classifications). Ask what is wrong or missing in your interpretation.
Examples and counterexamples should resolve meaningful identity, grain, lifecycle
or time boundaries. Do not repeatedly reopen confirmed decisions without new
contradictory evidence. Record who accepted a meaning and at what scope; one
team's definition is not automatically an enterprise definition.

## Facilitate one five-step loop

1. **Business needs:** establish the decision, owner and what plausible answers
   would change. Produce one readable question with aggregation, measure/event,
   population, dimensions, time basis, grain and definitions. Keep identifiers out
   of the question's prose. Confirm meaning before promoting it to the question
   register or model; existing explicit confirmations remain valid.
2. **Information modelling:** review one connected concept at a time: definition,
   identity, relationships, required attributes/value domains, business time and
   lifecycle. Prefer observable events where they express the intended concept;
   do not redefine a requested state merely to fit an event table. Preserve
   disagreements; use distinct concepts when one label hides different meanings.
   Use [model authoring](../../dab/authoring-dab-models/SKILL.md) for approved YAML.
3. **Source mapping:** after the initial question and meaning are understood,
   inspect contracts and source evidence with the relevant specialist. Classify
   support as exact, proxy or unavailable; a proxy retains its own question and
   limitation. Missing data does not change the business definition. Use
   [mapping authoring](../../dab/authoring-dab-mappings/SKILL.md) for bindings.
4. **Thin prototype:** hand the analytical phase to
   [DAR elicitation](../../dar/eliciting-dar-requirements/SKILL.md): determine
   whether existing or proposed facts, dimensions and runtime calculations
   answer the question. This is distinct from DAB conceptual completeness, not
   another pass through the entity interview. Reuse settled answers; return a
   specific missing concept to DAB. Coordinate the smallest DAS → DAB → DAR
   slice, preserving approved meaning when tooling cannot express it. Do not
   repair generated output. Label synthetic results and show the simplest useful
   visual for feedback.
5. **Business feedback:** return to the original decision with the prototype and
   limitations. Ask whether it answers the need and what is wrong or missing.
   Record validation, refinement or pivot. Close or explicitly park the loop with
   the owner before switching questions; do not silently run several interviews.

Business owners decide meaning. Source owners establish encodings and evidence.
Use technical subagents for bounded independent investigation or review when
useful; they may not settle business ambiguity for the owner. Select repository
roles natively only when supported and report the mechanism honestly. The
facilitator may prepare handoffs without deploying or acquiring new data.

## Evidence, handoffs and progress

Preserve interview statements and later corrections as evidence using the current
ledger's conventions. Never manufacture quotations, speakers, timestamps or
approvals. Keep exploratory proposals distinct from approved model changes;
append an explicit supersession rather than erasing an earlier decision.
Evergreen definitions belong in the model, source bindings in mappings, and
question-specific windows/proxies in the question or DAR contract.

At a meaningful checkpoint state the active question, loop step, confirmed
meaning, unresolved decisions and smallest next action. Scale the report to the
conversation; a single interview turn normally needs only a restatement and the
next question. Use the existing technical completion reports for implementation.

Request independent review through the bound technical reviewer role for substantive technical
handoffs, with fresh read-only context and the relevant playbook/layer rules.
Review does not replace business feedback or authorize a warehouse operation.
A facilitation session can end with a clear decision or evidence request; a full
loop is complete only after the agreed slice is reconciled and the owner has
validated, refined or pivoted. Do not claim a measured answer from local syntax
checks or promote archived operational rules into the current workflow.
