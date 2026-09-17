# Phase Lifecycle And Completion

Execution Plan's Status column is the authority for phase state. Before each transition, root confirms the recorded prior state and the evidence for the next state.
Update that phase row, affected Current State fields, Progress Log, and Next Actions together in the [ledger](progress-template.md). Read back under its Field Rules
before dependent work. Describing a transition in prose does not perform it. On write or readback failure, reconcile durable state before continuing.

## Transitions

| State | Meaning and next transition |
| --- | --- |
| Pending | Dependencies satisfied: enter In Progress before work. |
| In Progress | Execution and ownership release pass: enter Done. |
| Done | Enter In Review before acceptance validation or verifier launch. |
| In Review | Acceptance evidence passes: enter Accepted. Candidate corrections return to In Progress. |
| Accepted | Phase acceptance criteria passed. |
| Blocked | Record cause and prior activity; resume that activity after resolution, never jump directly to Accepted. |
| Not Applicable | Phase removed consistently with current scope after resolving ownership, writes, and obligations; record the reason and checkpoint. |

Read-only discovery may move directly from `In Progress` to `In Review`. An active phase cannot be discarded while ownership, writes, or obligations remain unresolved.
Resolve those first, then record `Not Applicable`. Any retained deliverable changes must meet their applicable acceptance obligations.

Acceptance requires mapped requirements, all recorded phase verification obligations across its assignments, released writers, and current candidate evidence where
applicable. Reopen an accepted phase to In Progress before affecting accepted behavior; use In Review for evidence-only reevaluation. Each phase closes through the
procedure below.

## Mandatory Phase Commit

At the end of every phase, commit that phase's accepted deliverable changes, including applicable design updates, and the current run's ledger before dependent work
starts. Include a specification created for the run or explicitly requested source edits where applicable. Compare the specification with its recorded content identity
and user-authorized edits; reconcile unauthorized or unexplained changes before closure. Inspect tracked and untracked files and stage only authorized paths, explicitly
including the ledger if ignored.

Exclude unrelated changes, other runs' records, pre-existing staged content, active writers' files, and other phases' unaccepted deliverable changes, even after ownership
release. Preserve the user's index and worktree. Root serializes ledger updates and checkpoint creation so concurrent phases cannot mutate the snapshot being committed.
If the accepted delta cannot be isolated safely, block closure.

Skip only with `Skipped: no task-owned changes` or `Skipped: no Git repository`, after checking the relevant condition for this checkpoint's scope. Never create an empty
commit. Evaluate changes after preparing required closure records; do not manufacture timestamp-only updates for an already closed phase. Missing Git executable,
identity, permissions, failing hooks, or a commit prohibition is a blocker, not absence of a repository. Do not change Git configuration, disable hooks, or push to satisfy
the gate.

## Close And Compact

Record `Accepted` after acceptance evidence passes, or `Not Applicable` after the removal conditions above are met. Include the phase outcome or removal reason, evidence,
released ownership, and next actions, preserving the detailed Progress Log. Commit that snapshot with the phase's accepted delta, identifying the run and phase in the
commit message. Closure requires both the disposition record and its verified commit, unless a skipped disposition applies. The ledger need not store its own commit
hash; use Git history to locate the committed phase record on resume.

Do not release dependencies on a failed or uncertain commit. Record the error and resume from the last verified checkpoint. Reuse a successful checkpoint after an
interruption; revalidate deliverable changes made by hooks before accepting them.

After confirming the phase commit, replace that phase's log entries with exactly one summary row, then read back before starting any dependent phase. Without Git, compact
after confirming the phase's acceptance or removal evidence and skipped disposition. A verified no-change closure may reuse its existing summary. Independent phases
already running may continue; root serializes log edits.

The summary identifies the phase, outcome, candidate, commit or skipped disposition, essential verification evidence, agent dispositions, and carried risks. Its Evidence
/ Result cell obeys the 500-character limit in the progress template. Keep unresolved obligations in the ledger's Active contracts or Blockers And Risks before removing
their log entries. Do not archive removed detail or add detail-recovery checks. The summary's Time retains the latest Accepted or Not Applicable event's timestamp,
including when compaction resumes after an interruption; Updated uses the actual compaction time. Place the summary at that historical position and preserve other
phases' entries. Run-level events remain separate.

Compaction is a working-tree update included in the next task commit, or the terminal commit for the last phase. Do not amend the phase commit containing the detailed
log. If interrupted after commit but before compaction, complete and verify the summary before releasing dependencies. When a phase reopens, retain its prior summary and
append new events; its next closure commit preserves both before replacing them with one updated summary.

## Complete The Run

Final assurance follows [verification](verification.md). Before goal completion require:

- every phase closed, with its checkpoint, one compacted summary, and source-coverage evidence;
- final assurance passed for the current deliverable;
- all implementation assignments complete, required subagents terminal, ownership released, and no pending evidence or blocker;
- limitations and residual risks ready for the user handoff.

Record `Complete goal and finalize ledger` in `Next Actions`, then check the complete ledger under Field Rules and reconcile it against the prerequisites above. Resolve
stale states, uncompacted phase logs, or structural errors before completing the goal; do not invent past transitions or evidence to make the ledger pass.
Keep that action pending while calling the goal completion tool under its contract. If completion fails, preserve the unfinished state and report the blocker; never
manufacture success. Goal `blocked` updates must obey the runtime's recurrence rules.

After goal completion succeeds, record its authoritative status and usage, final candidate, evidence, and risks. Set ledger status to `Ready For Final`, clear active
ownership, and set `Next Actions` to `None` to prepare the terminal snapshot. This state authorizes handoff only after the terminal checkpoint is verified or a valid
skipped disposition is confirmed; it does not prove persistence.

Check changed portions, then commit the remaining current-run ledger changes under the same commit protocol; skip only under its stated conditions. A completed
goal does not prove this step succeeded. On a failed or uncertain commit, record the pending persistence step in `Next Actions` and report the blocker. On resume, inspect
the checkpoint before retrying; do not repeat goal completion. Clear that pending action when preparing a retry snapshot.

After verifying the checkpoint or confirming a valid skipped disposition, deliver outcome, files, validation, risks, and ledger locator. Include the goal's
authoritative total token usage and human-friendly elapsed time when available, regardless of whether a token budget was configured; never estimate missing metrics.

If interrupted between goal completion and ledger finalization, reconcile the completed goal with terminal evidence and finish that ledger update. Check candidate
changes and ownership before reemitting a pending handoff; reuse valid evidence rather than rerunning accepted work. If the candidate changed, report the changes and
follow the tool's permitted goal lifecycle before further execution.
