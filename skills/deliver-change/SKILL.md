---
name: deliver-change
description: Implement a software change end to end, from plan to authorized draft pull request. Use for full implementation requests or implementation mode. Standalone phase requests use their own skill.
---

# Deliver change

Run the full workflow within the user's scope. First read the
[contract core](../../references/workflow-contract.md); each phase skill reads its
own phase references.

## 1. Scope

- Identify the request, project authorities, workspace, explicit limits, and
  existing evidence. Reuse completed phases whose inputs remain valid.
- Standalone phase request → use that phase skill and stop at its boundary.
- Explicit limits such as no-commit or no-push stay binding in full delivery.
- Required skill or host capability unavailable → report the gap; never simulate it.

## 2. Phase gates

Run the phases in order. Continue only when the gate holds for the current
candidate:

| # | Phase skill | Gate to continue |
|---|---|---|
| 1 | [plan-change](../plan-change/SKILL.md) | Plan ready, material decisions resolved, implementation authorized |
| 2 | [implement-change](../implement-change/SKILL.md) | Slice implemented, checks recorded |
| 3 | [verify-change](../verify-change/SKILL.md) | Required checks pass |
| 4 | [review-change](../review-change/SKILL.md) | Fresh independent review is complete |
| 5 | [remediate-findings](../remediate-findings/SKILL.md), when findings need it | Corrections verified and re-reviewed |
| 6 | [publish-change](../publish-change/SKILL.md) | Authorized operations done and read back |

A required check, review, or freshness result is missing, failed, unavailable, or
inconclusive → stop the dependent phases, continue unaffected authorized work,
and report the gap.

## 3. Phase inputs

- **Plan.** A revalidated accepted plan satisfies phase 1. Readiness does not
  approve an unresolved product or architecture choice.
- **Implement and verify.** Run phases 2–3 per coherent slice, including required
  test-ID validation. Missing validation mechanism → propose its scope, then add a
  small project-native check within implementation authority, or report a
  required gap.
- **Review.** Supply neutral context, current requirements, and the candidate,
  without a preferred verdict. Self-review never fills independent coverage.
- **Remediate.** Supply findings, candidate, requirements, edit authority, and the
  current round count and state. The three-round limit and earlier stopping
  conditions hold across calls and resumption. Accepting a real unresolved defect
  or a material redesign needs a decision.
- **Publish.** Supply the final candidate, current check and review evidence,
  dispositions, destination, operation permissions, explicit limits, prior
  attempts, and the
  [criterion results](../verify-change/SKILL.md#4-check-freshness-report-and-stop)
  updated with review evidence. Excluded operations stop; completed work stays.
  Mark ready only within authority, after required checks and review pass at the
  current revision.

## 4. Report

Report the behavior delivered, verification, findings, remaining gaps, and actual
publication state. Carry forward each criterion's status and gaps, and list
criteria whose required check did not run as `Not verified`. When blocked or
scope-limited, state what is complete and the next required action. Merge,
deployment, formal approval, and monitoring need separate authorization. These are
guided instructions, not controller-enforced gates.
