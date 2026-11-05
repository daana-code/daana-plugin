# DAB completion report

Use these fields in the task artifact or PR handoff. Keep it concise, but do not
collapse distinct evidence levels into one green verdict.

For model/mapping authoring, state **mode: governed authoring or source-led
candidate**; identify legacy reconstruction as a subtype when applicable.
For a candidate, extend the existing source-support matrix
with source path/revision, documented meaning (and approval provenance if any),
observed implementation, inference and unresolved questions. Mark decisions as
candidate rather than approved; distinguish preserving legacy behavior from
proposing a correction. State where the model/mappings live outside the selected
workflow and what owner review and source/compiler checks promotion still needs.
Include the selected model in that unchanged boundary, not just the workflow.
Do not invent DMDL fields for these report labels. A completed draft is not an
approved model, executable mapping or deployed answer.

Keep observed facts, inferred meanings and owner-approved decisions distinct in
the final summary as well as the detailed matrix. Sample arithmetic, naming and
successful validation do not approve a business definition. A proposed
interpretation stays a hypothesis until the named owner confirms it; do not
silently shorten it into a fact in the handoff.

1. **Files and artifacts:** exact changed paths, YAML/diffs, support matrix,
   prediction/operation packet or verification findings. In committed documents,
   use repository-relative links; in GitHub PRs, use repository-relative path
   labels with commit-pinned repository links. In local handoffs to the user,
   use full local paths, including for scratch artifacts. Label scratch evidence
   as local-only rather than implying the PR reader can open it.
2. **Agent decisions:** what was decided within approved meaning and why, with
   supporting model/source evidence.
3. **Owner decisions:** specific questions, options, evidence and blocked scope.
4. **Structural evidence:** exact local commands/results and output inspection;
   name untested expression context or ignored-field limitations. Static-only
   mappings say: "Static checks passed; executability not established."
   Include warnings from stdout/stderr. Verify ignored inputs or plugin/binary
   preservation with before/after digests; a clean Git diff cannot prove that
   ignored files were unchanged.
5. **Synthetic-engine evidence:** scenario, artifact, generator and date, or NOT
   RUN. Reused evidence retains its original provenance and limitations.
6. **Deployment reconciliation:** population boundary, jobs and invariant results,
   or NOT RUN. Synthetic success is not a production verdict.
7. **Omissions and next action:** not-tested list, unresolved findings and safe
   continuation. A prepared authorization packet completes preparation, not the
   operation. A specific owner decision request can complete a blocked subtask.
