# Delegation

## Select The Executor

Root implements by default. For each available implementation assignment, first determine whether a specialist's method materially improves a concrete correctness
problem within its declared domain. Delegate that bounded core when needed, even when it is the only implementation available.

For general implementation, root takes the work when only one assignment is available. When independent assignments can proceed concurrently, root takes one and
delegates the others where parallel execution provides a concrete benefit. Choose root's part for its use of existing context and ability to unlock dependent work.
Do not divide coupled work merely to keep agents occupied. Resolve shared interfaces and dependencies before concurrent writes.

Before starting its own implementation assignment, root announces a short description of the work it is taking, without explanation or a task list.
Repeat only when its assigned scope materially changes, not for routine continuation.

Root retains orchestration responsibility while implementing. Address blockers and decisions that prevent other authorized work before continuing local implementation;
handle coordination at natural execution boundaries without adding periodic status checks. Root may temporarily prioritize orchestration when its own implementation
would delay the overall task. Do not duplicate work already assigned to a subagent.

Keep in-scope diagnosis and corrections with the current implementer. Reconsider the executor when the boundary or capability needs change, or an ownership transfer
would materially improve progress; use the transfer rules below before another writer takes over.

## Select Delegated Roles

Define the required role contract by purpose, scope, authority, and domain fit before selecting a model.
For implementation, use a general implementer by default and a specialist for cores selected under the executor policy above.

## Model Catalog

| Nickname | Runtime model ID |
| --- | --- |
| Lua | `gpt-5.6-luna` |
| Terra | `gpt-5.6-terra` |
| Sol | `gpt-5.6-sol` |
| Astra | `gpt-6-astra` |

Resolve nicknames to these IDs in launch configurations and assignment prompts. Use an alternative ID only after runtime confirmation that it resolves to the same model.

## Mandatory Model Routing

