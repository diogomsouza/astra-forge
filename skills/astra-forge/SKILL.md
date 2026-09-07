---
name: astra-forge
description: >-
  Lead and implement complex or long-running work with bounded delegation, resumable state, staged verification, and phase commits. Use when independent assurance, independent
  workstreams, or durable resume state materially helps. Avoid simple tasks unless explicitly invoked. Implicit use requires a runtime-confirmed gpt-6-astra root;
  other models require explicit invocation.
---

# Astra Forge

Root leads and implements the work, delegates bounded assignments when useful, and accepts each phase against evidence selected before implementation.

Reviewing or editing this skill does not activate its workflow. User instructions take precedence over this skill within system, developer, tool, and environment
constraints. Use one orchestration workflow and a ledger dedicated to the current run.

## Admission

Explicit invocation admits the run. Otherwise require a runtime-confirmed `gpt-6-astra` root or confirmed alias and at least one of:

- material risk that benefits from independent assurance;
- independent workstreams that save time or improve evidence;
- work whose duration or coordination needs justify durable resume state.

If admission fails, work directly without Astra Forge artifacts. Do not infer model identity from the task, model names in files, or agent self-report.

## Operating Rules

- A matching runtime goal is mandatory. Create it at startup when missing; a ledger cannot substitute for it.
- Root is the primary implementer and owns product decisions, architecture, scope, assignment contracts, integration, acceptance, goal lifecycle, and the ledger.
  All implementers choose technical details, diagnose failures, and correct their work within those boundaries. Delegated implementers return to root when a discovery
  requires changing the contract, shared architecture, or ownership.
  Independent reviewers judge evidence within their contracts; root decides the response to findings and cannot prescribe a favorable verdict.
- Keep execution state in the current run's ledger and technical additions in one [design document](references/planning.md#specification-and-design). Preserve the
  specification as a protected source. These are the only run documents; create the specification only when none is supplied. Do not create other coordination files
  in any directory, including contracts, review reports, evidence bundles, manifests, or archives. Tool outputs are permitted only when needed to run the tools or
  produce task deliverables under project conventions. Do not persist console captures or reports solely to retain coordination or review evidence.
- Resolve routine technical choices from evidence. Ask only for a missing decision that cannot reasonably be inferred and materially affects scope, correctness, or
  authority. Continue independent authorized work while optional questions are pending.
- Select the executor under [delegation](references/delegation.md#select-the-executor). Root implementation follows the same scope, ownership, validation, and phase
  gates as delegated implementation. Use disjoint ownership for concurrent writes; capacity is a ceiling.
- Never use `full-history` or `fork_turns="all"`. Independent verifiers receive no inherited conversation; other agents receive only bounded task context.
- Create new tests only when explicitly required by the user or authoritative project requirements, or exceptionally when indispensable to complete the task. For the
  exception, root must record the exact obligation and why existing checks or another concrete validation method cannot establish it. Convenience, coverage targets, and
  reviewer preference do not qualify. Pass this decision in the assignment contract.
- Close every phase under the [commit protocol](references/lifecycle.md#mandatory-phase-commit): commit its accepted deliverable changes and current ledger before
  dependent work; skip only when that checkpoint has no changes or no Git repository exists.
- Treat user updates as steering of the active objective unless they replace it. Reconcile affected requirements, contracts, ownership, and evidence before dependent
  work. Async operations remain pending until their results arrive.
- Keep reports concise: outcome, material evidence, unresolved limitations, and next action. Do not replay coordination history.

## Read On Demand

Read the applicable reference before its first use, and reread it after context loss or a relevant rule change. Do not preload every reference.

| Action | Required reference |
| --- | --- |
| Start, resume, discover, or revise phases | [Planning](references/planning.md) |
| Initialize or update durable state | [Progress template](references/progress-template.md) |
| Select executors or prepare implementation obligations | [Delegation](references/delegation.md) |
| Integrate, review, or correct a candidate | [Verification](references/verification.md) |
| Transition, commit, close a phase, or finish | [Lifecycle](references/lifecycle.md) |

When composing a delegated assignment, also read its single prompt pattern: [exploration](references/exploration-assignment-prompt.md),
[command execution](references/command-assignment-prompt.md), [implementation](references/implementation-assignment-prompt.md), or
[independent verification](references/independent-verification-assignment-prompt.md).
