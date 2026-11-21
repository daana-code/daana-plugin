# Install and use Daana

Daana is the plugin ID in both clients. It provides 21 workflows spanning
interviews, ingestion, DAS, DAB and DAR, plus six canonical specialist roles.
It is a local developer plugin for working with **Daana CLI**, not a replacement
for that executable or a hosted warehouse service.

## Prerequisites

1. For DAB and DAR execution, install the Daana CLI artifact selected by your
   project using its official distribution instructions. Record its path/version
   or digest and supported commands in project context. DAS skills use the
   project's own generator and Dataform, not a Daana CLI `das` command; ingestion
   uses the project's acquisition tools. Do not assume tools or capabilities from
   another project.
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

## Install from the public GitHub marketplace

Official Anthropic or OpenAI directory acceptance is not required for this route.
The public repository supplies both marketplace catalogs; `daana@daana` selects
plugin `daana` from Daana's marketplace.

Claude Code, from a terminal:

```sh
claude plugin marketplace add daana-code/daana-plugin
claude plugin install daana@daana
claude plugin list
```

Codex, from a terminal:

```sh
codex plugin marketplace add daana-code/daana-plugin
codex plugin add daana@daana
codex plugin list --json
```

These commands install the repository's current default-branch package. Start a
fresh client session after installation, then invoke a skill by name. For a fixed
release, pin it as below or use the archive route.

On 2026-11-21 these commands were tested on macOS (arm64) with Claude Code 2.1.325
and codex-cli 0.171.0, each client in an empty home without sign-in. Against the
public repository they installed 0.1.1. Against a local Git copy of the repository
with the 0.1.2 archive committed on its default branch and tagged, the same
commands installed 0.1.2 with 21 skills, and both pin forms below selected their
tag. Read the [dated records](plugin-install-verification.md). They prove
installation, not that an agent selects a skill without being asked.

On 2026-11-10 the same routes were verified for 0.1.1 with Claude Code 2.1.318
and Codex CLI 0.167.0, each in a fresh Linux/aarch64 container without
credentials or prior plugin state. Both installed public commit
`1e1f7fae759ab58c29ceae4e9d7f81a3072e2924` and reported the plugin enabled.

### Pin a release

Instead of the default-branch marketplace-add command, use the one for your
client:

```sh
claude plugin marketplace add daana-code/daana-plugin#<release-tag>
codex plugin marketplace add daana-code/daana-plugin --ref <release-tag>
```

`<release-tag>` is a placeholder: the tag of this release is set when the release
is published. Then use the same install and inventory commands above. Claude Code
has no `--ref` flag; it reads the tag after `#`, and `@<release-tag>` also works.
Codex takes `--ref`. Codex records the ref in its `config.toml`, not in
`codex plugin list --json`. A tag selects that release only, not a later one.
On 2026-11-21 both forms selected tag `v0.1.1` on the public repository and
`v0.1.2` on the local copy. On 2026-11-10, the independent documentation review
for the Daana CLI 1.0 release candidate verified `--ref v0.1.1` with Codex
0.167.0.

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

On 2026-11-21 this route was tested in both clients with the 0.1.2 release
candidate archive: `SHA256SUMS` matched, `claude plugin validate --strict` passed,
and the persistent install commands above installed 0.1.2 with 21 skills in each
client. `claude --plugin-dir` was not part of that test.

Restart the client after installation. If its CLI lacks installation commands,
use the client plugin directory UI with the added marketplace, or update the
client. A catalog entry is not evidence that installation succeeded.

These commands intentionally modify that user's plugin configuration. They are
not commands an agent should run implicitly while answering an unrelated task.
For an empty installation test, use a fresh container with no host home or
credentials mounted, or an empty client home without credentials, as in the
recorded tests. A disposable container has its own home directory. On macOS an
empty home does not isolate the login Keychain; the recorded macOS test blocked
Keychain access. On a shared workstation, isolate client configuration rather than
changing the real user's home or account/project defaults. An empty configuration
tests installation; authenticated model use is a separate check.

## Bind a project

The plugin's shared [binding contract](../.agents/skills/shared/references/project-bindings.md)
defines the context sections. Keep one searchable context document in the project;
its filename need not contain a company name. At minimum, the task-root `AGENTS.md`
must explicitly point to it and require its operational restrictions before any
external work. Bind actual model/contract paths, commands, selected tools, identity,
approval owners and unavailable/parked surfaces. Configuration stays authoritative.

