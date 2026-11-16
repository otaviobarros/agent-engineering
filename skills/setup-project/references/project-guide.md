# Project-guide format

Use this format only when a project needs a new context map or its existing guide
benefits from these fields. Preserve the existing document's name, structure, and owner
where sufficient.

## Discovery

Start with instruction entrypoints, the directory inventory, manifests, and documentation
indexes. Include hidden configuration directories such as `.github/` in the inventory,
because some file-listing tools skip them. The discovery agent inventories every major package and source area and reads
representative source, tests, boundaries, and configuration in each:

- Entrypoints, package dependencies, module boundaries, and caller-facing interfaces.
- Domain models, persistence, external integrations, UI flows, and trust boundaries where present.
- Recurring error handling, validation, naming, and test patterns, including exceptions.
- Standards and rule IDs, ADRs, vocabulary such as `GLOSSARY.md` or `CONTEXT.md`,
  check configuration, CI, and collaboration/environment guidance.

Exclude generated output, dependencies, secrets, and unrelated repositories.
Return a compact map: area, representative paths, observed pattern, documented authority,
confidence or unresolved question. Add coverage, excluded areas, and specific documentation
gaps or improvement candidates with evidence. Read-only discovery inspects commands;
it does not run project tests, bootstrap scripts, or remote operations.

The user's request and project instructions and standards govern, under the host's
instruction hierarchy. As evidence of what is enforced, weigh tool configuration and CI
(linters, formatters, type checks, workflows) first, then ADRs and docs, then the
dominant code pattern as observation only. Report conflicts with confidence and
counterexample paths. Never resolve them by choosing the implementation or a tool
configuration as policy. The setup owner checks material evidence and owns the
recommendations and interview.

## Documentation baseline

Assess every row. Filenames below are examples, not required scaffolding or
prerequisites for invoking other skills. Reuse existing owners. Cover small projects in fewer documents and apply package scopes
in monorepos. Mark a missing topic as a gap, or not applicable with a reason.

| Topic | Useful documented outcome | Recommendation when missing |
|---|---|---|
| Purpose and architecture | Product purpose, important constraints, and a navigation map: each area's entry files, owner, and non-obvious rules | Draft the map from inspected code, linking files instead of narrating modules; confirm uncertain intent |
| Engineering standards | Index of applicable rules with task/path triggers and exceptions | Propose a small index; stable IDs for rules that need references, preserving existing IDs |
| Verification | Check catalogs, working directories, important behavior, test naming or ID conventions, and real-interface procedures | Link executable configuration; propose missing procedures without implementing a harness |
| Work and collaboration | Requirements owner, tracker or local alternative, commit/branch/PR conventions | Ask unresolved choices; a hosted tracker and stacked PRs are optional |
| Environment | Setup/configuration sources, safe local isolation, worktree/remote guidance when relevant, and cleanup | Document observed procedures; flag unverified commands and unresolved environment ownership |
| Decisions and vocabulary | Where significant decisions and domain terms are recorded and when to read them | Propose an ADR/glossary convention; add real accepted content when justified |
| Workflow selection | On-demand use or accepted default routing, including task limits | Ask explicitly; retain phase boundaries and publication permissions |

### Proposals

- Separate existing requirements, accepted decisions, and proposals. A documented
  choice stays established unless an authority conflicts or the user asks to change
  it; optional improvements neither reopen nor block it.
- Existing code patterns are observations, not standards. Document them with
  evidence and investigate exceptions before proposing one pattern across packages
  as a standard. Recording current architecture does not silently make it a
  permanent requirement.
- Recommend a standards index when rules are hard to find. Keep existing rule IDs;
  rule, acceptance-criterion, and test-case IDs remain separate.
- Recommend ADRs for significant tradeoffs whose rationale must last, in the
  project's decision owner and format; one ADR per answer is too many. Keep
  vocabulary apart from requirements.
- Draft factual context from inspected sources within edit authority; mark new
  normative guidance Proposed until accepted. Offer related documentation choices
  as one set the user can accept or amend.
- New requirements, policy replacements, and governance artifacts need an
  authorized adoption decision. Replacing standards, renumbering rules, tracker
  infrastructure, and code migrations are separate work.

## What the guide owns

The guide owns pointers, applicability, and setup decisions whose owner is not
already elsewhere. It does not replace standards, accepted ADRs, or task
requirements. Refer to existing policies and decisions rather than copying them.

Use a short scope statement and a source table. Each row answers: what concern,
when it applies, and which repository-relative file/section owns it. For a monorepo,
include the package scope and its instruction entrypoint; root rules do not erase
applicable local rules. Put rules that apply to one area in that area's instruction
file or a path-scoped rule file the host supports, not in the root entry. Relative
links resolve from the guide's directory, not repo root.

Write each line for something an agent cannot learn quickly from the code:
conventions, non-standard practices, commands, owners, and where to look. Link files
instead of describing them. Keep the always-loaded entry short and put detail behind
links read on demand.

