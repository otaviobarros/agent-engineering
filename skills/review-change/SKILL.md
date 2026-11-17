---
name: review-change
description: Review a software change against requirements and project standards. Use for change, branch, or PR reviews. Return validated findings about bugs, security, and maintainability. Stop before remediation.
---

# Review change

Return evidence-backed findings for one candidate. First read the
[contract core](references/workflow-contract.md) and the
[review rules](references/review.md).

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

## 2. Choose the mode

Read the project's authoritative requirements source before assigning the review.
If none is named, read README and relevant docs before reporting a Spec coverage gap.
Gather the diff, the changed-file list, and the requirements once. Give every
reviewer that same copy, so no reviewer gathers the candidate again.

Choose **quick** by default, regardless of diff size or the calling skill.
Choose experimental **deep** mode only when the user explicitly requests a deep
review. A request to be thorough alone does not select deep. Calling skills
forward the user's mode request; they do not select deep on their own.
A user request for a "quick review" takes precedence. A risk line adds a risk
pass in either mode.

- **Risk pass.** A focused checklist pass, inside the reviewer's own context, for
  each material risk a changed line touches: authentication or permissions,
  security or privacy, money, schema or migrations, concurrency, or a public
  contract. Trace the changed behavior through its callers, adapters, and consumers.
  Check which identity, scope, version, and completion rule each side uses. For
  asynchronous work, trace a retry and an older completion arriving after newer
  state. Use the governing contract to decide whether each ordering is allowed.
- **Quick.** One fresh reviewer covers every axis in one context and runs every
  risk pass.
- **Deep (experimental).** Split the diff into at most three partitions by context.
  Keep files that change together in one partition. Give the files with a risk line their
  own partition. One fresh reviewer takes each partition, covers every axis, and
  runs the risk passes for its files. Split by context, never by axis. A caller
  that is a fresh reviewer may take one partition itself. Assign each behavior
  that crosses partitions one owner for an end-to-end trace. Reconcile those
  traces before merging findings.
- **No delegation.** Deep needs at least one delegate. The host cannot delegate →
  run quick, and report the missing deep reviewers in the Arrangement line.
- **Independence.** A fresh reviewer did not author the candidate and gets neutral
  context. An implementer reviewing its own work delegates, in quick mode too. No
  delegation → report the missing independent review.
- **Delegation.** Each delegate gets the shared copy of the diff, file list, and
  requirements, plus scope, permissions, and its partition. It reads beyond its
  partition as needed. It returns findings, coverage, checks, and gaps, not code
  summaries. Delegates must see uncommitted inputs in scope; a worktree with only
  HEAD is a different candidate. Use only approved delegation destinations.
  Reviewers spawn no reviewers.

## 3. Inspect

Read callers, callees, tests, and configuration beyond the diff as needed.

- **Standards:** cite the governing project rule; separate convention from preference.
- **Spec:** trace requirements and exclusions through code, tests, and behavior
  docs; find omissions and unintended changes.
- **Bugs:** trace reachable failures, including retries, concurrency, and
  recovery; check that tests detect the defect.
- **Quality:** coupling, state, abstraction cost. Apply a structural lens: a file
  that crosses 1,000 lines, special cases scattered across callers, a wrapper that
  adds nothing, a simpler shape that removes branches. Propose a simpler form that
  keeps required behavior.
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

**Declined to judge.** List each behavior you considered and set aside as outside
the requirements, with the reason. The caller rules on each line; nothing set
aside drops silently.

**Existing PR comments.** Read them only after your own pass. Then merge your
findings with them and mark the duplicates.

**Each finding.** Quote the motivating `file:line`; a finding you cannot quote is
unverified. Compare with the base to separate regressions from pre-existing issues.

**Clean verdict.** Before returning no findings, try the strongest plausible
counterexample. Record target, source, and result.

## 4. Validate and return

Merge the reports of deep-mode reviewers and deduplicate root causes across
partitions. Validate and label findings under the review rules, including the
evidence gate; votes do not decide correctness. Order by label: Important, Nit, Pre-existing.
Recommend a material
redesign for decision; do not apply it. Run the contract's freshness check.
Unverified freshness or coverage → review incomplete.

Write each requested report artifact. Check its format and consolidated findings
before returning. Return this report in your final message even when findings are
also saved elsewhere. A saved file does not change its shape. Keep all eight numbered
labels, in this order; do not merge, rename, or move them. Fill every slot;
write `none` when empty.

```text
1. Candidate: base, head, dirty inputs | freshness: unchanged, refreshed, or unverified
2. Arrangement: mode | trigger | reviewers and partitions | risk passes | missing coverage | how to ask for the other mode
3. Findings by label, or "no findings":
   label | axis | location | trigger | expected vs observed | evidence: traced or reproduced | remedy
4. Claims: claim | changed location | status | source file:line
5. Coverage: axis | files or interfaces inspected | not checked
6. Checks: existing evidence | tests run | tests not run
7. Clean verdict only: counterexample | source | result
8. Declined to judge (behavior | reason); open questions (inconclusive findings: unconfirmed step, settling check); gaps; next action
```

Fictional rows:

```text
2. deep (experimental) | explicit user request | 2: db/, api/ | migrations, public contract | none | ask for a "quick review"
4. "Tokens expire after 24 hours" | docs/api.md:12 | confirmed | src/auth/config.py:8
5. Security | src/auth/session.py, POST /login | rate limiting
```

"No findings" never implies unrun checks passed. Standalone review ends here. In
delivery mode, return the report to the caller.
