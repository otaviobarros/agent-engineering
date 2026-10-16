---
name: deliver-change
description: Implement a software change through planning, implementation, verification, independent review, remediation, and authorized delivery. Use for full implementation requests or implementation mode. Standalone planning and review requests stay within their own phases.
---

# Deliver change

Run the implementation workflow within the user's scope. Read the
[shared workflow contract](../../references/workflow-contract.md) before starting.
The plugin includes this reference. Keep its directory layout intact.

## 1. Establish the delivery scope

Identify the request, project authorities, workspace, explicit limits, and existing
evidence under the shared contract. Preserve unrelated work and reuse completed
phases whose inputs remain valid.

If the request is planning-only or review-only, stop at that phase. Full delivery
does not override a no-commit, no-push, or other explicit limit. If required skills
or host capabilities are unavailable, report the gap rather than pretending to run them.

## 2. Prepare the plan

Use [plan-change](../plan-change/SKILL.md) to establish acceptance criteria, coherent
slices, verification, and review needs. Resolve material decisions before dependent
implementation. An existing accepted plan can satisfy this phase after revalidation.

Continue only when the plan is ready and implementation is authorized. Planning
readiness is not approval of an unresolved product or architecture choice.

## 3. Implement and verify each slice

Make the authorized changes with their tests and required documentation. Keep
each slice coherent and verify its observable result before proceeding. Use the
shared contract for defect-detection evidence, test identities, real-interface
checks, side effects, cleanup, and evidence freshness.

Run the shared contract's test-ID validation, not just the behavioral tests. Derive
the case list from tests and check required cases for missing or duplicate IDs.
Reuse the project's check. If none exists, include a small project-native check
in the authorized slice or report the missing validation as a required-check gap.
A handwritten mapping or unique-looking names do not establish a pass. Verify
that the check rejects missing IDs, duplicate IDs, and duplicate definitions
that collection can hide (such as identical test method names), using disposable
copies. Supplement collection with source checks where needed.

Record actual results and gaps. Failed, unavailable, or inconclusive required
checks block dependent delivery. Continue unaffected authorized work where useful.

## 4. Review and remediate

Request fresh independent review across the five dimensions in the shared
contract. Add its required specialists. Give reviewers neutral context, current
requirements, and the candidate rather than a preferred verdict.

Validate findings. Fix scoped defects, independently verify corrections, and
repeat affected checks/review at the current candidate. Follow the shared
three-round limit and earlier stopping conditions. Obtain a decision before
accepting a real unresolved defect or making a material redesign.

If independent review is unavailable, report delivery as incomplete. Self-review
does not fill that gap.

## 5. Deliver within authority

Recheck the final candidate, required evidence, permissions, and destination.
Perform only the authorized commit, push, and draft-PR operations under the shared
contract. Explicit limits stop those operations without discarding completed work.
Mark ready only after required checks and review pass at the current revision.
Merge, deployment, formal approval, and monitoring require separate authorization.

Report the behavior delivered, verification, findings, remaining gaps, and actual
publication state. If blocked or scope-limited, state what is complete and the next
required action. These are guided instructions, not controller-enforced gates.
