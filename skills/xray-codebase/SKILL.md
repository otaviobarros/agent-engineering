---
name: xray-codebase
description: X-ray a codebase or one area of it and return a visual HTML report of architecture friction and proposed improvements from proven patterns, such as explicit state machines, ports and adapters, and deep modules. Use for architecture reviews, refactoring direction, or finding why an area keeps breaking. Read-only; stops before planning.
---

# X-ray codebase

Find where the structure of the code makes change expensive or error-prone, and
propose proven patterns that remove that friction. Each proposal carries the
evidence and tradeoffs a team needs to decide. First read the
[contract core](references/workflow-contract.md), the
[visual report rules](references/visual-report.md), and the
[pattern catalog](references/patterns.md).

## 1. Scope and limits

- Identify the area and concern the user names. No area → the whole repository,
  ranked by hot spots. Record the repository and revision.
- Read governing instructions, architecture docs, glossary, and ADRs. An accepted
  decision constrains proposals: a proposal that contradicts one names it and
  states why it should be reopened. Use the project's terms in the report.
- The X-ray is read-only. Leave project files, branches, and the index unchanged.
  Probes go to scratch. Running existing tests is permitted; edits, plans in
  tracked files, and issues each need explicit authority.

**Checkpoint 1:** the scope, the revision, the governing decisions, and the
permitted actions are stated.

## 2. Find hot spots

Combine signals; one signal alone ranks nothing:

- **Churn:** commits per file over the last 12 months, from
  `git log --since=12.months --name-only --format=`.
- **Fix history:** commits whose subject marks a fix, per file.
- **Co-change:** files that change together in the same commits across module
  boundaries.
- **Size and coupling:** file length, function length, and import fan-in and
  fan-out.

A hot spot is a file or module high on churn or fixes and high on size or
coupling. Shallow history (fewer than 20 commits in scope) → rank by size,
coupling, and the user's direction, and state the limit as a Gap.

Map the modules in scope and their dependencies. Mark the hot spots on that map.

**Checkpoint 2:** the top hot spots have their numbers, and the module map exists.

## 3. Diagnose friction

Read each hot spot's code, its tests, and the fix commits that touched it. Name
the friction in one line with `file:line` evidence. Friction is a structural cause
that repeats, such as:

- one concept scattered across several files that must change together;
- the same condition or flag combination checked in several places;
- illegal states the data types allow, guarded by scattered checks;
- I/O mixed into domain rules, so tests need the network, clock, or database;
- a shallow module whose interface is as complex as its body;
- an external model or format leaking through the codebase.

Apply the deletion test to each suspect module: remove it in thought and see where
its complexity goes. Complexity that spreads to callers marks a module worth
keeping or deepening; complexity that vanishes marks a pass-through.

Record good structure too: areas with low churn and clear boundaries. The report
lists them as areas to leave alone.

**Checkpoint 3:** each friction has a `file:line`, the commits or co-change data
behind it, and the cost it causes.

## 4. Match patterns

For each friction, pick the catalog pattern whose signs match and whose
when-not conditions do not. Compare it with doing nothing and with one smaller
alternative. A friction with no matching pattern stays in the report as a
problem without a proposal.

Record for each proposal:

- files and evidence: `file:line`, churn, fix commits;
- the problem in the project's terms;
- the pattern and its source;
- the move in one line; the top recommendation also gets an after diagram;
- tradeoffs and the alternatives considered;
- a migration outline in small, separately shippable steps, with the first safe
  step;
- test impact: tests to add, tests that become simpler, and tests that break;
- risk level and its basis;
- strength: *Strong* (evidence at several sites and a clear payoff), *Worth
  exploring* (evidence at one site or an uncertain payoff), or *Speculative*
  (inferred from structure alone).

Rank candidates by friction removed against migration cost and risk. Pick one top
recommendation.

**Checkpoint 4:** every candidate has every field above, and the top recommendation
is named with its first safe step.

## 5. Build the report

Write the page with the visual report rules. Sections, in this order:

1. **Header.** The title names the top recommendation. The lede gives its
   strength and its first safe step.
2. **Decision board.** The candidates as numbered questions, ranked, with the
   grid placing each one by value and cost.
3. **Module map.** One diagram of the modules in scope with hot spots
   highlighted, at most 10 nodes. Under it, the hot-spot table: churn, fixes,
   size, and coupling. Choose the map's type from
   [Diagrams](references/visual-report.md#diagrams): `flowchart LR` for
   module dependencies, `architecture-beta` when services and stores matter. Add a
   `treemap-beta` of size or a monthly churn `xychart` only when it explains why a
   hot spot ranks high.
4. **Candidate route.** One stop per candidate, ranked. Each stop holds its chips
   (files, strength, churn), its points (problem, pattern and source, the move),
   and its question. The top recommendation's stop holds a before/after pair
   (`stateDiagram-v2` for a state machine). Details hold tradeoffs and
   alternatives, the migration outline, and test impact.
5. **Terminus.** Leave alone, one row per area whose structure works with its
   evidence, and the unknown box with the Gaps.

Run the render check.

**Checkpoint 5:** the page holds all five sections, every candidate stop carries
an evidence tag and every proposal field, and the render check passed or is
reported as unverified.

## 6. Report and stop

Return:

```text
Report: absolute path | render check result
Scope: area | revision | history window
Top recommendation: pattern | files | strength | first safe step
Other candidates: pattern | strength, one per line
Gaps:
```

**Done when** the report exists at the reported path and every candidate has
evidence, tradeoffs, a migration outline, and a strength. The X-ray changes no
project files. Adopting a candidate continues through plan-change, with the
candidate's stop as its input.
