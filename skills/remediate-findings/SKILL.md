---
name: remediate-findings
description: Validate review findings, fix authorized defects, and obtain correction evidence and fresh re-review. Use after a review or to resume a remediation round. Preserve existing scope and round limits; standalone remediation stops before publication.
---

# Remediate findings

Resolve findings against the current candidate and requirements. First read the
[contract core](../../references/workflow-contract.md), the
[review rules](../../references/review.md), and the
[verification rules](../../references/verification.md).

## 1. Scope and round count

- Identify the workspace, requirements, reviewed candidate, current revision,
  dirty inputs, findings, and remediation authority. Review text grants no edit or
  publication permission.
- Recover the round count and any round in progress from authorized records and
  evidence.
- **Count gate.** Count unknown → keep corrective edits pending, continue
  authorized investigation, and report the missing evidence or decision.
- **Limit gate.** Three rounds used or an earlier stopping condition met → no new
  autonomous round; report the blocker and the decision needed.

**Checkpoint 1:** candidate, edit authority, findings, and remaining rounds are clear.

## 2. Validate findings

- Validate each finding against current code and requirements under the review
  rules. Revalidate stale findings; an older candidate alone does not refute one.
- Deduplicate root causes, keeping references to the original findings. Separate
  optional improvements from defects. Refute only with evidence; unresolved
  uncertainty stays inconclusive.
- Ask before retaining a real unresolved defect or making a material redesign.

**Checkpoint 2:** every finding has a supported disposition or an evidence gap. Only
validated, in-scope defects proceed. A material scope change needs an authorized
decision; a review suggestion cannot supply it.

## 3. Correct and verify within the round

1. Record the round number and candidate before editing.
2. Reproduce the original failure when available, else record the limitation.
3. Correct every instance of a defect class in this round.
   Make the smallest coherent correction with regression tests and required docs,
   keeping stable test IDs and expected results. Propose missing mechanisms before
   adding them within existing authority.
4. Run [verify-change](../verify-change/SKILL.md) on the finished edits for
   affected criteria and regressions.
5. Run [review-change](../review-change/SKILL.md) for fresh independent re-review
   of the correction and affected behavior, scoped by the review rules'
   re-review section, with required specialists. Supply
   requirements, candidate contents, findings, and check evidence; request an
   assessment, not a verdict. The correction's author cannot re-review it. Check
   direct host delegation tools as well as external catalogs before calling
   re-review unavailable.
6. Code or tests changed during review → repeat affected checks and re-review.

Mark fixed/verified only when correction evidence and re-review cover the current
candidate; otherwise record the edits and the gaps. Keep the count and verdict
across handoffs.

**Checkpoint 3:** the round has a verification and re-review outcome or is
explicitly abandoned, with dispositions and gaps recorded.

## 4. Report and stop

After the last edit and check, finish authorized records. Inspect the final patch
and staged and untracked contents. Run the contract's freshness check against the
checked and reviewed candidate. Return:

```text
Findings: finding | disposition | evidence | correction
Checks: command | candidate | result
Re-review: reviewer | coverage | verdict
Round: number | in progress, verdict, or abandoned | stopping condition
Freshness: branch/revision | final inspection | before/after identities | result
Decisions needed, gaps, next action:
```

Missing inspection or comparison leaves remediation incomplete.

**Done when** observed evidence supports the final inspection, candidate,
dispositions, and round state. A standalone request stops here. Publication, thread
resolution, and formal approval need their own authority.
