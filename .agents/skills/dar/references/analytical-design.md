# Analytical design and evidence

Use this reference for grain, reuse, dimensions, time, runtime measures and
reconciliation. It is independent of an emitter. Tool syntax belongs in
[Daana DAR](daana-dar.md); actual policy and paths come from the task project's
[bindings](../../shared/references/project-bindings.md).

## Definition, mapping, then profile

Read the reviewed business definition first, its source mapping second, and
profile relevant data third. Filters, identity translations, derived timestamps
and mapping exclusions often explain missing keys. A histogram without these
inputs cannot distinguish an absent concept from intentionally excluded data.
Check input support and active/approved status, not just declaration existence.

Investigate technical facts; ask the owner about unresolved intent. Reuse prior
answers. Ask the fewest understandable questions that settle the design, one at
a time, and return one coherent design for confirmation. Missing reusable
meaning goes to DAB; missing acquisition or bad mapping goes to its owning
layer. Neither is repaired by inventing an analytical interpretation downstream.

## Reuse and sufficient detail

Inventory existing facts, dimensions and relationship outputs before designing
another one. Compare grain, population, definition, units, time basis, dimension
variant, coverage and retained detail. Choose reuse, a compatible bounded
extension, or a new output with the precise unmet requirement. Similar names
are not compatibility; changing a shared asset must preserve its other consumers.

Preserve the detail the approved question requires, not all conceivable detail.
For additive measures over fixed, exhaustive, non-overlapping slices, an existing
rollup can be sufficient. State additivity across each requested axis, its unique
grouping key and its boundary; aggregate and finish. Do not demand atomic identity
or another owner decision when the approved requirement has no need for either.
State unsupported future uses as limits, not blockers to the current question.

Conversely, daily distinct borrowers cannot be summed to obtain monthly distinct
borrowers. A configurable distinct window needs retained identities or another
explicitly approved sufficient representation. Ratios need compatible numerators
and denominators; balances usually need a time-selection rule, not a SUM across
time. Do not mint one fact per runtime window or invent a metric DSL.

## Assertable grain before pattern selection

Write what one row means and express it as an output constraint. Examples:

| Intended grain | Constraint to test |
|---|---|
| One independent occurrence | Non-NULL occurrence key, unique once in the output |
| Entity at a periodic boundary | Unique entity + boundary, explicit eligibility and absent-period policy |
| One lifecycle instance | Unique instance key; each milestone/value states its own time basis |
| Dimension version | Unique entity + effective start; valid intervals and required non-overlap per entity |
| Fixed-slice additive rollup | Unique grouping tuple, documented NULL group policy and compatible units |

Test uniqueness, NULL keys and relevant temporal constraints, not only total
counts. An inexpressible grain is an elicitation finding. Historical versions
per key can be corrections or restatements, not independent events. A row-count
histogram is evidence, never the grain definition. Do not append ROW_NUMBER,
pick an arbitrary winner or use DISTINCT to manufacture a business grain.

An expressible constraint is not compiler enforcement. Inspect whether a
supported declaration emits a check and whether it actually runs. Otherwise
retain the constraint and report the necessary verification separately; no
fictional YAML assertion field or claim of a protected join.

Choose the analytical pattern from the meaning: occurrence/event, state at a
periodic boundary, accumulating lifecycle milestones, or a justified combination.
Do not treat the compiler's menu of kinds as the business interview.

## Dimensions and relationships

Decide fact, dimension, or both. Separate event/state measures, flags and keys
from descriptive slicing attributes; a wide view does not settle ownership.
Choose values as of fact/milestone time, latest values, or both from the approved
analysis. Inspect conformed dimensions and do not silently change their variant.

An embedded foreign entity key belongs on a dimension only when single-valued
from its side and immutable. Could changing that relationship create a dimension
version while the entity's own attributes remain unchanged? If yes, represent
the relationship with its time semantics separately. Parent attributes are not
intrinsic child attributes. Classify cardinality and mutability independently:
a fixed M:N relation still multiplies rows and measures. Allocation, selection
or a bridge grain requires a justified policy, not arbitrary parent selection.

