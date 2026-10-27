# Project-guide format

Use this format only when a project needs a new context map or its existing guide
benefits from these fields. Preserve the existing document's name, structure, and owner
where sufficient. This is human-readable Markdown, not executable configuration.

## Discovery

Start with instruction entrypoints, the directory inventory, manifests, and documentation
indexes. The discovery agent reads representative source and tests across major areas:

- Entrypoints, package dependencies, module boundaries, and caller-facing interfaces.
- Domain models, persistence, external integrations, UI flows, and trust boundaries where present.
- Recurring error handling, validation, naming, and test patterns, including exceptions.
- Standards and rule IDs, ADRs, vocabulary such as `GLOSSARY.md` or `CONTEXT.md`,
  check configuration, CI, and collaboration/environment guidance.

Return a compact map: area, representative paths, observed pattern, documented authority,
confidence or unresolved question. Add coverage, excluded areas, and specific documentation
gaps or improvement candidates with evidence. Read-only discovery inspects commands;
it does not run project tests, bootstrap scripts, or remote operations.
The user's request and project instructions and standards govern, under the host's
instruction hierarchy. As evidence of what is enforced, weigh tool configuration and CI
first, then ADRs and docs, then the dominant code pattern as observation only. Report
conflicts with confidence and counterexample paths. Never resolve them by choosing the
implementation or a tool configuration as policy.
The setup owner checks material evidence and owns the recommendations and interview.

## Documentation baseline

Assess every row. Documentation coverage is expected during setup; the filenames below
are examples, not required scaffolding or prerequisites for invoking other skills.
Reuse existing owners. Cover small projects in fewer documents and apply package scopes
in monorepos. Mark a missing topic as a gap, or not applicable with a reason.

| Topic | Useful documented outcome | Recommendation when missing |
|---|---|---|
| Purpose and architecture | Product purpose, important constraints, and a navigation map: each area's entry files, owner, and non-obvious rules | Draft the map from inspected code, linking files instead of narrating modules; confirm uncertain intent |
| Engineering standards | Index of applicable rules with task/path triggers and exceptions | Propose a small index; stable IDs for rules that need references, preserving existing IDs |
| Verification | Check catalogs, working directories, important behavior, test identity rules, and real-interface procedures | Link executable configuration; propose missing procedures without implementing a harness |
| Work and collaboration | Requirements owner, tracker or local alternative, commit/branch/PR conventions | Ask unresolved choices; a hosted tracker and stacked PRs are optional |
| Environment | Setup/configuration sources, safe local isolation, worktree/remote guidance when relevant, and cleanup | Document observed procedures; flag unverified commands and unresolved environment ownership |
| Decisions and vocabulary | Where significant decisions and domain terms are recorded and when to read them | Propose an ADR/glossary convention; add real accepted content when justified |
| Workflow selection | On-demand use or accepted default routing, including task limits | Ask explicitly; retain phase boundaries and publication permissions |

Document observed patterns with evidence before proposing their promotion to standards.
Use the interview to challenge inconsistencies and explain improvements that suit the
codebase. An accepted documentation task can record current architecture; it cannot
silently make that architecture a permanent requirement. New policies need acceptance.
ADRs record actual significant decisions and their tradeoffs, not guessed history.
Rule IDs, acceptance-criterion IDs, and test-case IDs remain separate.

## What the guide owns

The guide owns pointers, applicability, and setup decisions whose owner is not
already elsewhere. Refer to existing policies rather than copying them. Applicable
project instructions and the host's instruction hierarchy still govern. This guide
does not grant permissions or replace standards, accepted ADRs, or task requirements.

Use a short scope statement and a source table. Each row answers: what concern,
when it applies, and which repository-relative file/section owns it. For a monorepo,
include the package scope and its instruction entrypoint; root rules do not erase
applicable local rules. Put area-specific rules in that area's instruction file or a
path-scoped rule file the host supports. Relative links resolve from the guide's directory, not repo root.

Map baseline topics to their existing owners where available:

- Standards index and original stable rule IDs, with task/path triggers.
- Architecture, accepted decisions and vocabulary owners.
- Requirements and tracker conventions; resolve live issue state at task time.
- Manifests, lockfiles, command/test catalogs, case-ID validation and working directories.
- Commit, branch, PR and dependent-stack conventions.
- Development, environment isolation, worktree/remote bootstrap and cleanup guidance.

Preserve privacy: no secrets, credential-bearing URLs, customer data, personal absolute
paths, raw logs, copied environment values, or cached authentication claims.
Record source absence as unknown or not established, not as permission to invent rules.

## Adoption record

Record the selected documentation approach: **Preserve and complement existing standards**
or **Adopt our recommended baseline**. Also record workflow selection separately:
**On demand** or **Default for matching tasks**. Reuse existing accepted choices; an unanswered
choice stays pending. Neither approach overrides current authorities or permits migration.
Attribute the selection to an explicit user choice or an existing accepted record,
not an inference from the requirement to respect project authorities.

Use a short table for relevant practices: practice, disposition, source or decision
reference, enforcement (lint rule, CI check, hook, CODEOWNERS, or prose only), scope
and rationale. Mark each practice as:

