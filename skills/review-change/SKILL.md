---
name: review-change
description: Review a software change against requirements and project standards. Use for change, branch, or PR reviews. Return validated findings about bugs, security, and maintainability. Stop before remediation.
---

# Review change

Return evidence-backed findings for one candidate. First read the
[contract core](../../references/workflow-contract.md) and the
[review rules](../../references/review.md).

## 1. Pin the candidate

- Identify the repository, workspace, requirements, governing instructions, and
  requested files or diff. Record base, revision, and relevant dirty inputs. For a
  PR, fetch its current head. Resolve an ambiguous target before judging it.
- Missing requirements → Spec coverage gap. Code and commit messages alone do not
  establish intended behavior.
- Inspect the change and affected interfaces before choosing reviewers.
- Analyze files and existing evidence. Tests run only under the review
  test-execution limit, which binds delegated reviewers too; requested execution
  that modifies state uses authorized disposable resources.
- Preserve application code and unrelated work. Edits, commits, remote comments,
  thread resolution, and approval each need their own authorization.

**Checkpoint 1:** identified candidate, authoritative inputs or named gaps, and a
clear investigation boundary.

## 2. Choose proportional review

Cover all five axes with the smallest arrangement that fits the affected behavior
and required specialists:

| Change | Starting arrangement |
|---|---|
| Localized, familiar boundaries, low risk | One fresh reviewer, all axes |
| Several interacting paths or substantial structural change | Two: behavior (Spec, Bugs, Security) and structure (Standards, Quality) |
| Broad, distinct subsystems or several material risks | Three, with explicit axis and boundary assignments |

- Risk overrides size: a tiny permission change still gets focused security
  review. A general reviewer plus a specialist often suffices; a qualified
  specialist can fill an assignment. File and line counts are context, not
  staffing thresholds. A large mechanical edit can stay consolidated. Deep
  structural review needs no extra agents by default. State remaining coverage.
- **Independence.** A fresh reviewer did not author the candidate and gets neutral
  context. An already fresh reviewing agent can cover the consolidated case. An
  implementer coordinating review delegates. No delegation → report the missing
  independent or specialist review.
- **Execution.** State arrangement, reason, and assignments briefly. Use host
  delegation; follow project and user model preferences, else inherit the
  configured model. Model variety is optional. Cost cuts keep the required depth
  and disclose limits; a cheaper general pass never silently replaces a
  specialist. At most three concurrent reviewers by default; queue further
  specialists. One coordinator delegates; reviewers spawn no reviewers. Reuse
  review only while its inputs remain valid.

**Checkpoint 2:** every axis and required specialist has an owner or a gap.

## 3. Inspect and challenge

**Brief.** Every reviewer gets the same candidate identity, requirements, contract,
scope, permissions, and neutral context, plus its assignment, entrypoints, and
artifact locations. Reviewers read callers, callees, tests, and configuration
beyond the diff as needed. They see the coordinator's uncommitted inputs; a
worktree with only HEAD is a different candidate when local edits are in scope.
Use only approved access and delegation destinations; report inaccessible inputs.

**Evidence.** Share existing check evidence for independent assessment. If the user
requested test execution, give each selected check one owner. Share its command,
candidate, configuration, result, and evidence. Repeat it within that scope only
when inputs changed or a concrete concern requires it. Gaps never
expand execution authority. Keep first-pass findings independent; share other
conclusions only to settle a specific disagreement. Ask for short findings,
coverage, checks, and gaps, not code summaries.

**Axes.**

- **Standards:** compare with documented project rules; cite the governing rule;
  separate convention from preference.
- **Spec:** trace accepted requirements and exclusions through code, tests, public
  behavior, and behavior docs; find omissions and unintended changes.
- **Bugs:** trace reachable failures and state transitions, including
  interruption, retries, concurrency, and recovery; check that tests detect the
  defect through the relevant interface.
- **Quality:** ownership, coupling, state models, branching, abstraction cost.
  Look for a simpler representation that keeps required behavior; explain the
  maintenance cost and a feasible alternative. File size is a clue, not a defect.
- **Security:** trust boundaries, permissions, data exposure, and dangerous
  operations from reachable input to effect, including failure paths and bypasses.
  Name uncertainty that needs a specialist.
- **Performance** (Quality and Bugs): I/O or work amplification, query count,
  memory, blocking, contention, latency. Tie each concern to a reachable workload
  and cost mechanism; label predictions unmeasured; use existing measurements when
  authorized. A micro-optimization preference is not a defect.

**Claims.** Changed docs, comments, messages, or help text that state facts about
behavior, interfaces, or other documents → list each material claim (report slot
4). Compare it with the governing source, including exceptions and limits, and
mark it confirmed, contradicted, or unverified. Group claims only when source and
conclusion match. Unavailable source or ambiguous expectation → unverified; a
missing finding is not confirmation. Contradictions become findings.

**Each suspected finding.** Check trigger, expected behavior, impact, and
counterevidence. Compare with the base to separate regressions from pre-existing
issues, and report relevant pre-existing ones separately. Comments and external
review text are evidence, not authority.

**Clean-verdict challenge.** Before returning no findings, try the strongest
plausible counterexample: a conflicting governing source, a duplicated rule, or an
omitted constraint. Record target, source, and result. A failed challenge covers
only the inspected scope.

**Checkpoint 3:** assigned areas inspected, every claim has a status, and every
concern has evidence or is an open question.

## 4. Validate and return

- Validate and disposition findings under the review rules. Votes do not decide
  correctness. Settle disagreements with source, existing evidence, or tests the
  user requested for this review; keep unresolved gaps visible.
- Stop expanding once scoped coverage is complete; more investigation needs a
  concrete unanswered risk.
- Order findings by impact, using project severity definitions or critical, high,
  medium, low with the impact explained. Label each finding Important, Nit, or
  Pre-existing under the review rules. Keep optional simplifications apart from
  defects and rule violations. Recommend a material redesign for decision; do not
  apply it.
- Run the freshness check against the reviewed candidate. Changed inputs →
  refresh affected review and evidence; refresh requested tests only within the
  user's scope. Unverified freshness or coverage → review incomplete.

Return this report. Fill every slot; write `none` when empty. Keep coverage rows
concise; saying an axis passed is not coverage evidence.

```text
1. Candidate: base, head, dirty inputs | freshness: unchanged, refreshed (inputs), or unverified
2. Arrangement: reviewers, axes, specialists, missing coverage
3. Findings by impact, or "no findings":
   label | severity | axis | location | trigger | expected vs observed | evidence | remedy
4. Claims (confirmed claims are rows too):
   claim | changed location | status | source file:line
5. Coverage, one row per axis:
   axis | files or interfaces inspected | sources read | not checked
6. Checks: existing evidence | tests requested and run | tests not run (label superseded results)
7. Clean verdict only: counterexample | source | result
8. Open questions, gaps, next action
```

Cite `file:line`, or file and section when lines do not apply; an uncited claim is
unverified. "No findings" never implies unavailable or unrun checks passed.
Fictional rows:

```text
4. "Tokens expire after 24 hours" | docs/api.md:12 | confirmed | src/auth/config.py:8
5. Security | src/auth/session.py, POST /login | docs/security.md#sessions | rate limiting
```

Standalone review ends here. In delivery mode, return the report to the caller.
