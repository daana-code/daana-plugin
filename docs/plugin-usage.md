# Install and use Daana

Daana is the plugin ID in both clients. It provides 21 workflows spanning
interviews, ingestion, DAS, DAB and DAR, plus six canonical specialist roles.
It is a local developer plugin for working with **Daana CLI**, not a replacement
for that executable or a hosted warehouse service.

## Prerequisites

1. Install the Daana CLI artifact selected by your project using its official
   distribution instructions. Record its path/version or digest and supported
   commands in project context. Do not assume a version from another project.
2. Use a current Claude Code or Codex client. The packaging record identifies
   the versions tested; older clients are not automatically covered.
3. Supply your project's instructions and explicit context binding. Never copy
   another company's credentials, datasets, owners or business definitions.
4. Keep credentials in the client's approved external credential store. The
   plugin has no credential form, MCP server, startup hook or automatic installer.

Missing CLI prevents CLI execution, not useful offline interviews or model review.
Installing the plugin does not authorize any warehouse operation.

Read the [release scope](release-notes.md) for tested and untested capabilities.
DAR execution requires a DAR-capable artifact and remains experimental; the DAB
authoring trials do not establish DAR runtime support. See
[data handling and support](plugin-data-handling.md) before sharing sensitive inputs.

## Local installation

Unzip either supplied archive into a new directory. Both archives contain the
same portable payload and both client manifests; the filenames identify the
intended installation route. Check `SHA256SUMS` before extraction. No symlink
support is needed for these archives.

For a temporary Claude Code session, replace the illustrative path:

```sh
claude plugin validate --strict /absolute/path/to/daana
claude --plugin-dir /absolute/path/to/daana
```

For a persistent local Claude install:

```sh
claude plugin marketplace add /absolute/path/to/daana
claude plugin install daana@daana
claude plugin list
```

For Codex CLI versions with `plugin add`:

```sh
codex plugin marketplace add /absolute/path/to/daana
codex plugin add daana@daana
codex plugin list --json
```

Restart the client after installation. If its CLI lacks installation commands,
use the client plugin directory UI with the added marketplace, or update the
client. A catalog entry is not evidence that installation succeeded.

These commands intentionally modify that user's plugin configuration. They are
not commands an agent should run implicitly while answering an unrelated task.
For isolated testing, set `CLAUDE_CONFIG_DIR` or `CODEX_HOME` to a new temporary
directory for that invocation; do not copy credentials into the test directory.
Do not redefine `HOME` or change shared account/project defaults.

## Bind a project

The plugin's shared [binding contract](../.agents/skills/shared/references/project-bindings.md)
defines the context sections. Keep one searchable context document in the project;
its filename need not contain a company name. At minimum, the task-root `AGENTS.md`
must explicitly point to it and require its operational restrictions before any
external work. Bind actual model/contract paths, commands, selected tools, identity,
approval owners and unavailable/parked surfaces. Configuration stays authoritative.

Start by invoking a Daana workflow and asking it to prepare this binding for your
review, using only the repository. An absent binding is not permission to probe a
warehouse. Review and commit the local binding before external operations.

Every generated plugin skill entrypoint loads the bundled shared router and its
canonical workflow. A plugin's root `AGENTS.md`/`CLAUDE.md` is **not** automatically
loaded as project instructions. For always-loaded project routing, explicitly link
the installed shared router from project `AGENTS.md`; Claude projects can import
that project router from `CLAUDE.md`. Do not commit a personal cache path: use your
project's stable dependency mechanism, or keep host installation paths local.

Choose one active instruction distribution per project: the pinned full checkout
or the plugin. Do not enable both native skill catalogs and silently mix versions.
Projects that need reproducible automatic routing can keep the pinned-checkout
installation rather than depending on a mutable personal plugin cache.

## Skills and roles

Claude skills use names such as `/daana:authoring-dab-models`. In Codex select the
installed skill from its skills UI/catalog; confirm the displayed package/path if
another plugin exposes the same name. Explicit invocation is useful for a first
installation check; automatic selection needs its own observed evidence.

Claude exposes six `daana:` agents. Their generated bindings read the canonical
roles. The reviewer is limited to Read/Grep/Glob; shell tests through it are NOT_RUN.

Codex's plugin component model does not register these six agents. Their canonical
files and existing `.codex/agents/*.toml` project adapters are included, but copying
them into a plugin does not make them native agents. Use the shared router manually,
or explicitly configure project registrations through the reviewed full-checkout
route. Do not claim native activation from reading a file.

Codex independent review remains a fresh manual read-only session, approval
`never`, with effective restrictions checked before dispatch. Read the shared
[reviewer launch scope](../.agentic/README.md#runtime-evidence-and-reviewer-launches).
Plugin loading does not prove sandbox or production isolation.

## Updates and removal

Review the new version, update the marketplace, update/reinstall the plugin using
the installed client's help, and start a fresh session. Re-run one useful local
task against actual project bindings before trusting the update operationally.
For a rollback, install a retained reviewed version/catalog revision, not an edited
cache. Generated entrypoints are rebuilt upstream, never patched in client caches.

Uninstall with `claude plugin uninstall daana@daana` or
`codex plugin remove daana@daana`, then remove the marketplace if no longer needed.
Remove stale project links deliberately. This does not uninstall Daana CLI, delete
project models or revoke warehouse credentials.

See [distribution and marketplace submission](plugin-marketplaces.md) for team
and public release paths, including decisions still required before publication.
