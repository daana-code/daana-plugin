# Distribute Daana: catalogs and public directories

Checked against official documentation on 2026-11-06. Client catalogs, workspace
distribution and public directory listings are different release actions. None
has been published by building these packages. `daana` is our manifest ID, not a
claim that a public listing name has been reserved.

## Build and release checklist

In the source repository, with Python 3.11+ and development requirements installed:

```sh
python3 scripts/validate_adss.py
python3 scripts/package_plugins.py
python3 -m unittest discover -s tests -v
python3 scripts/package_plugins.py --output /absolute/path/to/new-release-directory
```

The output directory must not exist. It contains two deterministic ZIPs,
`SHA256SUMS` and a per-file `CONTENTS.json`. The archives contain the same payload;
each host chooses its manifest. The builder includes only the declared runtime
files, not the repository's history or review records.

The chosen distribution destination is
[`daana-code/daana-plugin`](https://github.com/daana-code/daana-plugin), created
privately on 2026-10-25 with owner authorization. On 2026-11-06 Siavoush authorized
completion of the release PR, clean public distribution and both portal
submissions. Populate it only from the reviewed archive, without importing source
history. `daana-code/daana-skills` remains the single editable source and stays private.
Portal acceptance is recorded separately from the GitHub release.

Release owner checks:

- Review the commit and checks, bump root `plugin.json`'s version when publishing
  an update, regenerate with `python3 scripts/package_plugins.py --write`, and
  review the generated diff. Never edit generated manifests or loaders separately.
- Test installation from the actual archive in each client and one useful task
  with the intended project's bindings. Static checks are not task evidence.
- Verify that the archive includes the [MIT License](../LICENSE) and that both
  manifests declare it. Siavoush selected MIT for the plugin on 2026-10-25;
  Daana CLI remains separately licensed. Retain contribution attribution.
- Approve publisher identity, support contact, privacy/terms URLs, branding and
  data-handling statements. Do not invent legal URLs or imply that warehouse
  queries never send data to a model/provider.
  The package's [data-handling page](plugin-data-handling.md) describes its
  behavior; it is not an invented legal policy. The OpenAI portal on 2026-11-06
  requested website, support, privacy and terms URLs for this skills-only package
  too. Use approved public pages and complete the fields the actual portal requires.
- Audit history and retained evidence before making any existing repository public.
  Internal workflows remain in old Git commits. Prefer a separately reviewed clean
  distribution repository populated from the archive, with attribution retained.
- Merge, tag, upload assets or publish only on explicit owner instruction. Keep
  the tested ZIP and checksums attached to the release, not just a moving branch.

## Team catalogs: no public store acceptance required

Both catalog files are generated: `.claude-plugin/marketplace.json` and
`.agents/plugins/marketplace.json`. They expose the root package as `daana@daana`.
An authorized user can add a reviewed Git repository/ref instead of a local path.
Once the reviewed release has populated the chosen distribution repository:

```sh
claude plugin marketplace add daana-code/daana-plugin
claude plugin install daana@daana
codex plugin marketplace add daana-code/daana-plugin --ref reviewed-tag
codex plugin add daana@daana
```

For private catalogs, recipients need repository access. Do not embed tokens in
catalog URLs. A clean export must keep both hidden manifest directories and the
entire payload, not just `skills/`. A catalog source is not a public listing.
See the [OpenAI package/catalog reference](https://developers.openai.com/plugins/build/plugins)
and [Claude marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces).

## Claude directory

The public submission route is the
[developer portal](https://claude.ai/directory/manage). Follow the current
[submission procedure](https://claude.com/docs/plugins/submit): connect a GitHub
account with push rights, select the repository and plugin folder/ref, validate
that exact commit, complete listing/data-handling/compliance fields, and submit
for review. Fix findings in source and revalidate. Approval and publication are
separate owner actions. A private repository can be submitted for review but must
be public before listing; do not flip this source repo's visibility casually.

The package's `.claude-plugin/plugin.json` lives at the root of the exported
repository, so the plugin path is the repository root. Directory validation has
requirements beyond `claude plugin validate --strict`, including release metadata
and licensing. Declare the local Daana CLI prerequisite and supported Claude Code
surface clearly; do not advertise web-only execution as tested.

Version 0.1.1 includes the website's existing 512×512 PNG brand asset, unchanged,
in both packages. The packager emits the same asset in Claude's `icon` field and
OpenAI's icon fields. Run `claude plugin validate ./<plugin-folder> --strict --profile directory`
before submission; portal checks still remain separate.

Listing in Anthropic's directory is not the same as inclusion in the curated
`claude-plugins-official` marketplace. The current
[publishing guide](https://code.claude.com/docs/en/plugins/publish) directs official
marketplace inclusion through the partner contact, not the directory portal.
Team catalogs remain a usable distribution route while a public listing is reviewed.

## OpenAI / Codex directory

Use the [plugin submission portal](https://platform.openai.com/plugins) and the
[submission guide](https://developers.openai.com/plugins/deploy/submission).
The publisher needs the required organization permissions and verified identity.
Choose the skills-only route and upload the tested Codex ZIP. Complete the real
publisher, policy, support and review information; submit, address findings, then
publish after approval. Keep submitted version/ZIP/checksums together. Updating
source is not itself a published directory update.

This plugin invokes a local executable. Its root manifest therefore declares
`extensions.com.openai.requires_local_executor: true`, as required by the
[desktop-only guide](https://developers.openai.com/plugins/deploy/desktop-only).
It bundles no MCP server; do not fabricate one to fit a submission form. If the
portal rejects that execution field or account eligibility, contact OpenAI with
the submitting organization ID. Local catalog installation remains separate from
public directory eligibility. We have not tested ChatGPT desktop or obtained
directory acceptance by proving Codex CLI installation.

## What this build does not authorize or prove

No public-name reservation, publisher verification, legal approval, marketplace
acceptance, repository-visibility change, production-access isolation or warehouse
operation follows from a passing package test. Those are explicit release or
project decisions. The package is installable without pretending they are complete.
