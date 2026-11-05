# Shared analytical guidance

## File organization

The full collection is the install unit. Skills live once under
`.agents/skills/{shared,ingestion,das,dab,dar}/`; canonical roles live once under
`.agentic/agents/`. Codex TOML and Claude Markdown registrations are thin loaders.
Claude skill aliases are relative directory symlinks into the same skill tree.
No editable copies, reference synchronization or global installation changes.

Plugin releases generate flat `skills/` entrypoints and Claude `agents/` bindings
from these same sources. They explicitly load the shared router and canonical
files; they contain no second workflow manual. Root `plugin.json` owns release
metadata. `scripts/package_plugins.py` checks generated drift and exports the
dependency-closed payload. Codex plugin installation does not register project
TOML agents. See [plugin usage](../docs/plugin-usage.md).

The root and layer instruction files own constraints; knowledge explains them;
skills own task workflows. Project bindings live only in the task repository's
explicitly bound `project-context.md`, indexed by the
[binding contract](../.agents/skills/shared/references/project-bindings.md).
Resolve a skill's relative dependencies from its canonical symlink target.

Ship recurring useful workflows with cold discovery/application evidence. Do not
invent RED results or claim causal improvement without a baseline. Keep failed,
partial and omitted observations in the review record. A boundary change updates
its instruction in the same PR. Specialist roles stay thin, not duplicate manuals.

## Runtime evidence and reviewer launches

Historical evidence on Codex 0.153.0 and Claude Code 2.1.278/2.1.280 supports
scoped local useful tasks, shared references and role loading. It is not a new
claim for the consuming repository or current client version. See
[provenance](../PROVENANCE.md) for exact source and original review records.

- Codex skills: router-following and no-router-row tasks were observed; direct
  reads are not automatically native catalogue events.
- Claude skills: catalogue/Skill calls through flat aliases were observed;
  canonical-target link resolution is mandatory. Some runs omitted required
  workflow reads; useful results do not establish full instruction compliance.
- Reviewer: freshness, independent evidence and effective read-only controls
  remain mandatory. A native role name or prohibition is not enforcement.
- Codex reviewer support is **manual-only** on the tested version: a separate
  fresh `codex exec --sandbox read-only -c 'approval_policy="never"'` session,
  manually loading the canonical reviewer. This launch denied parent/helper
  writes in the recorded controls. Native restricted reviewer enforcement is
  NOT_PROVEN; the tested workspace-write parent override is unsupported.
- Claude native reviewer exposed only Read/Grep/Glob and denied edits, shell and
  delegation. Shell verification is NOT_RUN through that role, not implicitly
  available. Do not expand tools or use writable delegation to bypass it.
- Report role activation from launch metadata; without it report UNKNOWN.
- Production-access isolation is NOT_PROVEN and its replacement test NOT_RUN,
  explicitly outside the accepted release scope. No real-binding isolation claim
  or permission to run such a test follows from copying the package.
- Grok has historical router-only evidence. Windows, new native adapters and
  new client/runtime combinations remain untested. Windows needs symlink support.

Verify actual launch restrictions before reviewer dispatch. Stop that dispatch
if they cannot be established; continue independent permitted work. A later
native-support claim needs its own selection and edit/shell/delegation controls.
These local results grant no warehouse authority or deployed-data verdict.
