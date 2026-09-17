# Progress Ledger

Use `.astra-forge/PLAN-PROGRESS-{context-id}.md` for resumable execution state. Root alone writes it. It records execution decisions and evidence; it cannot grant permission.

Keep each fact in one home: scope in Objective, workspace and ownership in Current State, phase acceptance in Execution
Plan, material events in Progress Log, immediate work in Next Actions, and unresolved conditions in Blockers And Risks. Reference design and implementation decisions in
the design document. Do not duplicate raw outputs or agent reports.

Update on material decisions, ownership changes, transitions, candidate changes, or blockers. Consolidate related changes already available into one edit and readback
before dependent actions. Do not wait for additional results to record a required update, combine transitions separated by required actions or evidence gates, or update
the ledger solely because a wait timed out. Use clock-derived ISO 8601 timestamps with time and UTC offset for Created, Updated, and Time. Preserve Created and historical
times; use the same current timestamp for Updated and the new events in each update.
Compacted summaries retain their historical disposition timestamp under [Close And Compact](lifecycle.md#close-and-compact); Updated still reflects the actual edit time.
Check updates under Field Rules before dependent actions. Lifecycle and compaction rules live in [lifecycle.md](lifecycle.md).

## Template

```markdown
# Astra Forge Progress: {context-id}

Goal: {runtime goal identity}
Created: [YYYY-MM-DDTHH:mm:ss±HH:mm]
Updated: [YYYY-MM-DDTHH:mm:ss±HH:mm]
Status: {Pending | In Progress | Blocked | Ready For Final}

## Objective

- Request: {concise task description and source reference}
- Specification: {locator; User Referenced | Captured User Plan | Generated; authorized revision or content digest}
- Design: {existing design document locator or None}
- Scope and exclusions: {specification reference; effective user amendments and their sources}
- Done when: {observable result and required evidence}
- Decisions: {current execution decisions; design references for technical decisions}

## Current State

- Workspace and candidate: {root, baseline, identity recipe, current fingerprint}
- Active ownership: {assignment -> root or subagent runtime identity, scope, state}
- Active contracts: {assignment -> phase reference, applicable verification obligations, essential constraints, pending evidence}
- External state: {environment conditions or execution limits affecting the next action or resume}

## Execution Plan

| Phase | Status | Outcome and Acceptance | Source Coverage | Depends On |
| --- | --- | --- | --- | --- |
| P0 | In Progress | Define scope, source coverage, dependencies, and acceptance evidence; Root Evidence: source coverage and decomposition checks | {request and sources} | Objective |

## Progress Log

| Time | Event | Evidence / Result |
| --- | --- | --- |
| [YYYY-MM-DDTHH:mm:ss±HH:mm] | Initialized | {goal binding and initial context} |

## Next Actions

1. {phase, immediate action, pending condition, governing reference; owner or dependency only if otherwise unclear}

## Blockers And Risks

- Blockers: {None or condition and required resolution}
- Risks: {None or residual risk and consequence}
```

## Field Rules

Current State contains only facts needed for the next action or safe resume. Reference existing plan and evidence entries instead of repeating them; use `None` when
a field is not applicable. Consult available roles, models, and capacity when selecting agents rather than maintaining a runtime catalog here.

For ordinary updates, preserve the template's headings, field labels, columns, and order. Edit only affected values or rows; put content in its designated field or section.
Keep one blank line between headings and content and between blocks, with none inside tables. Keep each table row on one line and escape literal pipes as `\|`.
Append log rows immediately after the table's last row, before its trailing blank line; the next section's heading is not the insertion point.
For an inapplicable field, retain its label and write `None`. Use `Unknown: {reason}` for unresolved required values, including an inaccessible specification's content
identity. For empty Next Actions, retain the heading and use only `None` as its content.
After a local update, read back changed fields and rows with adjacent lines to verify placement, separators, and agreement with the phase status and pending action.
Check the complete structure at creation, resume, after compaction, and before goal completion: section order, required fields, timestamps, table continuity and columns,
cell limits, phase summaries, and empty-section representation. Expand other local checks only when they reveal a problem.

Evidence / Result contains at most 500 characters per cell, including spaces and punctuation. Summarize the material result and reference longer evidence by an existing
source path, reproducible command, or result identifier. This limit does not require preserving full output or creating an evidence file.
Progress Log has no row limit before compaction; record only material events and identify their phase. After compaction, each closed phase has exactly one summary row
under [Close And Compact](lifecycle.md#close-and-compact).

Keep terminal identities, superseded candidates, and verdicts in Progress Log rather than live fields. Maintain assignment identities and ownership for coordination
and resume; a timeout alone does not establish termination. Record required exceptional-selection justifications in Progress Log, linked to the assignment, before launch.

Every applicable source requirement has one primary phase. Source Coverage points to the original requirements or explicit user amendments, never only to the design.
Technical decisions remain revisable under those sources and do not acquire user authority.
Outcome and Acceptance holds the phase's verification mode and complete obligations. Active contracts record only each assignment's applicable portion and pending evidence.
Record assigned responsibility only in Active ownership. Consult the runtime for the goal's current status.

Next Actions identifies the exact pending step for each actionable phase or run-level gate, including goal completion until it succeeds. Reconcile stale actions before
proceeding. In a prepared `Ready For Final` snapshot, `None` is subject to the terminal checkpoint in [Complete The Run](lifecycle.md#complete-the-run); it does not prove
persistence.

On resume, identify the exact pending gate and load its governing reference. Keep terminal candidate identity, checkpoint/evidence locators, residual risks, and goal
usage in the final event so clearing live fields does not erase recovery evidence.
