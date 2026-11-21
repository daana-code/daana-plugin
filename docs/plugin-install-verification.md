# Installation evidence

This is a dated observation record, not a second installation procedure. Follow
[plugin usage](plugin-usage.md) for maintained installation steps.

## 2026-11-21: macOS, public 0.1.1 and the 0.1.2 candidate

### Result and scope

Environment: macOS 26 (Darwin 25.2.0), arm64, with Claude Code 2.1.325,
codex-cli 0.171.0 and git 2.50.1. Every client command ran under `env -i` with
`HOME`, `CLAUDE_CONFIG_DIR` and `CODEX_HOME` in an empty directory, without
client sign-in, Git system configuration, SSH user configuration or prompts.
A sandbox profile refused Keychain access; Claude Code's Keychain lookups were
answered "not found". Official marketplace auto-install and the autoupdater
were off. The only network access was cloning
`github.com/daana-code/daana-plugin`.

The 0.1.2 candidate is the release candidate archive with SHA-256
`fca07c6e15e30069c4f293b75fefaef5205293a20bd8911949dad285c19641c6`. The
local Git copy is a clone of the public repository with that payload committed
on its default branch and tagged `v0.1.2`, tag `v0.1.1` kept. Git's
`url.insteadOf` sent the public URL to it, so the clients ran the unchanged
public commands.

| Test | Client | Result |
|---|---|---|
| GitHub route, public repository | Claude Code | exit 0 for each command; `daana@daana` 0.1.1 enabled at commit `1e1f7fae`, 21 skills, 6 agents |
| GitHub route, public repository | Codex | exit 0 for each command; `daana@daana` 0.1.1 installed and enabled, 21 skills |
| Pin `#v0.1.1`, public repository | Claude Code | exit 0; ref `v0.1.1`, commit `1e1f7fae` |
| Pin `--ref v0.1.1`, public repository | Codex | exit 0; source `https://github.com/daana-code/daana-plugin.git#v0.1.1`, `ref = "v0.1.1"` in `config.toml` |
| Pin `v0.1.2`, public repository | both | exit 1, as expected while the tag is unpublished |
| Archive route, 0.1.2 candidate | both | `SHA256SUMS` OK, the two archives' payloads identical, `claude plugin validate --strict` passed; 0.1.2 installed with 21 skills in each client, and 6 agents in Claude Code |
| GitHub route, local Git copy | both | the public commands installed 0.1.2 at the tagged commit, 21 skills |
| Pins, local Git copy | both | Claude Code's `#<tag>`, `@<tag>` and full-URL `#<tag>` forms and Codex's `--ref`, `@<tag>` and `#<tag>` forms selected their tag; neither client accepted a `file://` URL |

Claude Code has no `--ref` flag. Codex records a pinned ref in `config.toml`,
not in `codex plugin list --json`.

In one authenticated Claude Code session with the 0.1.2 candidate installed
from the archive and Daana CLI commit `18a10c29` on the bookstore tutorial
project, `/daana:running-dab-operations` loaded the skill, which read the shared
router and its canonical workflow and then ran `daana check` (exit 0). The same
request without the skill name used no Daana skill.

This is installation evidence on one machine with isolated client homes. It
does not establish automatic skill selection, specialist activation, sandbox or
production isolation, installation on Linux or Windows with these client
versions, publication of 0.1.2, or official-directory acceptance. The local
Git copy stands in for the published repository. The raw transcripts are kept
with the release record; they are not part of this package.

### Success lines

Claude Code. When its output is not a terminal, `marketplace add` first prints
progress lines; with a pin, the clone line ends `(ref: <tag>)`.

```text
✔ Successfully added marketplace: daana (declared in user settings)
Installing plugin "daana@daana"...✔ Successfully installed plugin: daana@daana (scope: user)
```

`claude plugin list` shows `daana@daana` with its `Version:` and
`Status: ✔ enabled`.

Codex prints a second line after each success line:

```text
Added marketplace `daana` from https://github.com/daana-code/daana-plugin.git.
Installed marketplace root: <home>/.codex/.tmp/marketplaces/daana
Added plugin `daana` from marketplace `daana`.
Installed plugin root: <home>/.codex/plugins/cache/daana/daana/<version>
```

