---
name: setup-project
description: Set up or refresh a project's engineering workflow through codebase discovery, a guided interview, documentation proposals, and explicit workflow adoption. Preserve existing project authorities. Use for project onboarding or setup, not application implementation.
---

# Set up project context

Understand the codebase, challenge gaps, and establish useful engineering
documentation. First read the [contract core](../../references/workflow-contract.md).

Setup is optional; installing the plugin neither runs it nor authorizes changes.
Setup discovers code patterns, interviews project owners, and writes accepted
baseline documentation and instruction references, then stops. It starts no
delivery and runs no project tests. Policy migration, implementation, and
publication need separate authority.

## 1. Discover the codebase and its authorities

- Identify the workspace, requested scope, applicable instructions, and permitted
  documentation edits. Preserve unrelated work and scoped instructions. Inspect
  existing guides first and reuse a sufficient authority map; create no second
  owner or guide just for a filename convention.
- **Delegate.** Read the [discovery baseline](references/project-guide.md#discovery),
  then assign discovery to one read-only subagent on an available low-cost model
  suited to file discovery. Honor project model choices and confirm the model
  through host capabilities; never invent model identifiers. Brief it with the
  exact workspace, instructions, access limits, coverage goals, and a concise
  evidence format. Delegates stay in scope and cannot grant permissions or adopt
  practices. No delegation or low-cost model → report it and discover locally;
  never silently switch to a costlier delegate.
- Inventory all major packages and source areas; read representative code,
  tests, boundaries, and configuration in each. Go deeper where evidence conflicts
  or a decision needs it. Exclude generated output, dependencies, secrets, and
  unrelated repositories. On refresh, reuse current evidence and inspect changes.
- You own validation: verify policy sources and the evidence behind material
  observations before using them, reading more files when a report lacks evidence.
  A delegate's summary is not project authority.
- Separate documented policy, observed implementation, and unverified claims. A
  remote URL does not establish tracker, authentication, or permission; reading a
  command does not prove it passes. Inspect setup procedures without running
  bootstrap scripts, installing tools, changing credentials or settings, or
  writing remotely. Keep secrets and personal paths out of the guide.

**Checkpoint 1:** codebase map, existing owners, evidence paths, omissions, and
baseline gaps identified, covering source behavior as well as documents. Report
coverage; never claim every file was read.

## 2. Challenge missing decisions

**Adoption approach.** For initial setup, unless already stated, ask which the user
wants:

- **Preserve and complement existing standards**: map current authorities and
  propose compatible improvements.
- **Adopt our recommended baseline** (recommended): assess every baseline topic,
  draft missing documentation, and propose improvements for explicit acceptance.

Get an explicit choice: the recommendation is not a default, and following
existing authorities selects nothing. Reuse the accepted approach on refresh. A
read-only assessment reports an unset approach and continues. An unanswered choice
stays pending. Neither approach replaces existing authorities or relaxes the
shared contract, and choosing the baseline approves no recommendation or migration.

**Interview.**

1. Show a concise codebase map and the consequential gaps first.
2. Ask one consequential question at a time, decision-tree style: only questions
   whose prerequisites are settled, with answers selecting the next ones. Group
   only independent, closely related choices that save the user effort. Answer
   observable questions from the repository.
3. Ground each proposal in a source observation or a named missing practice, with
   its effect here, reason, alternative, benefit, and adoption cost. Cover small
   interfaces, clear ownership, and real-boundary verification where relevant.
4. Existing code patterns are observations, not standards. Investigate exceptions
   before recommending one pattern across packages.
5. Probe purpose, ownership, scope, exceptions, failure cases, and the evidence
   that would show the decision works; test answers against existing rules and
   counterexamples.
6. Continue until material branches are settled or explicitly pending, not until a
   question count is hit. Keep clear tasks brief. A proposal becomes policy only
   after an explicit answer.

**Documentation decisions.**

- Separate existing requirements, accepted decisions, and proposals. A documented
  choice stays established unless an authority conflicts or the user asks to
  change it; optional improvements neither reopen nor block it.
- Recommend a small standards index with stable rule IDs when rules are hard to
  find. Recommend ADRs for significant tradeoffs whose rationale must last, in the
  project's decision owner and format; one ADR per answer is too many. Keep vocabulary apart
  from requirements.
- Draft factual context from inspected sources within edit authority; mark new
  normative guidance Proposed until accepted. Offer related documentation choices
  as one set the user can accept or amend.
- Compatible shared workflow practices still apply. New requirements, policy
  replacements, and governance artifacts need an authorized adoption decision.
  Keep existing rule IDs; rule, criterion, and test-case IDs differ. Replacing
  standards, renumbering rules, tracker infrastructure, and code migrations are
  separate work.

**Workflow adoption.** Ask separately: agent-engineering as the default workflow for
matching tasks, or skills on demand. Keep an existing explicit choice on refresh; a
baseline choice selects nothing here. Adoption routes matching tasks to installed
skills and keeps phase boundaries and task permissions. Show the proposed routing
and instruction edits before acceptance.

**Checkpoint 2:** material choices accepted or named as pending, with consequences.
Unaffected discovery continues meanwhile.

## 3. Write agreed documentation

- Read the [project-guide format](references/project-guide.md) before creating or
  updating a guide. Prefer the existing owner, else `docs/agent-engineering.md`
  when conventions permit. Omit irrelevant sections.
- Map each topic to its source and reading trigger. Topics: package scope,
  standards, architecture and ADRs, requirements and tracker, tests and test
  identities, commit/PR/stack conventions, and safe environment or worktree
  procedures. Point
  to command catalogs with their working directory instead of copying commands.
- Assess every baseline topic. Reuse owners and write accepted missing content
  within edit authority; a small repository can combine topics. Link actual
  decisions and terms; never fabricate historical ADRs or scaffold empty trees.
  Mark missing sources and open choices.
- Record the approach, workflow choice, and each practice's disposition. Keep code
  changes and policy migrations as separate recommendations. Update setup-owned
  content in place and preserve user edits.
- **Entrypoint pointer**, where authorized and needed: add one short line to the
  existing instruction entrypoint. It says when to read the guide: planning,
  implementation, verification, and review. Prefer the shared entrypoint that host
  imports already reach. Accepted adoption adds the format's concise routing;
  on-demand use adds only needed pointers. Use installed skill names and
  project-relative links, not plugin paths. Keep host imports and scope; create no
  competing host guides.
- Persistence outside authority → return the proposed guide in the response.

**Checkpoint 3:** every baseline topic has a source, accepted documentation, a gap,
or a justified not-applicable disposition, and the workflow choice and entrypoint
edits match the user's acceptance.

## 4. Validate and hand off

1. Resolve local paths and named sections from the actual output location.
2. Read every saved setup document back from disk and check it against its
   sources. Write acknowledgements, cached text, and link or status checks do not
   count. Git's ordinary diff omits new untracked files.
3. Confirm scoped rules and existing IDs are intact. Remove stale claims instead of
   changing sources to fit.
4. Confirm command entries are catalog references with working directories.
5. Inspect the final diff, staged and untracked contents, branch, revision, and
   preserved user work. A timestamp or HEAD alone does not establish contents.

Report the guide or reused entrypoint, sources inspected, accepted decisions,
approach, workflow choice, discovery coverage and limits, proposals, pending
questions, actual checks, and source freshness. A validated context map is not
executable checks, available services, or delivery readiness. Name the references
later tasks will read and the skills the routing selects. Host discovery must
provide those skills; instruction references install and enforce nothing, so
report unavailable skills instead of claiming adoption works. Re-running setup
refreshes pointers and keeps accepted decisions; later phases reopen sources, or
discover normally without a guide.

**Done when** the final text is inspected from disk, each practice's disposition
matches its current authority (including the shared contract), and user work is
preserved. Missing checks → setup incomplete. Stop after the documentation;
commit, push, tracker writes, implementation, and deployment need separate
authority.
