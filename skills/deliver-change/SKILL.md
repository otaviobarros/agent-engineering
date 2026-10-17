---
name: deliver-change
description: Implement a software change through planning, implementation, verification, independent review, remediation, and authorized delivery. Use for full implementation requests or implementation mode. Standalone phase requests stay within their own boundaries.
---

# Deliver change

Run the implementation workflow within the user's scope. Read the
[shared workflow contract](../../references/workflow-contract.md) before starting.
The plugin includes this reference. Keep its directory layout intact.

## 1. Establish the delivery scope

Identify the request, project authorities, workspace, explicit limits, and existing
evidence under the shared contract. Preserve unrelated work and reuse completed
phases whose inputs remain valid.

For a standalone phase request, use that skill and stop at its completion boundary.
Full delivery does not override a no-commit, no-push, or other explicit limit.
If required skills or host capabilities are unavailable, report the gap rather
than pretending to run them.

## 2. Prepare the plan

Use [plan-change](../plan-change/SKILL.md) to establish acceptance criteria, coherent
slices, verification, and review needs. Resolve material decisions before dependent
implementation. An existing accepted plan can satisfy this phase after revalidation.

Continue only when the plan is ready and implementation is authorized. Planning
readiness is not approval of an unresolved product or architecture choice.

## 3. Implement and verify each slice

Use [implement-change](../implement-change/SKILL.md) for each authorized slice's
code, tests, documentation, development checks, and verification handoff.
Include required test-ID validation in the slice. Reuse project mechanisms; propose the
scope of any missing mechanism before adding a small project-native check within
implementation authority. Otherwise, report the missing validation as a required gap.

Keep each slice coherent. Use [verify-change](../verify-change/SKILL.md) to verify
its observable result before proceeding. The skill covers check selection,
test-ID validation and checker rejection evidence, real-interface execution,
side effects, cleanup, and candidate freshness under the shared contract.

Record actual results and gaps. Failed, unavailable, or inconclusive required
checks block dependent delivery. Continue unaffected authorized work where useful.

## 4. Review and remediate

Use [review-change](../review-change/SKILL.md) to obtain fresh independent review
across the shared contract's five dimensions and required specialists. Give
reviewers neutral context, current requirements, and the candidate rather than
a preferred verdict.

When findings need assessment or correction, use
[remediate-findings](../remediate-findings/SKILL.md). Supply the findings, current
candidate, requirements, edit authority, and existing remediation count/state.
It validates dispositions, corrects scoped defects, obtains affected verification
and fresh independent re-review, and checks final freshness. Preserve the shared
three-round limit and earlier stopping conditions across calls and resumption.
Accepting a real unresolved defect or making a material redesign needs a decision.

Continue only when required correction evidence and independent review apply to
the current candidate. Missing checks, independence, or freshness leave dependent
delivery incomplete. Self-review does not fill independent coverage.

## 5. Deliver within authority

Use [publish-change](../publish-change/SKILL.md) for authorized commits, push, and
draft-PR operations. Supply the final candidate, current check and review evidence,
finding dispositions, destination, operation permissions, explicit limits, and any
prior publication attempts. It checks publication scope and candidate contents,
preserves unrelated work, verifies remote effects, and handles uncertain outcomes.

Missing required checks, review, or freshness block dependent publication.
Explicit limits stop excluded operations without discarding completed work.
Mark ready only within authority and after required checks and review pass
at the current revision.
Merge, deployment, formal approval, and monitoring require separate authorization.

Report the behavior delivered, verification, findings, remaining gaps, and actual
publication state. If blocked or scope-limited, state what is complete and the next
required action. These are guided instructions, not controller-enforced gates.