## 2026-11-10: Linux containers, public 0.1.1

### Result and scope

Both exact GitHub marketplace routes passed with public distribution commit
`1e1f7fae759ab58c29ceae4e9d7f81a3072e2924`, version `0.1.1`.
Each client started with an empty plugin list, installed and enabled `daana@daana`,
and cached 21 skill entrypoints, 21 canonical workflows and six canonical roles.

| Client | Version | Marketplace add | Plugin install/add | Enabled inventory |
|---|---|---|---|---|
| Claude Code | 2.1.318 | exit 0 | exit 0 | `daana@daana`, 0.1.1 |
| Codex CLI | 0.167.0 | exit 0 | exit 0 | `daana@daana`, 0.1.1 |

Environment: two separate fresh Debian Bookworm Linux/aarch64 containers on
OrbStack, running as unprivileged uid 1000. The image contained Node.js, Git,
Python and the pinned clients. No Daana CLI was installed. Neither host home nor
client/warehouse credentials were mounted or passed into either container.
The sole bind mount was the read-only test runner; outbound network was available
for the public GitHub fetch. No client login or paid model invocation was used.
The recorded initial absence checks, mounts and environment names are below.

This is clean-container installation evidence, not a fresh physical machine test.
It does not establish native skill discovery during an authenticated session,
specialist activation, workflow quality, production-access isolation, macOS or
Windows installation, compatibility with the Daana CLI 1.0 release candidate,
or official-directory acceptance.
It tests the existing public 0.1.1 package, not publication of the proposed 0.1.2
wording correction. Six cached role definitions do not imply native Codex agents.

### Launch evidence

Environment values are deliberately omitted; the variable names and mount
restrictions suffice to identify the test setup without publishing secrets.

```json
{
  "image_id": "sha256:6297de1a79df38d01bdd36a88b952bea36c06332bff03c30fac43cba4641f491",
  "image_os": "linux",
  "image_architecture": "arm64",
  "containers": [
    {
      "name": "/daana-plugin-install-claude-20261110",
      "image_id": "sha256:6297de1a79df38d01bdd36a88b952bea36c06332bff03c30fac43cba4641f491",
      "user": "node",
      "working_dir": "/work",
      "entrypoint": [
        "python3"
      ],
      "args": [
        "/test/run_install.py",
        "claude"
      ],
      "environment_variable_names": [
        "PATH",
        "NODE_VERSION",
        "YARN_VERSION"
      ],
      "mounts": [
        {
          "type": "bind",
          "destination": "/test/run_install.py",
          "read_only": true,
          "source_kind": "one-off test runner"
        }
      ],
      "network_mode": "bridge",
      "privileged": false,
      "cap_drop": [
        "ALL"
      ],
      "security_opt": [
        "no-new-privileges"
      ],
      "memory_bytes": 1073741824,
      "nano_cpus": 2000000000,
      "exit_code": 0,
      "status": "exited"
    },
    {
      "name": "/daana-plugin-install-codex-20261110",
      "image_id": "sha256:6297de1a79df38d01bdd36a88b952bea36c06332bff03c30fac43cba4641f491",
      "user": "node",
      "working_dir": "/work",
      "entrypoint": [
        "python3"
      ],
      "args": [
        "/test/run_install.py",
        "codex"
      ],
      "environment_variable_names": [
        "PATH",
        "NODE_VERSION",
        "YARN_VERSION"
      ],
      "mounts": [
        {
          "type": "bind",
          "destination": "/test/run_install.py",
          "read_only": true,
          "source_kind": "one-off test runner"
        }
      ],
      "network_mode": "bridge",
      "privileged": false,
      "cap_drop": [
        "ALL"
      ],
      "security_opt": [
        "no-new-privileges"
      ],
      "memory_bytes": 1073741824,
      "nano_cpus": 2000000000,
      "exit_code": 0,
      "status": "exited"
    }
  ]
}
```

### Claude original command record

Captured stdout and stderr are preserved verbatim as JSON string values.

