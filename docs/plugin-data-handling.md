# Data handling and support

Daana is an instruction package for Claude Code and Codex. It contains skills,
references and role bindings. It bundles no Daana executable, MCP server,
credential store, startup hook or telemetry service.

The host agent reads the files and tool results made available in the session.
Those contents can be processed by the host's model/provider under that product's
settings and terms. Installing this package does not make those interactions
offline or private to your machine. Review the host's controls before supplying
confidential information.

When authorized by the user, workflows can invoke separately installed tools,
including Daana CLI, source APIs and warehouse clients. Those tools use the
project's own credentials and can read or change external systems. The plugin
does not provision credentials or grant authority. Its instructions require
explicit project bindings, identity checks and authorization for warehouse writes;
instructions are not a substitute for the host's enforced permissions.

Daana CLI's own network use is described in its
[licensing guide](https://docs.daana.dev/docs/guides/licensing#what-daana-sends-home).
In the 1.0 release candidate, the CLI sends no usage data; it contacts the Daana
license service only as that guide describes.

Report plugin problems as a [public issue](https://github.com/daana-code/daana-plugin/issues).
For help, ask in the [Daana community Slack](https://join.slack.com/t/daanacommunity/shared_invite/zt-4eq45w9s2-8Bg3QsGY5~kTBa_RZV0u3A)
first, then write to [support@daana.dev](mailto:support@daana.dev). Include the
plugin version, host version, affected workflow and a sanitized reproduction. Do
not send credentials, customer rows, signed URLs or unredacted session logs.

This page describes the package's behavior. It does not replace the host's or
Daana CLI's terms, and it is not a claim of production-access isolation.
