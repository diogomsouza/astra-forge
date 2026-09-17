# Integration And Verification

## Bind Evidence To The Candidate

Root reconciles the cumulative diff, attributes changes, preserves unrelated work, and checks acceptance evidence. Route substantive review under [mandatory model
routing](delegation.md#mandatory-model-routing). Suspend writes to the complete candidate in the workspace before review.
Include the design document when present; it is part of the reviewed deliverable, not live coordination state. Bind the review to the specification's recorded content
identity and explicit user amendments. Reconcile unexplained source changes before using them as acceptance authority.

Independent phases may write only outside the frozen candidate and any dependencies or shared state that can affect its evidence. Root must also leave the included
design document unchanged. If the candidate covers the whole product, pause all product writers for the review. Do not narrow required coverage to keep writers running.

Record the workspace, review scope, and baseline in Current State, using existing project revision or artifact references when available. This skill does not require
an additional candidate digest. Inspect the diff and relevant files, including untracked files and required ignored outputs, before review and acceptance. On resume,
check for changes before reusing evidence. Project-required integrity checks remain applicable.

## Review A Phase

Use the [lifecycle](lifecycle.md) to enter `In Review`. Confirm execution evidence and applicable cumulative validation. Reuse successful checks when candidate scope,
environment, and provenance remain valid. Repeat only for a change, failure, or unresolved concern; final assurance does not itself require rerunning an unchanged suite.
Check implementation conformance and the design's compatibility with original requirements and explicit user amendments. Following the design alone cannot establish
acceptance; apply the source authority rules in [planning](planning.md#specification-and-design).

Acceptance covers all verification obligations recorded for the phase, across its assignments. Root authorship does not change the verification mode or substitute
root's implementation checks for required independent review. For independent modes:

1. End implementation ownership and bind the workspace, candidate scope, baseline, evidence, relevant source requirements, and bounded review contract.
2. Select fresh verifiers through [delegation](delegation.md), with no inherited conversation, root deliberations, prior reports, or verdicts.
3. Keep the candidate unchanged until every required contract returns. Replace or serialize an unavailable verifier; block if required coverage cannot be completed.
4. After all required contracts return, inspect the diff, relevant files, and bound requirement sources once before acceptance. Resolve unexpected changes and
   revalidate affected evidence under [Correct And Revalidate](#correct-and-revalidate). An uncontrolled writer or unexplained drift prevents reliance on the review batch
   until its provenance is reestablished. Otherwise aggregate findings and classify them before authorizing one coherent correction wave.

Verifiers inspect behavior, consumers, failure paths, and evidence within their contracts. They may investigate suspected drift and report it; root owns the final binding
decision. Do not require redundant validation merely for independence.

Reject only for evidenced failure of an applicable requirement or affected guarantee. A preferred design is not a defect. Missing new tests alone is not rejection
evidence; an indispensable missing check must identify the obligation it cannot establish and why existing checks or another concrete method are insufficient.

Missing evidence that prevents a verdict without establishing a material violation yields `BLOCKED`, not `REJECT`. A required `BLOCKED` review leaves acceptance pending
until the missing condition is resolved and the review completes.

## Correct And Revalidate

Classify findings as planning, execution, integration, or newly discovered risk; a finding may expose more than one. Before authorizing the correction wave, root checks
the violated guarantee across affected callers, equivalent states, and adjacent transitions, then defines a coherent correction boundary and updates deficient contracts.
Apply the [scope rules](planning.md#scope-and-changes); new specialist review still requires the consequence-based selection gate.

Before corrections, reopen affected accepted phases and return the correcting phase to `In Progress`. Review-only evidence work stays `In Review`. Root specifies the
correction boundary and selects its executor under [delegation](delegation.md#select-the-executor), preserving the ownership-transfer rules when the writer changes.

Rerun rejecting contracts and contracts whose surfaces or guarantees may be affected. Carry forward unaffected evidence only with an explicit delta-based justification;
never present an old verdict as a review of subsequent changes.

Continue or reuse a verifier only within the same review assignment, including evidence completion and correction closure. A materially changed boundary, different
phase, or fresh final review requires a new identity.

Continue while the next correction has scope, authority, and checkable evidence. If a correction breaks the same guarantee, findings recur across its callers or states,
or validation repeatedly fails before exercising the target behavior, pause dependent correction work. Root must identify the missing rule or invalid assumption and
revise the model, contract, evidence strategy, or assignment before another attempt. Record the execution decision in the ledger; update the design document under
[planning](planning.md#specification-and-design). Repeated rejection alone justifies neither more compute nor abandonment.

## Final Assurance

After implementation phases close, review cumulative coverage and interactions. A final integration phase, when planned, performs this work within its own `In Review`
state; it need not already be accepted.

Require fresh independent general review for a high-risk cumulative candidate or a material cross-phase interaction not settled by phase evidence. Add a specialist only
for a changed boundary, new interaction, incomplete prior evidence, or authoritative requirement. Otherwise root confirms coverage from valid cumulative evidence; any
additional substantive review follows the model-routing policy.

Before launching final reviewers, bind their assignments to a phase in `In Review`; create a final-assurance phase or reopen a suitable phase for evidence-only
reevaluation when necessary.

Review the complete deliverable for final obligations without repeating unrelated accepted investigations. Final corrections reopen affected phases and require new phase
checkpoint commits. Complete the goal only through [lifecycle](lifecycle.md).
