# Daana

Model your business, generate the warehouse, and let your agent walk it: skills for declaring, building and verifying a Daana data platform.

## Install

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

Start a fresh client session after installation. The
[installation guide](docs/plugin-usage.md) covers release pins, archives,
project binding and removal.

## About this package

DAS skills use the project's own generator and Dataform; Daana CLI is needed
for DAB and DAR execution. Each layer uses explicit project-local bindings.
No credentials, CLI executable, hooks or MCP servers are bundled.

User-authorized workflows may read and store personal or business data through
the project's configured source APIs and warehouses, using local CLI tools.
These external services are not bundled connectors. The host model/provider
may process supplied files and tool results; Daana operates no plugin backend
that receives or retains them. See [data handling](docs/plugin-data-handling.md).

This distribution is generated from Daana's private source repository.
For bug reports or proposed improvements, [open a public issue](https://github.com/daana-code/daana-plugin/issues).
Maintainers update
the canonical source and regenerate the package; do not maintain a second
editable copy here.

For distribution see [marketplaces](docs/plugin-marketplaces.md).
Read the [release scope](docs/release-notes.md) and
[data handling and support](docs/plugin-data-handling.md).
Plugin code, skills and documentation use the [MIT License](LICENSE);
the separately distributed Daana CLI retains its own license.
Canonical workflow and role files are included unchanged. Native entrypoints
are generated bindings, not independent manuals.
