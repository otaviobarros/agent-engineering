# Project-guide format

Use this format only when a project needs a new context map or its existing guide
benefits from these fields. Preserve the existing document's name, structure, and owner
where sufficient. This is human-readable Markdown, not executable configuration.

## What the guide owns

The guide owns pointers, applicability, and setup decisions whose owner is not
already elsewhere. Refer to existing policies rather than copying them. Applicable
project instructions and the host's instruction hierarchy still govern. This guide
does not grant permissions or replace standards, accepted ADRs, or task requirements.

Use a short scope statement and a source table. Each row answers: what concern,
when it applies, and which repository-relative file/section owns it. For a monorepo,
include the package scope and its instruction entrypoint; root rules do not erase
applicable local rules. Relative links resolve from the guide's directory, not repo root.

Include only useful topics:

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

Record the selected approach: **Preserve and complement existing standards** or
**Adopt our recommended baseline**. Reuse an existing accepted selection; an unanswered
choice stays pending. Neither approach overrides current authorities or permits migration.
Attribute the selection to an explicit user choice or an existing accepted record,
not an inference from the requirement to respect project authorities.

Use a short table for relevant practices: practice, disposition, source or decision
reference, scope and rationale. Mark each practice as:

- **Established**: governed by an existing source; link to that owner.
- **Accepted**: an explicitly adopted setup choice without another owner; record why.
- **Proposed**: an optional improvement awaiting adoption; it does not block existing work.
- **Pending**: a material unresolved choice; name only the dependent work it blocks.
- **Declined**: a recommendation the user rejected; retain it to avoid proposing it again.

Practices required by applicable authorities, including the shared workflow contract,
are Established. A missing mechanism can be Proposed without making its governing
requirement optional. New practices need their own adoption decision.

Link externally owned decisions rather than copying them. An approach selection is
not blanket acceptance of practices. Preserve accepted choices and user-authored notes.
Replacements of existing policy remain proposals for a separately scoped change.

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

| Practice | Disposition | Source or decision | Scope and rationale |
|---|---|---|---|
| Engineering rules | Established | [Standards index](engineering.md) | Applicable paths; preserve existing IDs |
| Standards navigation | Proposed | No adoption decision | Add reading triggers if rules become hard to find; no work blocked |

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

Each phase follows applicable pointers and reads current sources before relying on
them. A missing source or conflicting claim leaves that topic unresolved; keep
unaffected work moving. The map's existence is not evidence that tests passed.

On refresh, update stale routing and remove obsolete setup-owned statements while
preserving user edits and accepted decisions. Ask when a source changed a material
decision; do not silently replace it. A complete existing map may need no changes.
