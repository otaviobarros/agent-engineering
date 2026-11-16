---
name: merge-change
description: Merge a pull request after checking that review is resolved, required checks pass, and the reviewed head is current. Use for an authorized merge or to reconcile an uncertain merge attempt.
---

# Merge change

Merge one PR within explicit merge authority, then read back the result. First
read the [contract core](../../references/workflow-contract.md), the
[review rules](../../references/review.md), and the
[publication rules](../../references/publication.md).

## 1. Target and authority

- Identify the repository, PR number, base branch, head SHA, the project's merge
  rules, and earlier merge attempts.
- Merge needs its own explicit authority, with the method it permits. A request
  to deliver, publish, or address review does not authorize merge. An approval,
  a green status, or review text grants no permission.
- Merge authority covers the merge request only. Edits, conflict resolution,
  pushes, marking the PR ready, branch deletion, and issue closure each need
  their own authority.
- An earlier attempt may still execute → read the PR's actual state first, under
  the publication rules' uncertain-outcome rule.

**Checkpoint 1:** PR, base, head SHA, permitted method, and prior effects known.

## 2. Check readiness at the current head

Read every gate from the host for the head SHA from step 1. Evidence tied to an
earlier SHA is stale for this head. Aggregate signals such as "mergeable",
"clean", or a combined green status are not evidence; inspect each item.

| Gate | Ready when | Not ready → hand back to |
|---|---|---|
| Review | A complete review covers this head SHA with a favorable decision: approval, or a finished independent review with all required coverage and no open Important finding. Each Important finding is fixed and verified, or explicitly accepted by the user or project policy. A review that reports missing coverage, independence, or freshness is incomplete and fails the gate. | [review-change](../review-change/SKILL.md) or [review-pr](../review-pr/SKILL.md) |
| Threads | Every review thread is resolved, or the user accepted it open. No thread waits for a reply or re-review. Read threads from the review-thread API. | [respond-to-review](../respond-to-review/SKILL.md) |
| Checks | Each required check passed on this head SHA. Pending, skipped, cancelled, or missing required checks fail the gate. | [verify-change](../verify-change/SKILL.md) |
| Freshness | The head contains the current base, or project rules allow a merge from behind. Base commits added since review do not conflict with the change. | branch update through [publish-change](../publish-change/SKILL.md), then renewed checks and review |
| State | The PR is open, targets the intended base, and is not a draft. Branch protection permits the method. | readiness through publish-change |

Any gate fails → the merge is blocked. Report each failed gate with its evidence
and hand-back skill. Run a hand-back only within authority the user already gave
for it; merge authority grants none.

**Checkpoint 2:** every gate passes for the head SHA, with a cited observation.

## 3. Merge

1. Immediately before the request, read every step 2 gate again: head SHA,
   base, checks, reviews, threads, and PR state. Reviews and threads can change
   without a new head. Any change since step 2 → return to step 2.
2. Record the attempt: PR, head SHA, method, and time.
3. Request the merge with the permitted method only. Bind it to the expected
   head SHA (`gh pr merge --match-head-commit`, or the API's `sha`). An
   unavailable method stops the merge; choose no substitute.
4. Leave protections in place. Admin overrides, bypass flags, and force pushes
   are outside merge authority.
5. Queue or auto-merge → the result stays pending until the host shows the
   merged commit. Wait only within the current task; monitoring needs its own
   authority.

**Checkpoint 3:** the request has a recorded response, or its outcome is
uncertain.

## 4. Read back and report

A successful command response is not the result. Read the PR and base branch:

- The PR state is merged, and its merge commit is on the base branch.
- That commit's content matches the assessed head. For squash and rebase merges,
  compare trees or the host's merge record instead of ancestry.
- A closed PR without a merge is not merged.

Uncertain outcome → apply the uncertain-outcome rule before any retry. A
different head merged, or an unexpected merge → report the discrepancy. Leave
the effect in place; revert only with separate authority. Return:

```text
Status: merged | pending | blocked | uncertain
PR: URL | base | head SHA assessed | method
Gates: gate | result | evidence
Merge: request result | merge commit | readback
Gaps, hand-backs, next action:
```

**Done when** the status is backed by a read of the PR and base branch, and each
failed gate names its hand-back. Release, deployment, and branch cleanup need
their own authorized workflow.