```json
{
  "started_at": "2026-11-10T10:27:14.100416+00:00",
  "client": "claude",
  "platform": "Linux-7.2.12-orbstack-00394-gbecdd6130068-aarch64-with-glibc2.36",
  "architecture": "aarch64",
  "uid": 1000,
  "home": "/home/node",
  "cwd": "/work",
  "config_absent_before": {
    "/home/node/.claude": true,
    "/home/node/.claude.json": true,
    "/home/node/.codex": true,
    "/home/node/.config/gcloud": true,
    "/home/node/.aws": true,
    "/home/node/.ssh": true,
    "/home/node/.gitconfig": true
  },
  "credential_or_config_override_env_names": [],
  "daana_cli_present": false,
  "runner_sha256": "33a0ab400f5216b27a7e48b4fd7a3315dcef262288925002067ebe214a059979",
  "commands": [
    {
      "argv": [
        "claude",
        "--version"
      ],
      "started_at": "2026-11-10T10:27:14.115606+00:00",
      "exit_code": 0,
      "stdout": "2.1.318 (Claude Code)\n",
      "stderr": ""
    },
    {
      "argv": [
        "claude",
        "plugin",
        "list",
        "--json"
      ],
      "started_at": "2026-11-10T10:27:15.001235+00:00",
      "exit_code": 0,
      "stdout": "[]\n",
      "stderr": ""
    },
    {
      "argv": [
        "claude",
        "plugin",
        "marketplace",
        "add",
        "daana-code/daana-plugin"
      ],
      "started_at": "2026-11-10T10:27:16.718285+00:00",
      "exit_code": 0,
      "stdout": "Adding marketplace\u2026SSH not configured, cloning via HTTPS: https://github.com/daana-code/daana-plugin.git\nRefreshing marketplace cache (timeout: 120s)\u2026\nCloning repository (timeout: 120s): https://github.com/daana-code/daana-plugin.git\nClone complete, validating marketplace\u2026\nCleaning up old marketplace cache\u2026\n\u2714 Successfully added marketplace: daana (declared in user settings)\n",
      "stderr": ""
    },
    {
      "argv": [
        "claude",
        "plugin",
        "install",
        "daana@daana"
      ],
      "started_at": "2026-11-10T10:27:18.611891+00:00",
      "exit_code": 0,
      "stdout": "Installing plugin \"daana@daana\"...\u2714 Successfully installed plugin: daana@daana (scope: user)\n",
      "stderr": ""
    },
    {
      "argv": [
        "claude",
        "plugin",
        "list",
        "--json"
      ],
      "started_at": "2026-11-10T10:27:19.133401+00:00",
      "exit_code": 0,
      "stdout": "[\n  {\n    \"id\": \"daana@daana\",\n    \"version\": \"0.1.1\",\n    \"scope\": \"user\",\n    \"enabled\": true,\n    \"installPath\": \"/home/node/.claude/plugins/cache/daana/daana/0.1.1\",\n    \"installedAt\": \"2026-11-10T10:27:18.848Z\",\n    \"lastUpdated\": \"2026-11-10T10:27:18.848Z\",\n    \"projectEnabled\": false\n  }\n]\n",
      "stderr": ""
    },
    {
      "argv": [
        "git",
        "-C",
        "/home/node/.claude/plugins/marketplaces/daana",
        "rev-parse",
        "HEAD"
      ],
      "started_at": "2026-11-10T10:27:19.513473+00:00",
      "exit_code": 0,
      "stdout": "1e1f7fae759ab58c29ceae4e9d7f81a3072e2924\n",
      "stderr": ""
    }
  ],
  "cached_payloads": [
    {
      "path": "/home/node/.claude/plugins/cache/daana/daana/0.1.1",
      "version": "0.1.1",
      "native_skills": 21,
      "canonical_skills": 21,
      "canonical_roles": 6,
      "manifest_sha256": "ee63a0141e14b8caea48336d4c7b4d27bd7e062911e13738dcc429009b27631d"
    },
    {
      "path": "/home/node/.claude/plugins/marketplaces/daana",
      "version": "0.1.1",
      "native_skills": 21,
      "canonical_skills": 21,
      "canonical_roles": 6,
      "manifest_sha256": "ee63a0141e14b8caea48336d4c7b4d27bd7e062911e13738dcc429009b27631d"
    }
  ],
  "finished_at": "2026-11-10T10:27:19.518444+00:00"
}
```

### Codex original command record

