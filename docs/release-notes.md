# Release notes

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

Daana CLI is an external prerequisite. Bind the actual executable and supported
commands per project; plugin installation neither installs nor upgrades it.
Prior bookstore trials used Daana CLI 0.7.3 with Focal CLI 0.7.1 and exercised
local DAB authoring and validation. They did not test warehouse deployment.
Their recorded failures remain evidence for the corrections above, not retroactive
passes for this candidate.

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