At each effective instant test the intended N:1 relation, unmatched keys and
fan-out. Inspect interval predicates and probe exact endpoints. Do not assume
all emitters use half-open validity intervals: some emit inclusive ends one
microsecond before the next start. Match the verified representation and test
that a boundary row matches exactly the intended version.

### Tracking start and unknown history

Entity existence before tracking does not prove its first observed attributes
held earlier. Compare independently evidenced entity ages/creation times with
the distribution of first effective times at a common boundary. Recent
clustering can indicate bulk population; inspect mapping time expressions and
load evidence, and consider alternative explanations. Without age evidence or
historical values, the inference remains unresolved.

Record the approved observed-start/unknown-history policy and label any imputation.
Backdating is an assertion about earlier values, not a fix for missing joins.
Do not backdate automatically for reference entities or for convenient coverage.

## Definitions and names

For DAB-sourced meaning use the bound canonical model, then only an explicitly
designated fallback. Record fallback provenance and the canonical gap. A
conflicting fallback does not overrule the canonical owner. If neither supplies
the meaning, request it through the existing owner-question/review mechanism.
Do not infer meaning from names, sample values or generated SQL. No second glossary.

DAR-derived semantics come from the approved analytical/metric requirement.
Describe units, keys, NULL meaning and time basis as relevant; technical columns
may be described from verified mechanics. A derivation alone is not a business
definition. Missing meaning blocks publication of the affected output, not
independent local work on already approved outputs.

Apply the bound naming convention and inspect emitted names. Do not silently
import another project's prefixes. In a lifecycle fact, a value resolved at a
milestone names that milestone (or explicitly latest/current) in its name,
description and join. An unqualified name asserts milestone independence and
needs an established invariant, not a sample with no observed changes.

## Reconciliation by meaning

Write the prediction before comparing. Source-row equality is an oracle only
for a true pass-through event fact, not every transformed grain. Test snapshots
against state at their boundary, lifecycle outputs against milestone meaning,
distinct metrics against identity sets and additive rollups against compatible
sums per slice as well as the grand total. A wrong as-of join can preserve the
grand total while moving measures between dimensions.

Pin sources, dimensions and outputs to one observation boundary. If history or
access cannot support that, qualify the comparison instead of attributing drift
to a mapping defect. Use typed comparisons and explain each filter, transformation,
late observation and expected NULL. Query-body validity is not published-schema
validity; duplicate column names can prevent CREATE VIEW despite a valid SELECT.

At least once per newly introduced upstream entity, trace a bounded load-bearing
result through DAB mappings and DAS to raw/landing. Reuse an earlier trace only
when its artifact/input scope and semantics still apply. Changed inputs or
meaning require the affected check again. This is verification lineage, never
a raw dependency in production DAR. Without authorized access, record NOT_RUN
and qualify fidelity rather than start a full-estate audit.

## Completion evidence

Report changed artifacts, agent decisions versus owner decisions, the analytical
result or precise finding, and the smallest next action. For each claim/check
record result, provenance/boundary, limitations and `evidence_level`:

- `STRUCTURAL`: identify source inspection, schema check or compilation performed.
- `SYNTHETIC_RESULT`: distinguish local oracle arithmetic, compiled SQL execution
  and selected-engine fixture execution.
- `DEPLOYED_DATA`: identify actual sources/output, artifact and common boundary.
- `NOT_RUN`: explicit absent evidence, not a fourth proof level.

A deployed result for one measure does not promote other claims. List untested
scope. Owner confirmation is a semantic decision, not a data test. A conversational
turn only needs its relevant restatement/question; do not force a full report
after every answer.

## Learn without relaxing constraints

At a meaningful checkpoint capture an observed missing, misleading or unnecessary
procedure. Within task authority, amend the smallest workflow/knowledge instruction
and repeat the affected acceptance check. Outside that authority, propose it.
Changes to business meaning, hard constraints, approval authority or layer
boundaries need the relevant owner's decision even if placed in a skill file.
Classify by effect, not file type. Preserve historical evidence; keep local
incidents in project context and reusable lessons in the package. No automatic
upstream publication or mandatory new retrospective interview.