Captured stdout and stderr are preserved verbatim as JSON string values.

```json
{
  "started_at": "2026-11-10T10:27:15.296071+00:00",
  "client": "codex",
  "platform": "Linux-7.2.12-orbstack-00394-gbecdd6130068-aarch64-with-glibc2.36",
  "architecture": "aarch64",
  "uid": 1000,
  "home": "/home/node",
  "cwd": "/work",
  "config_absent_before": {
    "/home/node/.claude": true,
    "/home/node/.claude.json": true,
    "/home/node/.codex": true,
    "/home/node/.config/gcloud": true,
    "/home/node/.aws": true,
    "/home/node/.ssh": true,
    "/home/node/.gitconfig": true
  },
  "credential_or_config_override_env_names": [],
  "daana_cli_present": false,
  "runner_sha256": "33a0ab400f5216b27a7e48b4fd7a3315dcef262288925002067ebe214a059979",
  "commands": [
    {
      "argv": [
        "codex",
        "--version"
      ],
      "started_at": "2026-11-10T10:27:15.307073+00:00",
      "exit_code": 0,
      "stdout": "codex-cli 0.167.0\n",
      "stderr": ""
    },
    {
      "argv": [
        "codex",
        "plugin",
        "list",
        "--json"
      ],
      "started_at": "2026-11-10T10:27:17.444968+00:00",
      "exit_code": 0,
      "stdout": "{\n  \"installed\": [],\n  \"available\": []\n}\n",
      "stderr": ""
    },
    {
      "argv": [
        "codex",
        "plugin",
        "marketplace",
        "add",
        "daana-code/daana-plugin"
      ],
      "started_at": "2026-11-10T10:27:18.148733+00:00",
      "exit_code": 0,
      "stdout": "Added marketplace `daana` from https://github.com/daana-code/daana-plugin.git.\nInstalled marketplace root: /home/node/.codex/.tmp/marketplaces/daana\n",
      "stderr": ""
    },
    {
      "argv": [
        "codex",
        "plugin",
        "add",
        "daana@daana"
      ],
      "started_at": "2026-11-10T10:27:19.264855+00:00",
      "exit_code": 0,
      "stdout": "Added plugin `daana` from marketplace `daana`.\nInstalled plugin root: /home/node/.codex/plugins/cache/daana/daana/0.1.1\n",
      "stderr": ""
    },
    {
      "argv": [
        "codex",
        "plugin",
        "list",
        "--json"
      ],
      "started_at": "2026-11-10T10:27:19.378072+00:00",
      "exit_code": 0,
      "stdout": "{\n  \"installed\": [\n    {\n      \"pluginId\": \"daana@daana\",\n      \"name\": \"daana\",\n      \"marketplaceName\": \"daana\",\n      \"version\": \"0.1.1\",\n      \"installed\": true,\n      \"enabled\": true,\n      \"source\": {\n        \"source\": \"local\",\n        \"path\": \"/home/node/.codex/.tmp/marketplaces/daana\"\n      },\n      \"marketplaceSource\": {\n        \"sourceType\": \"git\",\n        \"source\": \"https://github.com/daana-code/daana-plugin.git\"\n      },\n      \"installPolicy\": \"AVAILABLE\",\n      \"authPolicy\": \"ON_USE\"\n    }\n  ],\n  \"available\": []\n}\n",
      "stderr": ""
    },
    {
      "argv": [
        "git",
        "-C",
        "/home/node/.codex/plugins/cache/daana/daana/0.1.1",
        "rev-parse",
        "HEAD"
      ],
      "started_at": "2026-11-10T10:27:19.430103+00:00",
      "exit_code": 0,
      "stdout": "1e1f7fae759ab58c29ceae4e9d7f81a3072e2924\n",
      "stderr": ""
    }
  ],
  "cached_payloads": [
    {
      "path": "/home/node/.codex/plugins/cache/daana/daana/0.1.1",
      "version": "0.1.1",
      "native_skills": 21,
      "canonical_skills": 21,
      "canonical_roles": 6,
      "manifest_sha256": "ee63a0141e14b8caea48336d4c7b4d27bd7e062911e13738dcc429009b27631d"
    }
  ],
  "finished_at": "2026-11-10T10:27:19.431349+00:00"
}
```
