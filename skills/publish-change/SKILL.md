---
name: publish-change
description: Publish a verified, reviewed change through authorized commits, push, and a draft pull request. Use for the publication phase or to resume interrupted publication. Preserve operation-specific permissions and explicit limits.
---

# Publish change

Publish the current change within the user's authority. First read the
[contract core](../../references/workflow-contract.md) and the
[publication rules](../../references/publication.md).

## 1. Scope

- Identify the repository, workspace, branch, base, destination, authorized
  operations, candidate, evidence, limits, and earlier attempts. Read the
  project's commit, branch, and PR conventions; reuse existing records and tools.
- Commit, push, and PR creation are separate permissions; an invocation, passing
  check, or approval grants none. An excluded later operation leaves authorized
  preparation free to continue.
- Resolve missing material intent before its dependent operation.

**Checkpoint 1:** candidate, destination, permissions, and prior effects are clear.
Earlier attempt uncertain → apply the uncertain-outcome rule before any write.

## 2. Check the candidate

- Inspect the patch, index, and relevant untracked contents. Identify exactly what
  belongs to this delivery; preserve all other work.
- Compare the proposed commit contents with the checked and independently reviewed
  contents, including requirements and configuration, using the freshness check.
- Required verification, review, dispositions, and readiness conditions must hold.
  Keep failed, pending, unavailable, inconclusive, and stale evidence explicit and
  tied to its candidate. Missing evidence → block the dependent operation and
  return the gap to its phase; publication authority covers no corrective edits.

**Checkpoint 2:** gates support the exact candidate for the next operation.

## 3. Operation gates

**Commit**

1. Stage only authorized changes; inspect the staged contents. Commits stay
   coherent with their tests and docs and follow the convention.
2. Unrelated index entries stay. Keeping them conflicts with the reviewed
   candidate → stop for a decision.
3. After hooks, compare committed contents or content identities with the checked
   and reviewed candidate. Messages and diff statistics are not this comparison.
4. Unexpected change or hook failure → block publication, record effects, report
   the gap. Leave the work as is: no silent amend, reset, or discard.

**Push**

1. Confirm remote, target branch, intended commit, and destination state.
2. Inspect the full outgoing range and resulting tree; a reviewed final patch does
   not authorize unrelated unpublished ancestors.
3. Push normally, preserving remote history. A conflict needs reassessment and
   never authorizes a force push.
4. Read back the remote ref; its object ID must match the inspected commit before
   any PR write.

**Pull request**

1. Reuse a matching PR for the same repository, head, and base within update
   authority; create no duplicate.
2. Create new PRs as drafts, applying the project's description convention to
   prepared and published bodies.
3. Body: delivered behavior, actual verification, review evidence, limitations,
   and the [verification report](../verify-change/SKILL.md#4-check-freshness-report-and-stop)
   or a summary keeping each criterion's status and gaps. Derive remaining gaps
   from it, including criteria awaiting review.
4. Mark ready only under the publication rules' readiness condition.

**Checkpoint 3:** each authorized operation has an observed result or a precise
blocker. Recheck mutable inputs before the next operation; candidate, evidence,
destination, or permissions changed → stop dependent writes.

## 4. Recover and report

Interrupted or uncertain write → apply the uncertain-outcome rule, verifying
commit, branch, and PR identity and state through reads. Remaining limits stay.
Return:

```text
Candidate vs checked/reviewed contents: result
Commits: IDs
Remote: ref and object ID
Pull request: URL, draft state
Operations: completed | excluded | blocked (reason)
Partial effects, unresolved uncertainty, next action:
```

Keep local completion, remote publication, and readiness separate. Merge, release,
deployment, formal approval, and monitoring need their own authorized workflow.

**Done when** observed state supports the report and every authorized step is
accounted for. These are guided procedures, not crash-safe enforcement.
