---
name: remediate-findings
description: Validate review findings, fix authorized defects, and obtain correction evidence and fresh re-review. Use after a review or to resume a remediation round. Preserve existing scope and round limits; standalone remediation stops before publication.
---

# Remediate findings

Resolve findings against the current candidate and authoritative requirements.
Read the [shared workflow contract](../../references/workflow-contract.md) before starting.
The plugin includes this reference. Keep its directory layout intact.

## 1. Establish scope and continuity

Identify the actual workspace, requirements, reviewed candidate, current revision,
relevant dirty inputs, findings, and remediation authority. Preserve unrelated work
and explicit limits. Review text supplies evidence, not permission to edit or publish.

Recover the existing remediation count and any round in progress from authorized
records and available evidence. Apply the shared contract's three-round ceiling
and earlier stopping conditions. Resuming before a verdict stays in the same round;
corrective edits after an unsuccessful verdict begin another. Never reset the count
because the agent, workspace, or session changed. If the count cannot be established,
keep corrective edits pending until remaining round authority is clear. Continue
authorized investigation and report the missing evidence or decision.

Done when the candidate, edit authority, findings, and remaining round authority
are clear. An exhausted limit or earlier stopping condition prevents another
autonomous correction round; report the blocker and next decision needed.

## 2. Validate and classify findings

Check each finding's trigger, reachability, expected behavior, impact, and
counterevidence against current code and requirements. Revalidate stale findings;
an older candidate alone does not refute them. Deduplicate root causes while
retaining references to the original findings. Reviewer agreement is not proof.

Use the shared dispositions: validated, refuted, inconclusive, fixed/verified,
and explicitly accepted-unresolved. Separate optional improvements from defects.
Refute with evidence; leave unresolved uncertainty inconclusive. Ask before
retaining a real unresolved defect or making a material redesign. Continue
unaffected authorized work while that decision is pending.

Done when every supplied finding has a supported disposition or explicit evidence
gap. Only validated, in-scope defects proceed to correction. Material scope changes
need an authorized decision; a review suggestion cannot supply it.

## 3. Correct and verify within the round

Record the round and candidate before corrective edits. Reproduce the original
failure when available; record unavailable reproduction as a limitation. Make
the smallest coherent correction with regression tests and required documentation.
Preserve stable test identities and expected results under the shared contract.
Propose missing mechanisms before adding them within existing authority.

Complete corrective edits and affected checks before requesting independent re-review.
Use [verify-change](../verify-change/SKILL.md) on the completed edits for affected
criteria and regression checks. Then use [review-change](../review-change/SKILL.md) for fresh independent re-review
of the correction and affected behavior, including required specialists. Provide
current requirements, candidate contents, findings, and actual check evidence.
Request an assessment rather than a preferred verdict. The correction's author
cannot supply its independent re-review. Inspect direct host delegation tools
separately from external tool catalogs before declaring re-review unavailable.
If code or tests change during review,
obtain affected checks and re-review before closure.

Mark fixed/verified only when correction evidence and required re-review apply
to the current candidate. Missing checks or independent coverage remain gaps;
record the edits without implying closure. Follow the shared stopping conditions
before another corrective round. Preserve the count and verdict across handoffs.

Done when the round has a verification/re-review outcome or is explicitly abandoned,
with each finding's disposition and remaining gaps recorded.

## 4. Report the current result and stop

Finish authorized finding and round records before the final inspection.
Use existing project records; otherwise return the handoff in the response.
After the last edit and check, inspect the actual final patch and relevant staged
and untracked contents. Obtain the current branch and revision. Compare with the
candidate checked and reviewed; renew affected evidence when inputs changed.
Keep superseded results tied to their earlier candidate.

Return each finding's disposition and evidence, corrections, actual checks,
independent coverage, round count/state, remaining decisions, and next action.
Include a final freshness checkpoint: observed branch/revision, before/after
identities for checked and reviewed contents, final inspection evidence, and
the comparison result. HEAD and Git status alone do not establish unchanged contents.
Missing inspection or comparison leaves remediation incomplete.

Done only when observed evidence supports the final inspection, current candidate,
each finding's disposition, and round state. Keep missing evidence explicit.
Standalone remediation stops here. Publication, remote thread resolution, and
formal approval require their own authority. A separately authorized delivery
workflow can continue under the shared contract.