The model, effort, launch-context, and announcement rules below apply to delegated agents. Root retains its runtime configuration when implementing. Root's run-document 
maintenance follows [planning](planning.md#specification-and-design).

### Delegation Boundaries

Commands and validation needed to complete an assignment stay with its executor, within its scope, permissions, and ownership.

Root delegates standalone exploration to Lua when delegation provides a concrete coordination or parallelism benefit.
For standalone command execution, delegation requires the same benefit and a long-running validation campaign or script expected to take minutes or hours. Root runs other 
standalone commands directly, including quick commands.

### Model Selection

Classify delegated assignments by their required result:

| Required result | Model |
| --- | --- |
| Code/file exploration, lookup, extraction, and mechanical inspection | Lua |
| Eligible standalone command execution | Lua |
| Conventional implementation | Terra |
| Implementation requiring moderate reasoning | Sol |
| Implementation requiring elevated reasoning | Astra |
| General, specialist, correction, and final reviews | Astra |

Creating or modifying project scripts is implementation. Inline, nonpersistent inspection and validation commands that leave project implementation unchanged follow 
command-execution routing. Classify by effects, not language.

Implementers own diagnosis and technical choices within their contracts; root resolves changes to product behavior, architecture, or scope.

All reviews use Astra; their reasoning obligations determine effort, not model. For implementation, use Terra when established project patterns and bounded dependencies
suffice. Use Sol when moderate reasoning is needed to adapt those patterns or resolve bounded implementation choices across well-understood components. Use Astra when
correctness requires substantial reasoning about interacting invariants, concurrency, recovery, nontrivial algorithms, or uncertain failure behavior. Prefer Astra at the
Sol–Astra boundary.

Select the model by assignment type before choosing effort. Where model or effort can vary, base the choice on concrete reasoning needs; file count, duration, role,
technology labels, business importance, or a previous failure alone do not justify it.

### Effort Selection

Lua always uses `high`. For all other models, choose the lowest effort adequate for the remaining reasoning obligations, with a minimum of `medium` for Terra and Sol. 
Assess effort within the selected model's category; higher effort must not substitute for a required model change.

- `low`: localized reasoning with a defined approach, clear evidence, and few unresolved interactions.
- `medium`: resolve interacting rules, failure paths, or bounded technical choices within a known design.
- `high`: reconcile coupled mechanisms whose local decisions affect other guarantees, requiring joint analysis of ordering, partial effects, or competing constraints.
- `xhigh`: an exceptionally difficult bounded core requiring sustained reasoning over inseparable constraints; splitting the analysis would lose the guarantee being established.

Except for Lua, before launching at `high` or `xhigh`, briefly record in the ledger which obligation makes the next lower level insufficient and the expected evidence benefit. 
Prior lower-effort attempts are not required.

Select review effort from the review's own obligations, independently of implementation effort. Do not use `max` or `ultra` for delegated assignments.

### Launch Configuration

Select a runtime role compatible with the required contract, model, and effort. If a fixed role is incompatible, use another eligible configurable role. If no compatible route 
exists, report the blocker; do not silently switch models, inherit root's configuration, or bypass tool constraints.

Finalize role, model, effort, and context before launch. Use `none` or bounded context for exploration, command execution, and implementation; independent verification 
requires `none`. Full conversation history is forbidden. Use the host's supported bounded-context mechanism, or supply a self-contained prompt with `none`.

Check launch arguments against the selected configuration and tool contract. Use only supported parameters and permitted overrides compatible with fixed role settings. 
If the runtime reports a configuration mismatch, stop affected work, reconcile affected writes, and replace the invalid assignment context.

### Agent Announcements

Provide the exact runtime role identifier and configured launch-context parameter and value in initial and continuation prompts. Require the first commentary message of 
each execution, including continuations, to announce both before working, once per execution. Report the runtime role identifier, not a task label, and the context parameter 
and exact value (`fork_turns` or the host equivalent), not the assignment's scope.

Keep the original launch-context setting in continuation prompts; continuation does not reset the agent's own history.

Verify model and effort through authoritative runtime metadata; do not request them in agent announcements.
Announcements do not establish runtime identity.

If either announcement field is missing or incomplete, root requests it at the next interaction. This omission alone neither requires restarting the assignment nor invalidates 
otherwise valid evidence.

## Select Verification Before Writes

Choose one verification mode for each phase before its first implementation write, or before acceptance for read-only discovery. Record the mode and complete phase
obligations in the ledger's Outcome and Acceptance. Each assignment contract receives the applicable portion; no assignment's handoff substitutes for the combined
phase obligations. Choose among:

- `Root Evidence`: all effects are bounded, local, reversible, and decidable with reproducible root evidence; no material trust, durable-state, concurrency, lifecycle,
  schema, or public-contract boundary changes.
- `Independent General`: the default when those conditions do not hold.
- `Independent Portfolio`: general review plus specialist review of a changed boundary with a reachable material failure that root evidence and general review cannot
  adequately decide.

Substantive review is an acceptance judgment about behavior, invariants, or failure paths not already established by explicit, reproducible checks. Confirming
ownership, candidate binding, or evidence completeness alone is not substantive review. If acceptance requires substantive review, select an independent mode.

Activate specialists by concrete consequence, not technology labels. Read their available role contracts and translate applicable review dimensions into implementation
invariants, failure paths, and evidence obligations. Do not infer hidden instructions; missing internals block only when eligibility or coverage cannot otherwise be
established.

Escalate the recorded phase obligations and affected contracts after new risk, missing evidence, or consumer impact appears. Do not de-escalate after material writes.
Serialize required review when capacity is limited.

## Build The Contract

Define each implementation assignment before writes. For root-owned work, record its ownership and essential contract in the existing ledger, referencing the phase
obligations and design. Do not create a separate agent identity, self-addressed message, or contract file. Root resolves discoveries that change its contract or design
and updates affected records and agents before dependent writes.

For delegated work, root sends a self-contained contract in the assignment message before launch. Include only what the assignment needs:

- outcome, owned paths or systems, baseline, dependencies, and source requirements;
- the assignment's part of the solution design, interfaces, invariants, and required failure behavior;
- exclusions, permitted tool outputs, validation evidence and its limits, unavailable facts, and handoff condition;
- decisions that require returning to root, verification mode, and any new-test authorization.

Include persistence constraints in every delegated assignment: do not create auxiliary coordination files; return findings, decisions, and evidence in the response.
Root maintains the design document, protects the specification, and records essential execution results and pending obligations in the ledger.

For each material guarantee, root specifies whether supplied evidence, simulation, a real mechanism, or a public workflow can establish it. Simulation cannot establish
behavior it replaces. When fixtures reproduce permissions, process context, locking, or persistent state, require a representative check of that setup before expanding
the validation matrix. Use existing checks where sufficient; new tests remain subject to the test policy in [SKILL.md](../SKILL.md).

Carry the [solution design](planning.md#discover-and-decompose) into the contract. Implementers choose local algorithms, function organization, and debugging methods that
preserve it. Component boundaries, shared behavior placement, and dependency direction are architectural decisions even within one writer's owned files. An implementer
may propose an alternative; root resolves it before dependent writes. Do not dictate a reviewer's findings or conclusion.

Before dispatch, confirm the implementer can start without choosing missing product or architectural decisions; check for conflicting instructions, inaccessible
dependencies, and undefined success conditions. Resolve missing prerequisite evidence through bounded exploration or an authorized experiment under
[planning](planning.md#discover-and-decompose). Root interprets the result and updates the contract before dependent implementation. Implementation details may be
discovered during execution.

Give agents relevant original requirements, explicit user amendments, and applicable design sections, identifying the source of each. State that requirements govern
the design and assignment. Fresh reviewers receive no prior verdicts or predicted findings. If one executor cannot produce a coherent increment, use bounded sequential
assignments; create separate phases only for independently acceptable outcomes.

## Execute And Track

For delegated assignments, use the applicable [exploration](exploration-assignment-prompt.md), [command execution](command-assignment-prompt.md),
[implementation](implementation-assignment-prompt.md), or [verification](independent-verification-assignment-prompt.md) prompt.

A subagent identity belongs to one assignment and phase. Reuse it only for continuation or correction of that assignment. A different assignment requires a fresh identity.
Descendants require root authorization of each child's scope, role, configuration, depth, and capacity; they cannot own the ledger or verify their implementation
ancestry.

Each implementer, including root, writes only within its recorded ownership. Preserve unrelated edits. For isolated work, require a base and integration delta; for
shared work, use disjoint ownership or serialize, including commands that affect shared outputs or resources. Integrate into the cumulative workspace, never replace
it with an agent snapshot. Before transferring ownership, obtain the prior writer's explicit release or confirm it has stopped and cannot write there. Reconcile its
changes and pending operations, then record the new owner and notify any continuing agent before writes resume.
Disjoint ownership does not override an active [candidate freeze](verification.md#bind-evidence-to-the-candidate).

Each delegated executor carries out only the work authorized by its contract and returns evidence. Report `SPEC_GAP` when a discovery requires a contract change, `NEEDS_SPLIT` for an
incoherent boundary, or `MISROUTED` for an unsuitable capability. Pause only dependent work; root decides and updates the contract. Implementers continue local diagnosis and
corrections that preserve their contract boundaries.

When awaiting a subagent's progress or completion, use the longest timeout permitted by the tool and higher-priority instructions.

If a wait times out and no useful independent work, actionable new information, or concrete reason to intervene is available, continue waiting without requesting status. 
Timeout expiration alone does not justify rereading files or logs, reporting unchanged progress, or declaring inactivity. Use intermediate agent messages only for concrete 
coordination needs, not routine progress checks; final responses provide assignment results.

Treat task-relevant tool activity and coherent analysis as progress signals, even without file changes. Prefer steering before replacement. Intervene when needed to correct course, 
resolve a blocker or runtime failure, address confirmed inactivity, enforce an execution budget, or protect ownership/safety boundaries.

Combine already available decisions and clarifications for each agent into one message. Send blockers and correctness-affecting changes promptly; do not delay them
to collect more updates. Avoid repeating unchanged instructions or sending acknowledgment-only messages unless acknowledgment is required for the agent to proceed.
Preserve the required role and launch-context fields in continuation prompts.

Delegated execution handoffs state `DONE` when assigned execution and validation obligations pass, `INCOMPLETE` for unfinished work, or `BLOCKED` when a specific prerequisite
prevents continuation. Independent verification uses only `ACCEPT`, `REJECT`, or `BLOCKED` under its prompt. Every handoff reports evidence, gaps, and any out-of-scope
writes. Before advancing the [lifecycle](lifecycle.md), root confirms the complete diff, validation, and ownership release for every implementation assignment,
including its own. Record root's execution evidence directly in the ledger. Execution completion alone is not acceptance.