The tutorial project already has its binding (see
[First tutorial or small model change](#first-tutorial-or-small-model-change)).
For your own project, neither `daana init` nor the plugin's installation creates
one: ask the agent to prepare it using the repository and the starter below.
No dedicated setup skill is claimed. Review the discovered paths and unresolved
fields before using them; an absent binding is not permission to probe a warehouse. For a version-controlled project, commit
the agreed binding. A disposable tutorial directory does not need a Git repository
just to have a binding.

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

## First tutorial or small model change

Use the tutorial's current project and checkpoint as inputs.
`daana init --example bookstore` already writes the tutorial's `AGENTS.md` and
`project-context.md`, so the tutorial needs no binding step. Use the
[starter below](#minimal-local-project-starter) only for your own project.

In the Daana tutorial, [chapter 3](https://docs.daana.dev/docs/tutorial/03-structuring-logic)
is a useful first attribute change. [Chapter 5](https://docs.daana.dev/docs/tutorial/05-mastering-dmdl)
completes the order-line mapping from a scaffold: complete it with the agent
before you open a correct answer, then compare. Follow the chapter setup for
your installed CLI version and the [tutorial index](https://docs.daana.dev/docs/tutorial)
for current prerequisites and licensing guidance; this plugin does not grant a
CLI license.

Start with these existing routes; you do not need all 21 workflows:

1. **Author the model:** `authoring-dab-models` settles the changed entity,
   attribute or relationship and its time semantics. In Claude Code, invoke
   `/daana:authoring-dab-models`; in Codex, select the installed skill.
2. **Map the source:** `authoring-dab-mappings` binds that meaning to the available
   input. Keep the first task small, such as one well-defined attribute.
3. **Request independent review:** use the `data-platform-reviewer` role with
   fresh context and the [supported launch restrictions](../.agentic/README.md#runtime-evidence-and-reviewer-launches).
   It is a role, not another skill; Codex plugin installation does not register it
   natively. A review is a second opinion: distinguish demonstrated defects from
   checks that still need a run. Execute only after the operation is authorized.

You may be both the evaluator and the business owner. State that once in project
context; your explicit definition or decision counts without a second person.
Ownership alone does not authorize unspecified future writes. A useful first
result is a small model/mapping diff, its local validation and a clear next step.
This entry point does not claim that the current required reading chain has been
shortened or that model-session discovery was tested by the installation checks.

## Minimal local project starter

Ask the agent:

> Set up this existing project for the Daana plugin using local files. Preserve
> existing instructions. Draft the root binding and a minimal context from the
> configuration and installed-tool help. Mark unknowns; ask me only for intent,
> ownership or authorization that the files cannot establish. Do not open or
> modify the database during setup.

For a **local DuckDB evaluation only**, the following is a starting shape. The
agent fills it from the actual project; it is not a preconfigured connection or
permission grant. Cloud and additional-layer sections are added when relevant.
Do not copy the placeholders into an operation command.

Task-root `AGENTS.md` (merge into it if it exists):

```text
Project context: ./project-context.md.
Read its applicable bindings and Operational restrictions before project work.
Use the installed Daana skill entrypoint to load its shared router and workflow.
```

Task-local `project-context.md`:

```text
# Project context

## Coordinates and identity
- Workspace: <confirmed project directory>.
- Backend: local DuckDB; configuration/database: <discovered paths>.
- Invocation identity: <observed local user; no cloud identity assumed>.

## Operational restrictions
- Environment and meaning owner: <confirmed purpose and owner>.
- Current write authorization: none established by this starter.
- External/production access: none authorized by this local setup.
- Parked inputs or restrictions: <inspect project guidance; mark unknowns>.

## DAB bindings
- Model, mappings, workflow and connection config: <existing paths>.
- Definitions/question and source evidence: <existing files or missing inputs>.

## DAB offline commands and DMDL fields
- CLI path and version/digest: <verified local artifact>.
- Local checks and supported fields: <verified help/configuration references>.

## DAB evidence qualifications and refresh scope
- Executed checks and results: <observed results, or not run>.
- Refresh effects and runtime assumptions: <proved evidence, or unverified>.

## Warehouse bindings
- Local database and read/write scope: <resolved path and explicit authority>.
- Evidence location: <project-local output directory>.
```

Keep only applicable sections, link to existing configuration instead of copying
it, and leave secrets outside these files. Unknowns block only dependent work.
The starter must not be mistaken for established runtime evidence or approval.

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
