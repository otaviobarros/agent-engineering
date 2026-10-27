---
name: review-change
description: Review a software change against requirements and project standards. Use for change, branch, or PR reviews. Return validated findings about bugs, security, and maintainability. Stop before remediation.
---

# Review change

Return evidence-backed findings for one candidate. First read the
[contract core](../../references/workflow-contract.md) and the
[review rules](../../references/review.md).

Each tool call resends the whole context, so batch reads: read both references and
the diff in one command, and the files you need to inspect in as few commands as
possible.

## 1. Pin the candidate

- Identify the repository, requirements, governing instructions, and the diff.
  Record base, revision, and relevant dirty inputs. For a PR, fetch its current
  head. Resolve an ambiguous target before judging it.
- Missing requirements → Spec coverage gap. Code and commit messages alone do not
  establish intended behavior.
- Run tests only under the review rules' test-execution limit.
- Edits, commits, remote comments, thread resolution, and approval each need their
  own authorization.

## 2. Choose reviewers

One fresh reviewer covers all five axes by default. Add a focused specialist only
for a material risk the change touches: security or privacy, money, schema or
migrations, concurrency, or a public contract. Risk sets this, not size.

- **Independence.** A fresh reviewer did not author the candidate and gets neutral
  context. An implementer reviewing its own work delegates. No delegation →
  report the missing independent review.
- **Delegation.** Each delegate gets the same candidate identity, requirements,
  scope, permissions, and its assignment. It returns findings, coverage, checks,
  and gaps, not code summaries. Delegates must see uncommitted inputs in scope; a
  worktree with only HEAD is a different candidate. Use only approved delegation
  destinations. Run at most three reviewers at once; reviewers spawn no reviewers.

## 3. Inspect

Read callers, callees, tests, and configuration beyond the diff as needed.

- **Standards:** cite the governing project rule; separate convention from preference.
- **Spec:** trace requirements and exclusions through code, tests, and behavior
  docs; find omissions and unintended changes.
- **Bugs:** trace reachable failures, including retries, concurrency, and
  recovery; check that tests detect the defect.
- **Quality:** coupling, state, abstraction cost. Propose a simpler form that keeps
  required behavior.
- **Security:** trust boundaries, permissions, data exposure, and dangerous
  operations from reachable input to effect.
- **Performance:** tie each concern to a reachable workload; label predictions
  unmeasured.

**Claims.** For changed docs, comments, or messages that state facts, list each
material claim, confirmed ones included. Mark it confirmed, contradicted, or
unverified against its governing source, cited as `file:line`. Cite the line that
sets or enforces the value, not the start of its file or function. An uncited claim
is unverified. Group claims only when source and conclusion match. Contradictions
become findings.

**Each finding.** Quote the motivating `file:line`; a finding you cannot quote is
unverified. Compare with the base to separate regressions from pre-existing issues.

**Clean verdict.** Before returning no findings, try the strongest plausible
counterexample. Record target, source, and result.

## 4. Validate and return

Validate and label findings under the review rules; votes do not decide
correctness. Order by impact: critical, high, medium, low. Recommend a material
redesign for decision; do not apply it. Run the contract's freshness check.
Unverified freshness or coverage → review incomplete.

Return this report in your final message even when findings are also saved
elsewhere. A saved file does not change its shape. Keep all eight numbered
labels, in this order; do not merge, rename, or move them. Fill every slot;
write `none` when empty.

```text
1. Candidate: base, head, dirty inputs | freshness: unchanged, refreshed, or unverified
2. Arrangement: reviewers, axes, specialists, missing coverage
3. Findings by impact, or "no findings":
   label | severity | axis | location | trigger | expected vs observed | evidence | remedy
4. Claims: claim | changed location | status | source file:line
5. Coverage: axis | files or interfaces inspected | not checked
6. Checks: existing evidence | tests run | tests not run
7. Clean verdict only: counterexample | source | result
8. Open questions, gaps, next action
```

Fictional rows:

```text
4. "Tokens expire after 24 hours" | docs/api.md:12 | confirmed | src/auth/config.py:8
5. Security | src/auth/session.py, POST /login | rate limiting
```

"No findings" never implies unrun checks passed. Standalone review ends here. In
delivery mode, return the report to the caller.
