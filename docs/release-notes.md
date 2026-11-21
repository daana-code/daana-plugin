# Release notes

## 0.1.2

- Dependency wording distinguishes the project generator and Dataform used by
  DAS from Daana CLI, required for DAB and DAR execution. Ingestion uses its
  project-bound acquisition tools.
- Installation commands live in the usage guide. The generated public README
  shows the same GitHub marketplace commands, copied from the guide at packaging
  time, and the marketplace guidance links to it. The in-session
  `/plugin install` form is no longer shown.
- Installation tested on 2026-11-21 on macOS with Claude Code 2.1.325 and
  codex-cli 0.171.0 in empty client homes: the GitHub route against public 0.1.1
  and against a local Git copy of the 0.1.2 archive, both release pins, and the
  archive route in both clients. Claude Code pins a release with
  `daana-code/daana-plugin#<release-tag>` (it has no `--ref` flag); Codex keeps
  `--ref <release-tag>`. The earlier GitHub-route runs on fresh Linux containers
  with Claude Code 2.1.318 and Codex CLI 0.167.0 against public 0.1.1 are kept.
  Results, success lines and limits are in the
  [dated records](plugin-install-verification.md).
- First-use guidance routes tutorial readers to existing model, mapping and
  reviewer workflows and supplies a minimal project-binding starter.
- Reviewer guidance separates confirmed defects from unverified runtime concerns;
  non-Git Codex launch guidance identifies the conditional repository-check flag.
- Public release guidance omits internal approval history. These documentation
  corrections do not claim that required reading volume has been reduced.
- Tutorial chapter links and the release-pin routes for both clients are
  included; the tag for this release is set at publication. The generated
  README directs feedback to public issues rather than asking readers
  to edit a private repository.
- Guidance follows the Daana CLI 1.0 release candidate. The DAR local lane uses
  the public `dar apply --dry-run` plan and `dar generate --preview` SQLX instead
  of the hidden `dar compile`, and the descriptions of `running-dar-operations`
  and `validating-dar-structure` name dry-run plans and previews instead of
  compile. DAB completion checks count skipped runs, which end `row_st = 'S'`.
  Operations guidance identifies the CLI as one `daana` executable, and the
  authoring reference names root `daana check` and the atomic context.
- Tutorial guidance uses the binding that `daana init --example bookstore`
  writes and describes chapter 5 as a mapping task. Plugin problems go to public
  issues; help goes to the community Slack, then support@daana.dev. Layer names
  use "Data according to System / Business / Requirements".

## 0.1.1

- MIT licensing for plugin code, skills and documentation. The separately
  installed Daana CLI retains its own license.
- Existing 512×512 Daana icon included in both deterministic archives and both
  clients' listing metadata.
- Source-led DAB drafts from typed tables follow the same candidate boundary as
  legacy reconstruction: coherent model and mappings outside selected runtime
  configuration until their meaning is approved.
- Completion reports retain the distinction between observed facts, inferred
  meanings and owner-approved decisions, including in the final summary.
- Validation guidance records warnings and uses digests for ignored inputs;
  scratch work uses a new task-local directory.

The package remains 21 skills and six canonical roles. No new workflow, engine
capability, scheduler or automatic installation mechanism is introduced.

GitHub distribution and public-directory acceptance are separate. A GitHub release
does not establish an approved OpenAI or Anthropic listing.

## Compatibility and evidence scope

Daana CLI is an external prerequisite for DAB and DAR execution; DAS uses the
project's generator and Dataform. Bind actual tools and supported commands per
project; plugin installation neither installs nor upgrades them.
Prior bookstore trials used Daana CLI 0.7.3 with Focal CLI 0.7.1 and exercised
local DAB authoring and validation. They did not test warehouse deployment.
Their recorded failures remain evidence for the corrections above, not retroactive
passes for this candidate.

On 2026-11-21 the CLI commands this guidance names were run on a macOS arm64
build of Daana CLI commit `18a10c29` (the 1.0 release candidate; `daana --version`
reports `v1.0.0-rc.1-rehearsal.4-118-g18a10c29`), against the bookstore tutorial
project on DuckDB with an empty home directory. At checkpoint ch5: root
`daana check`, `check model`, `check mapping --skip-schema-validation`,
`check workflow`, `install`, `deploy` and two runs of `execute`; the second run
ended its skipped runs `row_st = 'S'`. At checkpoint ch7: `dar check`, `dar lint`,
`dar apply --dry-run --dialect duckdb`, and `dar generate --preview` on a document
without output checks. All exited 0. The refusals the guidance describes were
observed too: a dry run without a dialect, and `dar generate` on documents with
output checks. `dar apply` on a deployed DAB and Dataform execution were not run.
In one authenticated Claude Code session with the 0.1.2 candidate installed from
the archive, `/daana:running-dab-operations` ran `daana check` on the bookstore
project after reading the router and workflow; the same request without the
skill name used no Daana skill. See the
[installation records](plugin-install-verification.md).

**DAR execution remains experimental and untested in those trials.** It needs a
DAR-capable Daana artifact. The presence of DAR skills does not establish that the
installed binary supports them or that generation, apply or reconciliation passed.

Claude Code plugin skills and role bindings, Codex plugin skills, and manual
Codex role use are distinct support claims. Codex plugin installation does not
register native specialist agents. Independent Codex review retains the manual
read-only launch scope documented in the
[shared guidance](../.agentic/README.md#runtime-evidence-and-reviewer-launches).
No client-install result certifies sandbox enforcement, production isolation,
ChatGPT desktop support or public marketplace acceptance.
