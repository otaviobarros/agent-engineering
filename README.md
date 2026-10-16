# agent-engineering

Reusable skills for AI-assisted software development. Plan a change for review,
or carry an authorized change through implementation, verification, independent
review, and delivery.

## Skills

| Skill | Purpose |
|---|---|
| `plan-change` | Define scope, acceptance criteria, implementation steps, and verification needs; stop with a plan for review. |
| `deliver-change` | Coordinate implementation and authorized delivery, preserving the limits of the request. |

Both skills use the included shared workflow contract. They provide agent
instructions; the host controls permissions and execution. Explicit limits such
as "do not commit" remain binding throughout the workflow.

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

Install the complete plugin to retain its shared references. Both skills become
available; invoke either one independently. Copying only an individual skill
directory is not supported.

## Usage

> Use plan-change to plan quantity validation. Return the plan for review before
> making changes.

> Use deliver-change to implement the accepted plan. Run the required checks,
> obtain independent review, and leave the changes uncommitted.

## Status

Experimental. Intended for Codex CLI and Claude Code.

Report problems through this repository's issues. Include the host and version,
expected behavior, observed behavior, and a reproducible example with private
information removed.

## License

Original code and documentation are licensed under the MIT License included in
this repository.
