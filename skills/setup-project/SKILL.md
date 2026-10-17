---
name: setup-project
description: Set up or refresh a project's engineering workflow through codebase discovery, a guided interview, documentation proposals, and explicit workflow adoption. Preserve existing project authorities. Use for project onboarding or setup, not application implementation.
---

# Set up project context

Understand the codebase, challenge gaps, and establish useful engineering documentation.
Read the [shared workflow contract](../../references/workflow-contract.md).
Setup is optional; installing the plugin does not run it or authorize project changes.

## 1. Discover the codebase and its authorities

Identify the actual repository/workspace, requested scope, applicable instructions,
and permitted documentation edits. Preserve unrelated work and scoped instructions.
Inspect existing guides before selecting an output. Reuse a sufficient authority map;
avoid creating a second owner or a guide solely to satisfy a filename convention.

Read the [discovery and documentation baseline](references/project-guide.md#discovery)
before assigning discovery. Use one read-only subagent with an available low-cost
model suited to file discovery. Honor project model choices and confirm the model
through host capabilities; do not invent model identifiers. Give it the exact workspace,
applicable instructions, access limits, coverage goals, and a concise evidence format.
Keep delegates within the same scope; they cannot grant permissions or adopt practices.

Inventory all major packages and source areas, then read representative implementations,
tests, boundaries, and configuration in each. Deepen discovery where evidence conflicts
or a proposed decision needs it. Exclude generated output, dependencies, secrets, and
unrelated repositories. Report coverage and omissions rather than claiming every file
was read. On refresh, reuse current evidence and inspect changed areas.

If delegation or a suitable low-cost model is unavailable, report that limitation.
Continue discovery locally within scope; do not silently choose a costlier delegate.
The setup owner validates policy sources and checks evidence supporting material
observations before using them in questions or documentation. Read additional files
when the report lacks evidence. A delegate's summary is not project authority.

Distinguish documented policy from observed implementation and unverified claims.
A remote URL does not establish tracker choice, authentication, or permission.
Reading a command does not prove it passes. Inspect setup procedures without running
bootstrap scripts, installing tools, changing credentials/settings, or writing remotely.
Those operations need their own authority. Keep secrets and personal paths out of the guide.

Done when the codebase map, existing owners, evidence paths, omissions, and baseline
gaps are identified. Discovery covers source behavior as well as existing documents.

## 2. Challenge missing decisions

For initial setup, ask which adoption approach the user wants unless already stated:

- **Preserve and complement existing standards**: map current authorities and propose
  compatible improvements.
- **Adopt our recommended baseline** (recommended): assess every baseline topic,
  draft missing documentation, and propose improvements for explicit acceptance.

Reuse the accepted approach on refresh. For a read-only assessment, report an unset
approach without blocking the assessment. An unanswered choice remains pending.
Neither approach replaces existing authorities or relaxes the shared contract.
Following existing authorities does not select an approach. Obtain an explicit
choice; the recommendation is not a default selection.
Selecting the baseline does not approve every recommendation or authorize migration.

Show a concise codebase map and the consequential gaps first. Use a decision tree
for the interview: ask questions whose prerequisites are settled, then use the answers
to identify the next questions. Ask one consequential question at a time; group only
independent, closely related choices when that reduces effort for the user.
Answer observable questions from the repository instead of asking the user to discover facts.

Ground each proposal in a source observation or a named missing practice. Explain the
effect on this codebase, the reason for the recommendation, and a practical alternative.
Ask about ambiguous intent, conflicting authorities, and worthwhile improvements,
including alignment with small interfaces, clear ownership, and real-boundary verification.
State the benefit and adoption cost. Existing code patterns are observations, not
automatically standards to enforce. Investigate apparent exceptions before recommending
one pattern across packages. Wait for an explicit answer before treating a proposal as policy.

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
Keep domain vocabulary separate from requirements. Draft factual context from inspected
sources within edit authority; keep new normative guidance marked Proposed until accepted.
Offer related documentation choices as a concrete set the user can accept or amend.

Compatible shared workflow practices still apply. New project requirements,
policy replacements, or governance artifacts need an authorized adoption decision.
Preserve existing rule IDs; rule, acceptance-criterion, and test-case IDs differ.
Setup may create accepted baseline documentation. Replacing existing standards,
renumbering rules, creating tracker infrastructure, and code migrations remain separate work.

Ask separately whether the project should use agent-engineering as its default workflow
for matching development tasks or keep skill selection on demand. Preserve an existing
explicit workflow choice on refresh. A baseline choice alone does not select workflow
adoption. Show the proposed task-to-skill routing and instruction edits before acceptance.

Done when material choices are accepted or named as pending, with their consequences.
Continue unaffected discovery while a decision is pending.

## 3. Write agreed documentation and workflow references

Read the [project-guide format](references/project-guide.md) when creating or updating
a guide. Prefer the existing owner. Otherwise use `docs/agent-engineering.md` when
the project's documentation conventions permit it. Omit irrelevant sections.

Map topics to authoritative sources and reading triggers, including package scope,
standards, architecture/ADRs, requirements/tracker, tests and test identities,
commit/PR/stack conventions, and safe environment/worktree procedures where applicable.
Point to command catalogs with their working directory rather than a second command list.
Mark missing sources and unresolved choices explicitly; proposals are not active rules.
Assess every documentation baseline topic using the project-guide format. Reuse existing
owners and write accepted missing content within documentation edit authority. A small
repository can cover several topics in one document. Link actual decisions and domain terms;
do not fabricate historical ADRs or scaffold empty documentation trees.
Record the adoption approach, workflow choice, and each practice's disposition.
Keep proposed code changes and policy migrations as separately scoped recommendations.

Update existing setup-owned content in place and preserve user edits. Add one short
pointer from the existing instruction entrypoint only where authorized and needed.
The pointer names when to read the guide during planning, implementation, verification,
and review. Prefer the shared entrypoint when host imports already reach it.
For accepted workflow adoption, add the format's concise task-to-skill routing to the
appropriate instruction entrypoint. For on-demand use, add only needed context pointers.
Use installed skill names and project-relative references, not machine-specific plugin paths.
Preserve host imports and instruction scope; do not create competing host guides.
If persistence is outside authority, return the proposed guide in the response.

Done when each baseline topic has an authoritative source, accepted documentation, an
explicit gap, or a justified not-applicable disposition. The workflow choice and any
authorized entrypoint edits match the user's acceptance.

## 4. Validate and hand off

Resolve local source paths and named sections from the actual output location.
After saving, read all changed setup documents from disk and inspect that tool output
against its sources. Write acknowledgements, cached text, and link/status checks
do not complete this inspection.
Git's ordinary diff omits new untracked files.
Confirm scoped rules and existing IDs remain intact. Remove stale claims without
changing sources to fit the guide.
Check that command entries give catalog references and working directories, not copied invocations.
Inspect the final diff and relevant staged/untracked contents, branch/revision,
and preserved user work. A timestamp or HEAD alone does not establish current contents.

Report the guide or reused entrypoint, inspected sources, accepted decisions,
adoption approach, workflow choice, discovery coverage and limits, proposals, pending
questions, actual checks, and source freshness. Distinguish a
validated context map from executable checks, available services, or delivery readiness.
Re-running setup refreshes changed pointers and preserves accepted project decisions.
Later phases reopen applicable sources; without a guide they use normal discovery.

Done when the complete final text is inspected, each practice's disposition matches
its current authority (including the shared contract), and user work is preserved.
For saved guides, inspect the contents returned from disk. Report missing checks as
incomplete setup.
Explain which references later tasks will read and which skills the accepted routing
selects. Host discovery must make those skills available; instruction references do not
install skills or mechanically enforce invocation. Report unavailable skills instead of
claiming adoption is operational. Setup does not start delivery or execute project tests.
Stop after setup documentation. Commit, push, tracker writes, implementation, and deployment require
separate authority under the shared contract.
