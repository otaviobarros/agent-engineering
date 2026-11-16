# Changelog

Notable changes to the agent-engineering plugin, newest first. Each released
version has a matching Git tag and GitHub Release. Versions follow
[Semantic Versioning](https://semver.org/).

## Unreleased

## 0.6.0

### diagnose-issue

- New skill: diagnose a bug, failing check, or unexplained behavior, starting
  from a working reproduction and ending at an evidenced root cause. It stops
  before the fix and hands off a named regression test.

### respond-to-review

- New skill: respond to review comments on your own pull request. It checks
  each comment against the code, fixes validated defects, replies with evidence,
  and resolves threads within your authority.

### merge-change

- New skill: merge a pull request after checking that review is resolved,
  required checks pass, and the reviewed head is current. It can also reconcile
  an uncertain merge attempt.

### verify-change

- Reports end with a coverage map: one row per acceptance criterion, with each
  covering test, its evidence level, the result, and any limitation. Criteria
  with no covering check are listed as gaps.
- Each test that a change adds gets a value card that states when the test
  fails.

### review-change and review-pr

- Findings use one classification: Important, Nit, or Pre-existing. The label
  sets report order and, in PR reviews, whether a thread blocks.
- An Important finding needs traced or reproduced evidence. A finding below that
  bar is reported as an open question, with the check that would settle it.
- PR reviews add a priority only when the project defines a priority scale.
- Reviews default to quick mode with one fresh reviewer, including PR reviews
  and large diffs. Experimental deep mode uses up to three reviewers only when
  explicitly requested; asking for a thorough review alone keeps quick mode.
  Risk passes trace behavior across files in either mode, including identities,
  retries, and completion order.
- Re-review after a fix covers only the correction, sent to the reviewer that made
  the earlier review when the host allows it.

### Planning and verification

- Test IDs are optional. Projects without an ID scheme can use behavior slugs.

### setup-project

- The setup guide is shorter. Branch-only detail moved into the project guide.
- Discovery is handed to a low-cost subagent when the host has one, on both
  initial setup and refresh, and it now includes hidden configuration
  directories such as `.github/`.
- Setup runs no project tests, linters, or checks, even when project
  instructions ask for them. It reports that project checks were not run.
- On refresh, setup edits only its own lines and keeps text you wrote word for
  word.
- Each practice row has exactly one disposition value; explanations go in the
  rationale column.

### Documentation

- Adds this changelog. Each GitHub Release now uses the matching section as its
  notes.

Existing skill names and entry points are unchanged. No migration steps are
required; update through your host's plugin manager. The plugin remains
experimental, and results depend on the model, host, and project.

## 0.5.0

### implement-change

- Adds a reuse-first ladder: use an existing helper, then the standard library,
  then an installed dependency, and only then new code.
- Searches the codebase for an existing parser, formatter or validator before
  writing one, and states what it found.
- Leaves out unrequested extras and names them; uses a `Not built:` line when the
  task mentions speculative or future needs.
- Never cuts trust-boundary validation, data-loss handling, security,
  accessibility, or a test for new non-trivial logic.

### plan-change

- Uses the same reuse-first ladder when choosing an approach.

### review-change

- Shorter review path focused on evidence and the behavior a change affects.
- Defaults to one fresh reviewer covering all five axes; adds specialists for
  material security, privacy, money, schema/migration, concurrency or
  public-contract risks.
- Labels findings Important, Nit or Pre-existing.
- Keeps the numbered final report even when findings are also saved to a file.
- Re-reviews more widely when a correction is large, changes the design, or
  touches high-risk areas.

### review-pr

- Marks Important findings blocking, and Nits and Pre-existing findings
  non-blocking.
- Doesn't repost a thread that repeats an earlier one.
- The summary opens with finding counts by label and says plainly when nothing
  needs fixing.

### remediate-findings

- Fixes every instance of a defect class in the same round.
- Scopes the re-review with the shared re-review rules.

### setup-project

- Guides focus on conventions the code doesn't show, commands taken from the
  project, scoped rules, and how standards are enforced.
- On refresh, checks that linked paths, named sections and listed commands still
  exist, and flags contradictions with other sources.

### All skills

- New shared writing rules make reports, PR descriptions, commit messages and
  comments shorter without dropping check results, uncertainty or gaps.

The plugin remains experimental. Behavioral checks for these changes ran on
Codex. Claude Code behavior isn't verified for them, and results depend on the
model, host and project.

## 0.4.0

This release makes the nine workflow skills lighter to load and stricter about
what they report as done.

- Every skill now reads a smaller core workflow contract (about 42% fewer
  tokens). Phase-specific rules moved to new verification, review, and
  publication references that load only in the phases that need them.
- Change reviews require evidence for each claim, and acceptance-criterion
  evidence now carries across planning, verification, and publishing handoffs.
- A criterion whose required check did not run is reported as unverified instead
  of complete.
- When Git writes are blocked, skills stay inside the workspace boundaries
  instead of working around the block.
- Codex can install the plugin from this repository's marketplace file
  (`.agents/plugins/marketplace.json`).
- The README adds a 30-second overview and a "How it works" section.

Skill names and entry points are unchanged. No migration steps are required;
update through your host's plugin manager.

## 0.3.2

This update makes the plugin's execution, data handling, and support boundaries
easier to inspect.

- Document which project data host tools may read, write, or send to GitHub and
  configured Git remotes.
- Expand the privacy policy with personal Git metadata, local and remote
  retention, and provider privacy links.
- Add a security policy with GitHub private vulnerability reporting.
- Add concise prerequisites, troubleshooting, and disposable evaluation guidance
  to the README.

The nine workflow skills are unchanged. No breaking changes or migration steps
are required; update through your host's plugin manager to receive the new
documentation.

## 0.3.1

- Added the plugin icon and documentation, support, and privacy-policy links for
  Claude Code listings.
- Added a privacy policy explaining plugin data handling and host/service
  responsibilities.

Skill behavior is unchanged from v0.3.0.

## 0.3.0

- Strengthened `setup-project` with codebase discovery and a low-cost read-only
  subagent when available.
- Added context-informed questions and improvement recommendations with explicit
  adoption choices.
- Added a documentation baseline and optional default workflow routing while
  preserving existing project authorities.

## 0.2.2

- Made project test execution opt-in during change and PR reviews, including
  delegated reviews.
- Kept reviews focused on source changes and existing evidence; delivery
  verification remains unchanged.

## 0.2.1

- Added a plugin icon and cover artwork.
- Refreshed the README with clearer workflow examples and recommended project
  setup guidance.

## 0.2.0

- Expanded the plugin from two to nine skills, adding setup, implementation,
  verification, review, remediation, publication, and PR review.
- Connected the delivery phases through shared scope, evidence, and
  authorization rules.
- Added prioritized inline PR findings, review summaries, and approval handling.

## 0.1.1

- Moved plugin manifests, skills, and shared references to the repository root
  for a simpler installation layout.
- Preserved the planning and delivery skill behavior.

## 0.1.0

Initial public plugin release.

- Introduced `plan-change` for scoped plans and acceptance criteria.
- Introduced `deliver-change` for guided implementation, verification,
  independent review, and authorized delivery.
- Included a shared workflow contract and plugin metadata for Codex and Claude
  Code.
