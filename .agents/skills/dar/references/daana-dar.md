# Daana DAR: applicability and command boundaries

Use for Daana-generated DAR only. Elicitation is compiler-independent; this
compiler expects Daana DAB/a0 metadata, not an arbitrary entity warehouse.
Resolve the selected artifact, config, source/schema owners and observed
capabilities through **DAR compiler and operation bindings** and **DAR evidence**
in the task project's [context](../../shared/references/project-bindings.md).
Version labels, source checkout HEAD and executable hashes are different evidence.

## Resolve before authoring

Read the selected executable's help and its matching schema/source/tests where
available. Recognition of a kind or field does not prove every combination,
dialect, emitted constraint or runtime behavior. Never invent a field from a
donor's draft schema. Recheck when the executable, schema, backend or layout changes.

Bind the input, DAB model, workspace, output location, dialect and backend.
Check how the selected command finds its model: ancestor search does not resolve
a sibling model merely because the repo contains one. A supported co-located
fixture proves that layout only. Do not create a second editable model, relocate
DAB or patch the compiler inside an authoring task to hide a binding gap.

Read the complete emitted plan: workspace targets and flags are intentions,
not proof of resolved source/target coordinates. Check each object's qualified
name and read dependencies before interpreting or executing it. A target mismatch
blocks that deployment, not structural investigation of the generated result.

## Local structural lane

After verifying these forms on the selected artifact, bind `DAR_BIN`,
`DAR_CONFIG`, `DAR_INPUT`, `DAR_OUT`, `DAR_DIALECT` and `DAR_BACKEND` from task
context. Use an explicit nonsecret config and fresh local output directory;
inspect ambient overrides without exposing their secret values. Do not borrow
another client's global config. A scratch `{}` config can be sufficient for
offline work only where that behavior has been verified.

```bash
"$DAR_BIN" --config "$DAR_CONFIG" --no-tui dar check "$DAR_INPUT" --format json
"$DAR_BIN" --config "$DAR_CONFIG" --no-tui dar lint "$DAR_INPUT" --format json
"$DAR_BIN" --config "$DAR_CONFIG" --no-tui dar compile "$DAR_INPUT" --dialect "$DAR_DIALECT" --backend "$DAR_BACKEND" --out "$DAR_OUT" --format json
```

Capture stdout, stderr, exit and invocation; compile once per candidate/configuration,
then inspect the saved plan and all emitted files. Do not keep recompiling to
view another section. Avoid an output directory containing stale generated objects.
If the output set changes, prove file ownership and non-reproduction before
proposing removal under the project's deletion authority; do not delete by glob.

`check` checks shape/graph; `lint` adds public-description checks; offline
`compile` resolves the local model and emits a plan. They do not validate live
DAB column existence, actual values, approved definitions or materialized grain.
Inspect emitted checks: an accepted `checks` property is not evidence that
assertions were emitted or executed. Likewise description presence is not meaning.

## Connected catalog and warehouse analysis

Keep these separate from the credential-free lane. On the inspected command
family, an explicitly supplied connection flag selects connected compilation;
even an empty flag can change the path. Do not add flags as decorative defaults.
Inspect the exact selected command's effects, including inner CLI/catalog access.

Connected compilation obtains the warehouse catalog through the configured
client. It needs scoped identity/access and does not itself prove values or
temporal cardinality. Warehouse SQL analysis has its own costs/prerequisites;
use [querying warehouse](../../shared/querying-warehouse/SKILL.md) for that work.
Missing schema/catalog is not permission to install or reset the substrate.

Review published output names and schema, not just the SELECT body. Duplicate
output aliases can pass query analysis while CREATE VIEW rejects them. Prepare
the appropriate object-shape check; never silently create a temporary object
under a read-only authorization.

## Operation boundary

`dar apply` is a warehouse mutation: metadata persistence plus published-object
creation. Confirm the selected install/catalog mode and connection. An outer
CLI delegating the connection to an inner executable does not make it read-only.

Do not infer safety from `--dry-run`. Inspect and qualify the exact command,
artifact and flags; evidence about a different command's dry-run behavior is
not transferable. Where supported, an offline plan can aid preparation but
does not authorize apply, prove target readiness or estimate every runtime cost.

Prepare an exact invocation from current help and resolved bindings, not a
copied global default. Check emitted coordinates against the authorized targets.
Use [running DAR operations](../running-dar-operations/SKILL.md) before any
mutation. Reinstall, reset, refresh, retry and recovery are not implicit side
tasks; their scope and approval must be explicit.

## Temporal and capability inspection

Inspect emitted partition/order expressions, tie behavior and interval endpoints.
An inclusive SCD2 end computed as next-start minus one microsecond differs from
a half-open interval; tests must match the representation. Do not normalize it
by hand-editing output or assume it solves source-time ambiguity.

Describe unsupported requirements as compiler feedback with minimal input,
expected semantics and observed output. Preserve business meaning; do not
replace the approved grain with a shape the emitter happens to accept. Distinguish
repository/source inspection, local generated output, synthetic execution and
actual warehouse results in the [completion report](analytical-design.md#completion-evidence).