- **Established**: governed by an existing source; link to that owner.
- **Accepted**: an explicitly adopted setup choice without another owner; record why.
- **Proposed**: an optional improvement awaiting adoption; it does not block existing work.
- **Pending**: a material unresolved choice; name only the dependent work it blocks.
- **Declined**: a recommendation the user rejected; retain it to avoid proposing it again.

Practices required by applicable authorities, including the shared workflow contract,
are Established. A missing mechanism can be Proposed without making its governing
requirement optional. New practices need their own adoption decision.
Separate the governing requirement from any proposed mechanism in different rows.
For example, a required test-identity rule is Established even when a catalog is Proposed.
Use only the five dispositions above for practices. Put documentation coverage gaps
and not-applicable topics in a separate coverage column or section, not as dispositions.

Link externally owned decisions rather than copying them. An approach selection is
not blanket acceptance of practices. Preserve accepted choices and user-authored notes.
Replacements of existing policy remain proposals for a separately scoped change.

## Workflow adoption

For accepted default routing, show the project owner a concise instruction block before
writing it to the applicable `AGENTS.md` or `CLAUDE.md`. Adapt the following intent map
to installed skills; the user's requested outcome and limits select the scope.

| Requested outcome | Skill |
|---|---|
| Project setup or refresh | `setup-project` |
| Plan only | `plan-change` |
| Full implementation workflow | `deliver-change` |
| Implement an accepted slice only | `implement-change` |
| Verify only | `verify-change` |
| Analyze a change | `review-change` |
| Review a GitHub PR | `review-pr`, preserving report-only or feedback permissions |
| Correct review findings | `remediate-findings` |
| Authorized commit, push, or draft PR | `publish-change` |

Keep the always-loaded instruction short. For example:

> For development tasks, use the installed agent-engineering skill matching the requested
> outcome. Use `deliver-change` for full implementation; use the relevant phase skill
> for narrower requests. Read the project workflow guide for routing and
> applicable standards. Explicit task limits and project authorities govern. Report a
> missing skill; do not treat this reference as permission to install or publish.

Add the actual project guide's relative link from the entrypoint. Keep the routing table
in the guide or an existing owner instead of copying it into every host instruction.
If the guide is itself the instruction entrypoint, a second pointer is unnecessary.
On-demand selection does not add default-routing instructions. Existing independently
accepted workflow rules still apply until their owner authorizes a change.

Skill selection does not authorize tests during review, external PR comments, commits,
push, approval, merge, or deployment beyond the user's task authority. A PR link alone
does not request a review or publication. Default routing remains agent-followed guidance;
do not add hooks, a persistent mode, or an orchestrator as part of setup.

## Example shape

The paths below are fictional examples, not required project filenames or new sources
to scaffold. Replace them with inspected sources; omit rows that do not apply.

```markdown
# Project workflow guide

Scope: this repository; package rules apply within the paths named below.
Purpose: find current project authorities. This map grants no execution permissions.

| Concern | Read when / scope | Authoritative source |
|---|---|---|
| Instructions | Every task | [Agent guide](../AGENTS.md) |
| Engineering standards | Changed behavior; preserve existing rule IDs | [Standards index](engineering.md) |
| UI conventions | Changes under apps/web | [Web instructions](../apps/web/AGENTS.md), [UI rules](engineering.md#ui) |
| Architecture and ADRs | Interfaces, ownership, significant tradeoffs | [Decision index](adr/README.md) |
| Requirements/tracker | Planning, issue or PR work | [Work conventions](work.md) |
| Stack and checks | Identify current versions/commands; cwd: repository root | [Manifest](../package.json), [Check guide](testing.md) |
| Worktrees and environments | Bootstrap or drive an application | [Environment guide](environment.md) |

## Adoption record

Approach: Preserve and complement existing standards (selected by the user).
Workflow selection: On demand (selected by the user).

| Practice | Disposition | Source or decision | Enforcement | Scope and rationale |
|---|---|---|---|---|
| Engineering rules | Established | [Standards index](engineering.md) | Lint and CI | Applicable paths; preserve existing IDs |
| Standards navigation | Proposed | No adoption decision | Prose only | Add reading triggers if rules become hard to find; no work blocked |

Add accepted setup choices only when they have no other owner. Name material pending
choices and their actual blockers. The example rows are illustrative, not adopted policy.
```

If no existing entrypoint points here, add a short link from the appropriate existing
agent instructions within edit authority. State when the guide applies, for example:
“For planning, implementation, verification, and review, read the project workflow guide.”
Use the actual relative link. When `CLAUDE.md` imports `AGENTS.md`, one pointer in
`AGENTS.md` is sufficient. With independent entrypoints, add pointers only where needed
and authorized. Do not copy the whole guide into host files.
Do not create an import loop when the map links back to those instructions.

## Consumption and refresh

Confirm the chosen host instruction/import chain reaches the guide without loops.
Check referenced skill availability through host discovery. If unavailable, preserve
the accepted choice but report activation as unverified; do not install anything.
Each phase follows applicable pointers and reads current sources before relying on
them. A missing source or conflicting claim leaves that topic unresolved; keep
unaffected work moving. The map's existence is not evidence that tests passed.

On refresh, check that every linked path, named section, and listed command still
exists, and flag statements that contradict another source. Propose a rule for a
review finding that recurs across changes. Update stale routing and remove obsolete
setup-owned statements while
preserving user edits and accepted decisions. Ask when a source changed a material
decision; do not silently replace it. A complete existing map may need no changes.
