# Daana

Model your business, generate the warehouse, and let your agent walk it: skills for declaring, building and verifying a Daana data platform.

Requires a separately installed Daana CLI and project-local bindings.
No credentials, CLI executable, hooks or MCP servers are bundled.

User-authorized workflows may read and store personal or business data through
the project's configured source APIs and warehouses, using local CLI tools.
These external services are not bundled connectors. The host model/provider
may process supplied files and tool results; Daana operates no plugin backend
that receives or retains them. See [data handling](docs/plugin-data-handling.md).

This is a generated distribution. Edit the canonical source in
[daana-skills](https://github.com/daana-code/daana-skills), then rebuild;
do not maintain a second editable copy here.

Install in a Claude Code session:

```text
/plugin install daana --marketplace daana-code/daana-plugin
```

Start with [installation and setup](docs/plugin-usage.md).
For distribution see [marketplaces](docs/plugin-marketplaces.md).
Read the [release scope](docs/release-notes.md) and
[data handling and support](docs/plugin-data-handling.md).
Plugin code, skills and documentation use the [MIT License](LICENSE);
the separately distributed Daana CLI retains its own license.
Canonical workflow and role files are included unchanged. Native entrypoints
are generated bindings, not independent manuals.