Link each baseline topic to its existing owner where available. Include original
stable rule IDs with their task/path triggers, manifests and lockfiles, command/test
catalogs, any adopted test-ID check, and dependent-stack conventions. Point to
tracker conventions; resolve live issue state at task time.

List the commands an agent cannot guess, such as running one test, lint, typecheck,
and build, with their working directory and source file. Mark commands not taken
from configuration or CI as unverified. Link full catalogs instead of copying them.

Preserve privacy: no secrets, credential-bearing URLs, customer data, personal absolute
paths, raw logs, copied environment values, or cached authentication claims.
Record source absence as unknown or not established, not as permission to invent rules.

## Adoption record

Record the selected documentation approach: **Preserve and complement existing standards**
or **Adopt our recommended baseline**. Also record workflow selection separately:
**On demand** or **Default for matching tasks**. Attribute each selection to an explicit
user choice or an existing accepted record, not an inference from the requirement to
respect project authorities.

Use a short table for relevant practices: practice, disposition, source or decision
reference, enforcement (lint rule, CI check, hook, CODEOWNERS, or prose only), scope
and rationale. Prefer a tool for a rule that must always hold; propose the mechanism
as separate work, since setup installs nothing. Mark each practice as:

- **Established**: governed by an existing source; link to that owner.
- **Accepted**: an explicitly adopted setup choice without another owner; record why.
- **Proposed**: an optional improvement awaiting adoption; it does not block existing work.
- **Pending**: a material unresolved choice; name only the dependent work it blocks.
- **Declined**: a recommendation the user rejected; retain it to avoid proposing it again.

Practices required by applicable authorities, including the shared workflow contract,
are Established. A missing mechanism can be Proposed without making its governing
requirement optional; put the requirement and the mechanism in different rows. For
example, a test-ID convention that project instructions require is Established even
when its uniqueness check is Proposed.

Each Disposition cell holds exactly one of these five words, with no qualifier.
Put an explanation, such as the covering source or a replaced proposal, in the
rationale column. Record documentation coverage gaps and not-applicable topics in
a separate coverage section, outside the practices table. When a source now settles
a Proposed or Pending practice, change that row's disposition and name the source.

Settle test IDs from discovery:

- A test-ID or test-naming convention set by project instructions, check
  configuration, or a recorded adoption decision → record it as Established, with
  its source and any uniqueness check.
- A pattern seen only in test code → record it as an observation with evidence, and
  propose its adoption. It governs verification only after an explicit answer.
- No pattern → list **behavior-slug test IDs** as Proposed. Benefit: traceability
  across renames and for external QA or compliance tracking. Cost: a uniqueness check
  to maintain.
- Raise the proposal in the interview only on a signal: external test tracking,
  compliance requirements, or a large E2E suite.

## Workflow adoption

For accepted default routing, show the project owner a concise instruction block before
writing it to the applicable `AGENTS.md` or `CLAUDE.md`. Adapt the following intent map
to installed skills; the user's requested outcome and limits select the scope. Routing
keeps phase boundaries and task permissions.

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

Keep the always-loaded instruction short, for example:

> For development tasks, use the installed agent-engineering skill matching the requested
> outcome. Use `deliver-change` for full implementation; use the relevant phase skill
> for narrower requests. Read the project workflow guide for routing and
> applicable standards. Explicit task limits and project authorities govern. Report a
> missing skill; do not treat this reference as permission to install or publish.

Keep the routing table in the guide or an existing owner instead of copying it into
every host instruction. On-demand selection adds no default-routing instructions.
Existing independently accepted workflow rules still apply until their owner
authorizes a change.

Skill selection does not authorize tests during review, external PR comments, commits,
push, approval, merge, or deployment beyond the user's task authority. A PR link alone
does not request a review or publication. Default routing remains agent-followed guidance;
do not add hooks, a persistent mode, or an orchestrator as part of setup.

## Entrypoint pointer

If no existing entrypoint points to the guide, add one short line to the existing
instruction entrypoint within edit authority. State when the guide applies, for
example: “For planning, implementation, verification, and review, read the project
workflow guide.” Use the actual project-relative link and installed skill names, not
plugin paths. Accepted default routing adds the instruction block above; on-demand use
adds only needed pointers.

- Prefer the shared entrypoint that host imports already reach. When `CLAUDE.md`
  imports `AGENTS.md`, one pointer in `AGENTS.md` is sufficient. With independent
  entrypoints, add pointers only where needed and authorized.
- If the guide is itself the instruction entrypoint, a second pointer is unnecessary.
- Keep host imports and scope. Create no competing host guides, do not copy the
  whole guide into host files, and create no import loop when the map links back to
  those instructions.

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
```

## Refresh

Re-running setup refreshes pointers and keeps accepted decisions. Check that every
linked path, named section, and listed command still exists, and flag statements that
contradict another source. Propose a rule for a review finding that recurs across
changes. Update stale routing and remove obsolete setup-owned statements while
preserving user edits, user-authored notes, and accepted decisions. Edit the
existing guide in place. Ask when a source changed a material decision; do not
silently replace it. A complete existing map may need no changes.
