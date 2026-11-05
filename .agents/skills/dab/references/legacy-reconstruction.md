# Legacy reconstruction: a candidate, not an approved business model

Use within the existing model and mapping authoring skills when asked to derive
a first iteration from a dbt/Dataform or comparable transformation project.
The output is a useful candidate model **and source mappings**, with uncertainty
visible for later business review. This mode does not replace question-led
discovery, activate sources or authorize operations. It adds no skill or agent.

## Bound the task

Read the task's project context and existing approved model first. Use the stated
business/domain context to choose a subject area; domain knowledge suggests
questions, not facts. If no business question is supplied, reconstruct one bounded
connected area of the legacy project and state that choice. Do not invent a
decision-maker, analytical requirement or approval, or stop all drafting because
the owner is absent. If the task is an ordinary approved attribute addition,
stay in governed authoring: reconstruction is not a mandatory extra process.

## Reconstruct from evidence

1. **Read definitions, then implementation, then data.** Start with available
   glossary, model and documentation; record conflicts and approval provenance.
   Trace authored SQL, source declarations, tests, dependencies and existing
   compiled artifacts before interpreting supplied or authorized sample data.
   Inspect macros, hooks and configuration before running tools: a compile command
   can execute code or access external systems. Dynamic/unresolved dependencies
   are gaps, not guessed relations. No tool execution is required just to draft.
2. **Recover each row's meaning.** Trace keys (including composites), joins,
   filters, aggregations, deduplication, snapshots and history. Record input and
   output grain, clock/units, NULL/deletion semantics and loss of detail. Declared
   tests are intended constraints, not measured results; a join in code is not a
   cardinality proof. Equal values on two days may be two observations; corrected
   versions of one event may still be one event. A timestamp's name alone cannot
   establish business time, acquisition time or safe incremental processing.
3. **Separate concepts from tables.** Identify candidate things with independent
   identity/lifecycle, descriptive attributes, and relationships at an effective
   instant. A reporting group-by does not by itself earn an entity, and not every
   intermediate or mart becomes one. A physical link table is not automatically
   M:N: multiple targets over history can remain N:1 at each instant. Inspect all
   its columns, including created/updated times; names do not make them disposable.
   If association attributes/lifecycle justify a link entity, explain that choice.
4. **Draft model and mappings together.** Use the bound compiler's supported
   vocabulary and the existing authoring workflows. Preserve explicit composite
   identity without confusing it with multi-identifier merging. Keep implemented
   population filters and time choices traceable; do not silently generalize a
   report's filter into the definition of a reusable concept. Show legacy-preserving
   bindings separately from proposed corrections. Existing approved meaning wins
   over contradictory code; report the discrepancy instead of rewriting it.
5. **Keep one support matrix.** Extend the authoring matrix, rather than creating
   a new registry. For each candidate record source path/revision and distinguish:
   documented meaning with its provenance; directly observed implementation;
   inference with rationale; and unresolved input/owner decisions. Documentation
   is not automatically approval. State whether cardinality/coverage comes from
   declarations, code or actual supplied measurements, and how to challenge it.
6. **Deliver the supported subset.** Author candidate model/mapping YAML in a
   clearly marked draft location outside the selected runtime workflow; do not
   replace approved artifacts or add mappings to active execution. Use comments
   and the completion report for candidate status, not invented language fields.
   Missing compiler bindings permit a conceptual model plus field-level mapping
   specification, labelled not compiler-validated. Missing inputs get explicit
   omissions or preparation handoffs, never constant-NULL mappings, fabricated
   identifiers or lookups typed from domain memory. Do not repair upstream data
   while reconstructing the model.
7. **Check and hand off.** Run only verified local commands and supplied-fixture
   checks within scope; compare keys, populations, time and relationship behavior
   against the traced legacy logic. State which differences preserve behavior and
   which require review. Report missing source readiness and unsupported compiler
   mechanisms without claiming execution. Use the existing
   [completion report](completion-report.md), including exact omissions and the
   few owner questions that would materially change the candidate. Later review
   may promote, revise or reject it; operations retain their separate authorization.

## Illustration (not a compiler declaration or project command)

A maintenance project has equipment rows, assignment intervals, and a regional
dashboard that selects only operational equipment. A candidate may retain
equipment as an entity, condition as an attribute and assignment as a temporal
relationship. The dashboard filter is observed scope, not proof that stopped
equipment ceases to exist. Distinct assignments across years do not establish
simultaneous M:N. An inspection's repeated equal reading can be independently
meaningful; a corrected reading of that same inspection is not a new inspection.
Each choice needs source evidence and, where inferred, a visible review question.

Success is a reviewable first iteration, not a questionnaire alone and not a
production-ready migration. Do not claim broad generality from repeatedly tuning
against one demo: assess different domains and structures, preserve failures, and
keep cases used for revision separate from fresh held-out cases.
