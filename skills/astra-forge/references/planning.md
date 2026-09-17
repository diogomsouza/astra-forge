# Planning And Resume

## Start

Before substantial discovery, delegation, ledger creation, or candidate writes, inspect goal-lifecycle capabilities, current goal state, and any matching run ledger.
If a matching ledger exists, reuse its context ID and follow [Resume](#resume); do not reinitialize it.

Reuse an unfinished goal only when its objective matches the request; ask the user to resolve a conflicting unfinished goal. When no matching goal exists, derive the
outcome, scope, non-scope, and completion evidence from the request and authoritative sources. Resolve only technical gaps needed to define the goal through bounded
read-only inspection; leave implementation discovery and phase decomposition to P0. Ask only for material product or scope decisions that cannot be inferred from those
sources, then create the goal. Set a token budget only when explicitly requested. If goal lifecycle is unavailable or fails, stop; preserve an existing matching ledger
and record the blocker only when safe.

For a new run, choose a unique `YYYY-MM-DD-{slug}` context ID. After creating or reusing the matching goal:

1. Use the user-referenced specification. If it cannot be found or read, try to locate it or recover access; do not generate a substitute. Keep only source-dependent
   work pending while that prerequisite remains unresolved. Only when no specification was supplied, capture the user's request, specified or clarified requirements,
   scope, exclusions, and acceptance criteria in `docs/PLAN-SPECS-{context-id}.md`, preserving any user-approved conversational plan. Do not turn agent assumptions into
   requirements.
2. Preserve that specification after creation, regardless of origin. Edit it only on an explicit user instruction to update that file. Record its locator, origin,
   and current authorized content identity (an immutable revision covering that content or a digest) in the ledger. Follow [Specification And Design](#specification-and-design)
   for technical additions.
3. Create `.astra-forge/PLAN-PROGRESS-{context-id}.md` using the [progress template](progress-template.md), initially with only discovery phase P0. On Windows,
   attempt `attrib +h ".astra-forge"` from the workspace root after folder creation; the leading dot alone does not hide it.

Record a concise request description and its source, specification origin and locator, scope references, and acceptance criteria. Preserve user requirements in the
source specification rather than copying them into the ledger. Every applicable requirement must map to acceptance evidence;
exclusions need a reason consistent with the user's scope.

## Specification And Design

When material technical additions are needed, root creates `docs/PLAN-DESIGN-{context-id}.md`. Maintain one design document for the run across phases and resumes; do not
create empty placeholders or documents per phase or decision. Record its locator in the ledger's Design field.

Record only material decisions needed to coordinate implementation: component responsibilities, shared interfaces, dependency direction, cross-component invariants,
and unresolved assumptions. For each decision, state its governing source, the chosen approach, and a brief rationale. Reference existing specifications, schemas,
symbols, and tests instead of restating their contents.

Keep local algorithms, implementation walkthroughs, execution instructions, agent contracts, verification results, and debugging history out of the design. Include
detailed state transitions only when they define a shared contract or a correctness guarantee that cannot be understood from existing references.

Organize decisions under stable component or concern headings. Update decisions in place and remove superseded detail; Git preserves history. Before closing an
affected phase, consolidate duplicated rules and replace implementation detail already established in code with references. Complete these design edits before
freezing the candidate for review under [verification](verification.md#bind-evidence-to-the-candidate).

Acceptance criteria and numerical limits remain authoritative in their original sources. Reference those sources directly; do not introduce an alternative definition
in the design.

The specification and subsequent explicit user instructions govern requirements. The design guides implementation within those boundaries and never acquires authority
to add functionality, remove obligations, relax acceptance criteria, or change exclusions. Resolve ordinary technical choices from evidence and correct design
conflicts against clear requirements. Ask the user only for a missing material decision that cannot be inferred or for a change to approved scope; pause only work
dependent on that resolution. Keep effective user amendments and their sources in the ledger's Scope and exclusions, and update the affected design and assignments.
Update the specification's recorded content identity only after a confirmed user change or an explicitly authorized edit. Scope approval alone is not an instruction
to edit the source file.

## Discover And Decompose

P0 is bounded read-only discovery of implementation, consumers, tests, project instructions, existing changes, and relevant external state. Where a comparable workflow
exists, compare its responsibilities, dependencies, and guarantees with the requested behavior before choosing what to reuse. Similarity alone does not justify
abstraction or refactoring.

Identify unverified assumptions that could change the design or invalidate acceptance evidence. Resolve them through available read-only checks, or make the smallest
authorized experiment a prerequisite to dependent implementation after P0. Stop discovery when remaining unknowns cannot change phase boundaries, dependencies,
obligations, or evidence, or are assigned explicit prerequisites requiring replanning from their results. Before P0 acceptance, writes are limited to run documents
under [Start](#start) and [Specification And Design](#specification-and-design).

Inspect runtime topology, available roles, supported model/effort pairs, fixed configurations, context-transfer options, capacity, and lifecycle capabilities. Recheck
when these change or after resume. Unknown writer topology forbids concurrent writes.

Root defines the solution design: affected component responsibilities, dependency direction, interfaces, and what to reuse, adapt, separate, or create. Locate shared
behavior according to those responsibilities and identify how existing consumers will integrate with it. Resolve structural decisions before fixing the corresponding
assignment boundaries. When an experiment is needed, P0 defines it and marks only the dependent design and decomposition as provisional. Root finalizes those decisions
from the result before releasing dependent implementation. Maintain technical additions under [Specification And Design](#specification-and-design). A requirements
list and file ownership alone do not define a design.

Group work by independently acceptable outcomes or a shared invariant whose parts must pass and be corrected together. Split when an outcome can start earlier, unlock
useful work, or be accepted and corrected independently. Do not split by file count, technical layer, or available agent slots alone.

Map each required behavior and cross-phase guarantee to one primary phase and a resolvable source section. Give each phase its earliest dependencies and observable
acceptance evidence in Outcome and Acceptance. Record each phase's verification mode and complete obligations there under
[Select Verification Before Writes](delegation.md#select-verification-before-writes). Create assignments only when dependencies permit work, choose root or a subagent
under [Select The Executor](delegation.md#select-the-executor), and record responsibility in Active ownership.
Reserve final integration phases for behavior that cannot be established earlier.

For work whose correctness depends on ordering, durable state, or recovery, root defines the governing states, permitted transitions, partial effects, and evidence
authorizing continuation or compensation. Include interruption during recovery and affected callers in the design. Unresolved platform behavior remains an explicit
prerequisite, not an assumed guarantee.

Confirm P0 source coverage and decomposition, then close it through the [lifecycle](lifecycle.md) before dependent work.

## Scope And Changes

A correction must address an approved requirement or a directly affected existing guarantee. Separate a valid defect from an unnecessarily broad remedy. Do not add
features, compatibility layers, or adjacent refactors merely because a reviewer suggests them. Apply the test exception in `SKILL.md` before authorizing new tests.

Discard unsupported or unrelated remedies from execution. Material unrelated findings may be reported separately without turning them into work or blocking this task.
User updates can amend scope; reconcile affected phases, contracts, and evidence.

Give agents access to relevant original requirements and specification sections. Include clean requirement excerpts in assignment messages when a source also contains
previous verdicts or implementation deliberations. Root remains responsible for complete source coverage; a bounded contract must not silently replace or omit an
applicable requirement.

## Resume

Read `SKILL.md`, this reference, and the complete matching ledger. Inspect the goal, workspace, agent identities and ownership, candidate identity, and relevant external
state. Then load only references governing the pending action.
Read the specification sections governing the pending work, effective user amendments, and the relevant design sections and their dependencies before reconstructing
assignments or making design decisions. Read the complete design only when the affected scope cannot be determined or a cross-cutting change requires it. Reuse the
recorded design locator; do not create another document on resume.

Reconcile durable records against authoritative sources. Treat summaries as memory, not permission. Stop for conflicting goals, ambiguous ledgers, or unreconstructable
critical state. Recreate a missing goal for the active objective.

Reproduce evidence whose candidate binding, provenance, or independence is uncertain. If the goal is already complete, use the terminal recovery procedure in
[lifecycle.md](lifecycle.md); do not restart accepted work.
