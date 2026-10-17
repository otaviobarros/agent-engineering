---
name: publish-change
description: Publish a verified, reviewed change through authorized commits, push, and a draft pull request. Use for the publication phase or to resume interrupted publication. Preserve operation-specific permissions and explicit limits.
---

# Publish change

Publish the current change within the user's authority.
Read the [shared workflow contract](../../references/workflow-contract.md) before starting.
The plugin includes this reference. Keep its directory layout intact.

## 1. Establish the publication scope

Identify the actual repository and workspace, branch, base, intended destination,
and authorized operations. Recover the current candidate, check and review evidence,
explicit limits, and any previous publication attempts. Read project conventions
for commits, branches, and pull requests. Reuse existing records and tools.

Distinguish commit, push, and pull-request authority. A skill invocation, check pass,
or review approval does not grant those permissions. Preserve earlier limits
across resumption. Continue authorized preparation when a later operation is excluded.
Resolve missing material intent before its dependent operation.

Done when the candidate, destination, operation permissions, and prior effects are clear.
For an interrupted or uncertain attempt, apply step 4 before another external write.

## 2. Check the candidate and evidence

Inspect the actual patch, index, and relevant untracked contents. Identify exactly
which changes belong to this delivery. Preserve unrelated staged, unstaged, and
untracked work. Compare the proposed commit contents with the contents checked
and independently reviewed, including relevant requirements and configuration.
HEAD and Git status alone do not establish freshness.

Apply required verification, independent review, finding dispositions, and readiness
conditions from the shared contract and project authorities. Keep failed, pending,
unavailable, inconclusive, and stale evidence explicit. Return affected gaps to the
appropriate phase; publication authority alone does not authorize corrective edits.

Done when applicable gates support the exact candidate for the next operation.
Missing required evidence blocks that dependent operation. Keep prior results tied
to their actual candidate rather than relabeling them as current.

## 3. Commit and publish within authority

Prepare only the authorized changes. Inspect the proposed staged contents before
committing. Keep commits coherent with their tests and documentation, and use the
project's commit convention. Preserve unrelated index entries. If that preservation
conflicts with producing the reviewed candidate, stop for a decision.

After commit hooks complete, inspect the committed file contents and remaining workspace.
Compare the committed contents or returned content identities with the checked
and independently reviewed candidate. Commit messages and diff statistics do not
complete this comparison. Unexpected changes or hook failures leave dependent
publication blocked. Record existing effects
before returning the gap; do not silently amend, reset, or discard work.

Before pushing, confirm the remote repository, target branch, intended commit, and
current destination state. Inspect the full outgoing commit range and resulting
tree; a reviewed final patch does not authorize unrelated unpublished ancestors.
Use an ordinary push that preserves remote history.
A destination conflict needs reassessment; it does not authorize a force push.
Read back the remote ref and require its object ID to match the inspected commit
before any PR write.

Before creating a pull request, inspect existing requests for the intended repository,
head, and base. Reuse a matching request within update authority; avoid duplicates.
Create new requests as drafts. Describe the delivered behavior, actual verification,
review evidence, and remaining limitations. Mark ready only with separate readiness
authority and current required checks and independent review.

Done when each authorized operation has an observed result, or a precise blocker.
Recheck mutable inputs before the next operation. Stop dependent writes when the
candidate, evidence, destination, or permissions no longer match.

## 4. Recover uncertain outcomes and report

After an interrupted or uncertain external write, inspect local records and actual
remote state before retrying. Verify the intended commit, branch, and pull-request
identity and state. A matching observed effect can satisfy that operation; it does
not authorize later operations. Retain any remaining scope limits.

If an effect is absent, establish that the earlier attempt cannot still execute
before retrying within current authority. Absence alone is insufficient. Renewed
publication permission does not establish that an earlier attempt has stopped.
If the outcome remains uncertain, stop further effect-producing attempts and
report what must be resolved. A fresh agent or session does not reset this uncertainty.

Report the candidate and evidence comparison, actual commit IDs, destination refs,
pull-request URL and draft state, completed operations, blockers, and next action.
Separate local completion, remote publication, and readiness. Report partial effects
honestly. Merge, release, deployment, formal approval, and monitoring remain outside
this skill's publication scope unless separately authorized through their own workflow.

Done when observed state supports the report and no authorized publication step
remains unaccounted for. These are guided procedures, not crash-safe enforcement.
