---
name: explain-change
description: Explain a pull request, branch, or diff as a visual HTML guide for the person who approves it. Use when someone wants to understand a change before approving it, see its decisions, risks, and app impact, or know where to look first. Returns a guide with no verdict and changes nothing.
---

# Explain change

Build a visual guide that lets the approver understand one change, see where it
can hurt the application, and decide with less effort. The guide directs the
approver's attention and questions; the approver keeps the decision. First read the
[contract core](references/workflow-contract.md), the
[visual report rules](references/visual-report.md), and the
[evidence ladder](references/verification.md#coverage-map).

Batch reads: gather the diff, the change's metadata, and the governing
instructions in one command where the host allows it.

## 1. Pin the change and the limits

- Identify the target: a PR number or URL, a branch against its base, or a patch.
  Resolve an ambiguous target before reading it. Record the repository, base and
  head revisions, and the diff's file and line counts.
- Read a PR through `gh pr view` and `gh pr diff`, plus its commits, linked issue,
  and review threads. Read a branch through `git diff <base>...<head>` from the
  merge base.
- The guide is read-only. Leave the working tree, index, branch, and stash
  unchanged. Run tests only when the user asks; otherwise coverage evidence is at
  most *traced*. Posting the guide or a comment, and writing it into tracked files,
  each need explicit authority.

**Checkpoint 1:** the target, its revisions, and the permitted actions are stated.

## 2. Collect the stated intent

Read what the author and the project say the change must do: the PR body, linked
issue, plan, commit messages, review threads, governing instructions, and ADRs.
Write the intent in one or two lines and cite its sources. No stated intent →
Gap, and describe what the diff does without judging it against a goal.

Compare intent with the diff in both directions:

- Promised but missing: intent the diff does not implement.
- Present but unstated: behavior the diff changes that no source mentions.

**Checkpoint 2:** the intent has sources or is a Gap, and each mismatch has a
`file:line`.

## 3. Map the change

- Group the changed files into areas by concern, never by directory alone. Give
  each file a kind: behavior, interface, data or migration, configuration, test,
  generated, or docs.
- Set a reading order: the core behavior first, then its interfaces and callers,
  then tests, then configuration and docs. Mark generated and mechanical files as
  skim.
- Read the code around each hunk, not the hunk alone. For each changed function,
  type, schema, endpoint, event, or configuration key, search for its callers and
  consumers. Those that the diff leaves untouched form the blast radius.

**Checkpoint 3:** every changed file sits in one area with a kind, and every changed
public symbol has its callers listed or a Gap stating the search that failed.

## 4. Assess each area

For each area, record:

- **Decisions.** Each design choice, its alternatives, and its source. Tag a
  decision you deduce from the code *inferred*.
- **Risks.** Use the levels in the visual report rules. Look hardest where a
  changed line touches authentication or permissions, security or privacy, money,
  data and migrations, concurrency or retries, error handling, performance, or a
  public contract. Trace each such risk through its callers to the effect a user or
  external system sees.
- **Coverage.** The tests that exercise the area, each with its evidence level and
  what a pass does not prove. Name behavior that no test reaches.
- **Gaps.** What you could not establish from the sources.

Then write the decision list, ranked by risk. Each row is a question the approver
answers before approving, and it is the only place its risk appears. A good
question:

- points to one `file:line`;
- needs the approver's judgment or knowledge the diff does not hold;
- states, in its details, what makes the answer safe and what makes it unsafe.

Write one row for every High or Medium risk and every intent mismatch; merge rows
that share a cause. Low risks stay in their area's details. A likely defect enters
the list with its evidence and the note that `review-change` can validate it. The
guide gives no approval, rejection, or merge recommendation.

**Checkpoint 4:** every area has its decisions, risks, coverage, and gaps, and
every High or Medium risk and mismatch has a decision row.

## 5. Build the guide

Write the page with the visual report rules. Sections, in this order:

1. **Header.** The title states what the change delivers. The lede gives the
   stated intent with its evidence tag, the highest level, and the number of
   questions.
2. **Decision board.** The decision list as numbered questions, with the risk grid
   placing each one by impact and likelihood.
3. **Where the change lands.** A proportion bar of lines added per area, then the
   area table in reading order: name linked to its stop, files, lines added and
   removed, level.
4. **How it works.** One diagram of the affected flow: changed nodes highlighted,
   plus the untouched callers, consumers, data, and external systems that form the
   blast radius. Add a step strip when the flow is a straight sequence the reader
   should follow first. Add a second diagram only when it answers a question the
   flow cannot, choosing the type from
   [Diagrams](references/visual-report.md#diagrams): a `sequenceDiagram` or
   `swimlane-beta` for a call order across services, a `stateDiagram-v2` for added
   or altered states, an `erDiagram` for a schema change, a `classDiagram` for a
   changed interface.
5. **Review route.** One stop per area, in reading order. Each stop holds its
   chips (files, coverage level, skim marks), its points (purpose, coverage and
   what a pass does not prove), its transfers to external systems, its questions
   from the decision list, a before/after pair where a structure changes, and a
   detail with its Low risks and tests.
6. **Terminus.** The decisions you inherit as a decision table, and the unknown
   box with the Gaps.

Run the render check.

**Checkpoint 5:** the page holds all six sections, every question sits at its
area's stop with an evidence tag, and the render check passed or is reported as
unverified.

## 6. Report and stop

Return:

```text
Guide: absolute path | render check result
Change: target | base..head | files, +added -removed
Delivers: one or two lines
Highest risk: level | title | file:line
Decide: top three questions, each with file:line
Gaps:
```

**Done when** the guide exists at the reported path, every changed file appears
in one area, and every High or Medium risk and intent mismatch has a decision
row. The guide changes no project files and records no review decision.
Validating a suspected defect continues through review-change.
