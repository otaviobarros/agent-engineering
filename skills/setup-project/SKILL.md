---
name: setup-project
description: Set up or refresh a project's engineering workflow through codebase discovery, a guided interview, documentation proposals, and explicit workflow adoption. Preserve existing project authorities. Use for project onboarding or setup, not application implementation.
---

# Set up project context

Understand the codebase, challenge gaps, and establish useful engineering
documentation. First read the [contract core](references/workflow-contract.md).

Setup is optional; installing the plugin neither runs it nor authorizes changes.
Setup discovers code patterns, interviews project owners, and writes accepted
baseline documentation and instruction references, then stops. It starts no
delivery. It runs no project tests, linters, or checks at any step; it reads
them instead. Policy migration, implementation, and publication need separate
authority.

## 1. Discover the codebase and its authorities

- Identify the workspace, requested scope, applicable instructions, and permitted
  documentation edits. Preserve unrelated work and scoped instructions. Inspect
  existing guides first and reuse a sufficient authority map; create no second
  owner or guide just for a filename convention.
- **Delegate.** Read the [discovery baseline](references/project-guide.md#discovery).
  Then dispatch discovery to one read-only subagent on an available low-cost model
  suited to file discovery, before you read project source yourself. Delegate for
  every repository size, on initial setup and on refresh. Honor project model
  choices and confirm the model through host capabilities; never invent model
  identifiers. Brief it with the exact workspace, instructions, access limits,
  coverage goals, and a concise evidence format. Delegates stay in scope and cannot
  grant permissions or adopt practices. The delegate's report is this step's input.
  No subagent mechanism or low-cost model → report it and discover locally; never
  silently switch to a costlier delegate.
- Cover every major package and source area as the baseline describes. Go deeper
  where evidence conflicts or a decision needs it. On refresh, brief the delegate
  with the existing guide and the changes since it, and follow
  [refresh](references/project-guide.md#refresh).
- You own validation: verify policy sources and the evidence behind material
  observations before using them, reading more files when a report lacks evidence.
  A delegate's summary is not project authority. The baseline's authority order
  and conflict rule bind your conclusions too.
- Separate documented policy, observed implementation, and unverified claims. A
  remote URL does not establish tracker, authentication, or permission; reading a
  command does not prove it passes. Read commands and check configuration, such as
  a Makefile or CI workflow, without running them. Inspect setup procedures without
  running bootstrap scripts, installing tools, changing credentials or settings, or
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
   only independent, closely related choices that save the user effort.
3. Ground each proposal in a source observation or a named missing practice, with
   its effect here, reason, alternative, benefit, and adoption cost. Cover small
   interfaces, clear ownership, and real-boundary verification where relevant.
   Apply the [proposal rules](references/project-guide.md#proposals).
4. Probe purpose, ownership, scope, exceptions, failure cases, and the evidence
   that would show the decision works; test answers against existing rules and
   counterexamples.
5. Continue until material branches are settled or explicitly pending, not until a
   question count is hit. Keep clear tasks brief. A proposal becomes policy only
   after an explicit answer.

**Workflow adoption.** Ask separately: agent-engineering as the default workflow for
matching tasks, or skills on demand. Keep an existing explicit choice on refresh; a
baseline choice selects nothing here. Show the proposed routing and instruction
edits from [workflow adoption](references/project-guide.md#workflow-adoption)
before acceptance.

**Checkpoint 2:** material choices accepted or named as pending, with consequences.

## 3. Write agreed documentation

- Before creating or updating a guide, read the
  [project-guide format](references/project-guide.md) and write by it. Prefer the
  existing owner, else `docs/agent-engineering.md` when conventions permit. Omit
  irrelevant sections.
- Assess every baseline topic and map it to its source and reading trigger. Reuse
  owners and write accepted missing content within edit authority; a small
  repository can combine topics. Link actual decisions and terms; never fabricate
  historical ADRs or scaffold empty trees. Mark missing sources and open choices.
- Record the approach, workflow choice, and each practice's disposition and
  enforcement in the [adoption record](references/project-guide.md#adoption-record).
  Each Disposition cell holds exactly one of its five values; put explanations in
  another column. Keep code changes and policy migrations as separate
  recommendations.
- On an existing guide, edit setup-owned lines in place instead of rewriting the
  file. Keep user-authored text, such as a person's note, word for word in its
  original section, even when you restructure nearby setup-owned content.
- Add the [entrypoint pointer](references/project-guide.md#entrypoint-pointer)
  where authorized and needed.
- Persistence outside authority → return the proposed guide in the response.

**Checkpoint 3:** every baseline topic has a source, accepted documentation, a gap,
or a justified not-applicable disposition, and the workflow choice and entrypoint
edits match the user's acceptance.

## 4. Validate and hand off

1. Resolve local paths and named sections from the actual output location.
2. Read every saved setup document back from disk and check it against its
   sources. Write acknowledgements, cached text, and link or status checks do not
   count. Git's ordinary diff omits new untracked files.
3. Confirm scoped rules, existing IDs, and user-authored text are intact. Remove
   stale claims instead of changing sources to fit.
4. Confirm each listed command names its working directory and source file, and
   that every linked path and section exists. Confirm a command by reading its
   source. Run no listed command, test suite, linter, or project check such as
   `make check`. When applicable project instructions require a check before
   hand-off and no authority exempts setup, keep the check unrun. Report it as a
   required check that was not run, and report the hand-off as incomplete for that
   requirement.
5. Confirm the host instruction or import chain reaches the guide without loops.
   Check each referenced skill through host discovery; for an unavailable skill,
   keep the accepted choice, report activation as unverified, and install nothing.
6. Inspect the final diff, staged and untracked contents, branch, revision, and
   preserved user work. A timestamp or HEAD alone does not establish contents.

Report the guide or reused entrypoint, sources inspected, accepted decisions,
approach, workflow choice, discovery coverage and limits, proposals, pending
questions, the document checks you performed, and source freshness. Name the
project checks that were not run, including any that project instructions require
before hand-off. A validated context map is not executable checks, available
services, or delivery readiness. Name the references
later tasks will read and the skills the routing selects. Instruction references
install and enforce nothing; report unavailable skills instead of claiming
adoption works.

**Done when** the final text is inspected from disk, each practice's disposition
matches its current authority (including the shared contract), and user work is
preserved. Missing document checks → setup incomplete. A required project check
that was not run → hand-off incomplete for that requirement. Stop after the
documentation; commit, push, tracker writes, implementation, and deployment need
separate authority.
