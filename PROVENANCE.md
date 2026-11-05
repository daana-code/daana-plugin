# Collection provenance

Transfer input: `dosemedbox/analytics` commit
`d9982cdbab7c2013c93bf5c0db0ee096bd61630d`, merged PRs 44 and 45, 2026-09-22 UTC.
Promotion prepared 2026-09-23. This file records origin, not consumer bindings.

At transfer commit `84766e312bd566885073513e92e8e1cbd15d5af3`, all 21 skill
bodies, their reference files, six role bodies, twelve registrations, architecture,
playbook and layer knowledge were copied without content changes.
Packaging adaptations: shared root resolves the task-root context; ingestion
instruction routes use bound active/retired components instead of donor paths;
DAS's project-specific parked-action wording becomes bound restricted actions.
The organization note is a portable summary with the original support limitations.
None changes the twelve root safety rules or establishes new runtime behavior.

Lars Fredholm's selected contributions from `daana-code/adss-template` PR 19
(`3d1661f1a79124fbc9650bbbcabd5c6f0eb01fd5`) were consolidated and reviewed in
PR 44. Attribution includes consumer-query guidance, physical DAB lineage,
cross-layer diagnosis and pattern-scoped USS procedures. Rejected generalizations
were not imported. PR 19 is not closed or merged by this transfer.

The 2026-10-11 follow-up adds bounded legacy reconstruction to the existing DAB
model/mapping workflows, with one linked reference and coherent router/playbook
wording. It adapts the useful source-backed first-iteration intent discussed with
Lars, not the demo's complete modelling rules or coupled ingestion commands.
It adds no skill/role and does not claim that repeated success on one demo proves
generality. Canonical role-target checks also address Peiman's packaging review.
Neither addition alters runtime models, mappings, twelve root safety rules or
the historical client-support qualifications.

Historical review/evidence (private source access may be required; the collection
does not depend on access to these records to run):

- [Contribution disposition](https://github.com/dosemedbox/analytics/blob/d9982cdbab7c2013c93bf5c0db0ee096bd61630d/docs/superpowers/specs/2026-09-22-agent-harness-consolidation-design.md)
- [Phase-2 evidence and accepted limitations](https://github.com/dosemedbox/analytics/blob/d9982cdbab7c2013c93bf5c0db0ee096bd61630d/docs/superpowers/plans/2026-09-22-harness-tool-independence.md)
- [Explicit release scope and merge authority](https://github.com/dosemedbox/analytics/pull/45#issuecomment-5784950779)

The official collection becomes the editable upstream only after owner-authorized
merge. Candidate consumer pins are review dependencies, not a claim that the
source project's installed package has already been replaced. Each consumer
cutover is recorded separately; personal installations are untouched.

Release icon `assets/daana-icon.png` is an unchanged copy of
`public/android-chrome-512x512.png` from Daana's website repository, `daana-code/daana-web`,
commit `014eaf17991b7cf22d2f90a2ffb73bed82243958`. It is the existing 512×512
brand icon, not a newly generated mark. It is used only as an image in the plugin
manifests; no bundled script or hook executes it. MIT was selected for the plugin by
Siavoush on 2026-10-25; separately distributed executables retain their own licenses.
