# agent-engineering

Reusable skills for AI-assisted software development. Plan, implement, verify,
review, remediate, or publish a change. Use delivery mode to carry an authorized change
through the workflow.
Optionally map your project's standards and workflow conventions with `setup-project`.

## Skills

| Skill | Purpose |
|---|---|
| `setup-project` | Discover project authorities, discuss adoption choices, and create or refresh a small workflow guide; stop before policy migration or implementation. |
| `plan-change` | Define scope, acceptance criteria, implementation steps, and verification needs; stop with a plan for review. |
| `implement-change` | Implement an accepted plan with code, tests, documentation, and a handoff; stop before independent review or publication. |
| `verify-change` | Check a change against acceptance criteria and report results, freshness, and required gaps; stop before fixes or publication. |
| `review-change` | Review a change against requirements and project rules, validate findings, and report evidence gaps. |
| `review-pr` | Use review-change to assess a GitHub PR, then publish authorized finding threads, a summary, and a justified review decision. |
| `remediate-findings` | Validate findings, correct authorized defects, and obtain verification and fresh independent re-review; stop before publication. |
| `publish-change` | Commit, push, and create a draft PR within authority; verify published state and reconcile interrupted attempts. |
| `deliver-change` | Coordinate implementation and authorized delivery, preserving the limits of the request. |

All skills use the included shared workflow contract. They provide agent
instructions; the host controls permissions and execution. Explicit limits such
as "do not commit" remain binding throughout the workflow.
Publication covers Git and pull requests. Merge, release, and deployment require
separate authorization and workflows.

## Installation

Register the marketplace in your host.

For Codex CLI:

```sh
codex plugin marketplace add otaviobarros/agent-engineering
codex plugin add agent-engineering@agent-engineering
```

For Claude Code:

```sh
claude plugin marketplace add otaviobarros/agent-engineering
claude plugin install agent-engineering@agent-engineering
```

Install the complete plugin to retain its shared references. All nine skills become
available; invoke each independently. Copying only an individual skill
directory is not supported.

## Usage

> Use setup-project to map our project standards and workflow conventions. Ask which
> adoption approach I want, preserve existing authorities, and save a concise guide.

> Use plan-change to plan quantity validation. Return the plan for review before
> making changes.

> Use implement-change to implement the accepted plan with tests and documentation.
> Return the implementation handoff without starting review or publication.

> Use verify-change to verify the current changes against the accepted criteria.
> Report evidence and gaps without changing code or publishing anything.

> Use review-change to review this branch against the accepted requirements.
> Return findings without changing code or publishing comments.

> Use review-pr to review PR #42 and post findings as threads with a summary.
> If the required review is complete and clean, approve it; otherwise report the gaps.
> Preserve the code. If formal approval is unavailable, state that in a comment.

> Use remediate-findings to assess these review findings and fix confirmed defects
> within the accepted scope. Verify and obtain independent re-review; do not commit.

> Use publish-change to commit the verified and reviewed changes, push this branch,
> and create a draft PR. Preserve unrelated work and existing publication limits.

> Use deliver-change to implement the accepted plan. Run the required checks,
> obtain independent review, and leave the changes uncommitted.

## Optional project setup

Setup reuses an existing project guide or, where project conventions permit, creates
`docs/agent-engineering.md`. It links to current standards, decisions, requirements,
checks and collaboration guidance rather than replacing those sources.

Choose to preserve and complement existing standards or adopt the recommended
baseline. The guide separates established requirements, accepted setup choices,
proposals, pending decisions and declined recommendations. Choosing an approach
does not approve every proposal or authorize migration.

When needed and authorized, setup adds a short reference to existing agent instructions
and preserves host imports. It does not automatically create `CONTEXT.md`, ADRs,
rule IDs or a standards system.

Installation does not run setup. Other skills work without a guide or adoption choice
and discover project authorities normally. Setup does not run project procedures,
implement code or publish changes.

## Status

Experimental. Intended for Codex CLI and Claude Code.

Report problems through this repository's issues. Include the host and version,
expected behavior, observed behavior, and a reproducible example with private
information removed.

## License

Original code and documentation are licensed under the MIT License included in
this repository.
