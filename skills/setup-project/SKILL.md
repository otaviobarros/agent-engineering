---
name: setup-project
description: Discover or refresh a project's workflow context and guide. Map existing standards, decisions, checks, and collaboration conventions; question material gaps and propose improvements without replacing project authorities. Use for project onboarding or setup requests, not application implementation.
---

# Set up project context

Make the project's engineering practices discoverable to people and phase skills.
Read the [shared workflow contract](../../references/workflow-contract.md).
Setup is optional; installing the plugin does not run it or authorize project changes.

## 1. Establish scope and inspect existing authorities

Identify the actual repository/workspace, requested scope, applicable instructions,
and permitted documentation edits. Preserve unrelated work and scoped instructions.
Inspect existing guides before selecting an output. Reuse a sufficient authority map;
avoid creating a second owner or a guide solely to satisfy a filename convention.

Read relevant instruction entrypoints, documentation indexes, standards and rule IDs,
architecture decisions, domain vocabulary, manifests, executable check configuration,
and collaboration/environment guidance. Follow scoped references for affected packages.
Inspect vocabulary candidates such as `GLOSSARY.md` and `CONTEXT.md` before reporting missing ownership.
Use repository-relative locations; scope discovery rather than scanning all source files.
Record where to read current versions and commands instead of copying their values.

Distinguish documented policy from observed implementation and unverified claims.
A remote URL does not establish tracker choice, authentication, or permission.
Reading a command does not prove it passes. Inspect setup procedures without running
bootstrap scripts, installing tools, changing credentials/settings, or writing remotely.
Those operations need their own authority. Keep secrets and personal paths out of the guide.

Done when existing owners, scoped sources, and material gaps are identified.

## 2. Challenge missing decisions

For initial setup, ask which adoption approach the user wants unless already stated:

- **Preserve and complement existing standards** (recommended): map current authorities
  and propose compatible improvements.
- **Adopt our recommended baseline**: propose practices for missing areas and identify
  differences that need an explicit adoption decision.

Reuse the accepted approach on refresh. For a read-only assessment, report an unset
approach without blocking the assessment. An unanswered choice remains pending.
Neither approach replaces existing authorities or relaxes the shared contract.
Following existing authorities does not select an approach. Obtain an explicit
choice; the recommendation is not a default selection.
Selecting the baseline does not approve every recommendation or authorize migration.

Answer observable questions from the repository. For unresolved intent or conflicting
authorities, interview the user before dependent decisions. Ask one consequential
question at a time, with concrete alternatives, tradeoffs, and a recommendation.
Wait for the answer; do not turn a recommendation or silence into an accepted policy.

Probe the decision's purpose, ownership, scope, exceptions, failure cases, and what
evidence would show it works. Resolve prerequisite choices before dependent ones.
Check each answer against existing rules and practical counterexamples. Continue
until material branches are settled or explicitly pending; do not end the interview
merely because a fixed question count was reached. Keep clear tasks brief.

Separate existing requirements, accepted decisions, and proposed improvements.
Treat a documented choice as established unless an applicable authority conflicts
or the user requests a change. Optional improvements do not reopen that choice
or block work governed by it.
Recommend a small standards index with stable rule IDs when rules are hard to find.
Recommend ADRs for significant tradeoffs whose rationale must survive later work;
reuse the project's decision owner and format. Do not create an ADR for every answer.
Keep domain vocabulary separate from requirements. Favor clear module ownership,
small caller-facing interfaces, and verification through real boundaries.

Compatible shared workflow practices still apply. New project requirements,
policy replacements, or governance artifacts need an authorized adoption decision.
Preserve existing rule IDs; rule, acceptance-criterion, and test-case IDs differ.
Setup does not rewrite standards, renumber rules, or create a tracker or ADR system.

Done when material choices are accepted or named as pending, with their consequences.
Continue unaffected discovery while a decision is pending.

## 3. Save the smallest useful guide

Read the [project-guide format](references/project-guide.md) when creating or updating
a guide. Prefer the existing owner. Otherwise use `docs/agent-engineering.md` when
the project's documentation conventions permit it. Omit irrelevant sections.

Map topics to authoritative sources and reading triggers, including package scope,
standards, architecture/ADRs, requirements/tracker, tests and test identities,
commit/PR/stack conventions, and safe environment/worktree procedures where applicable.
Point to command catalogs with their working directory rather than a second command list.
Mark missing sources and unresolved choices explicitly; proposals are not active rules.
Record the selected adoption approach, its scope, and each practice's disposition
using the project-guide format. Keep policy migrations as separately scoped proposals.

Update existing setup-owned content in place and preserve user edits. Add one short
pointer from the existing instruction entrypoint only where authorized and needed.
The pointer names when to read the guide during planning, implementation, verification,
and review. Prefer the shared entrypoint when host imports already reach it.
Preserve host imports and instruction scope; do not create competing host guides.
If persistence is outside authority, return the proposed guide in the response.

Done when the map is useful and discoverable without duplicated policy or unrelated edits.

## 4. Validate and hand off

Resolve local source paths and named sections from the actual output location.
After saving, read the complete guide from disk and inspect that tool output
against its sources. Write acknowledgements, cached text, and link/status checks
do not complete this inspection.
Git's ordinary diff omits new untracked files.
Confirm scoped rules and existing IDs remain intact. Remove stale claims without
changing sources to fit the guide.
Check that command entries give catalog references and working directories, not copied invocations.
Inspect the final diff and relevant staged/untracked contents, branch/revision,
and preserved user work. A timestamp or HEAD alone does not establish current contents.

Report the guide or reused entrypoint, inspected sources, accepted decisions,
adoption approach, proposals, pending questions, actual checks, and source freshness. Distinguish a
validated context map from executable checks, available services, or delivery readiness.
Re-running setup refreshes changed pointers and preserves accepted project decisions.
Later phases reopen applicable sources; without a guide they use normal discovery.

Done when the complete final text is inspected, each practice's disposition matches
its current authority (including the shared contract), and user work is preserved.
For saved guides, inspect the contents returned from disk. Report missing checks as
incomplete setup.
Stop after setup. Commit, push, tracker writes, implementation, and deployment require
separate authority under the shared contract.
