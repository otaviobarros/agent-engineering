# agent-engineering

![Give your coding agent a playbook. Plan clearly. Check the work. Review before you ship.](branding/cover.png)

**From “build this” to a reviewed draft PR.**

Nine skills for **Codex and Claude Code**. Clear plans. Checks you can inspect.
Independent review. Your project's rules.

Use one skill for the next step, or `deliver-change` for the whole workflow.
**You choose the finish line.**

## Install

**Codex CLI**

```sh
codex plugin marketplace add otaviobarros/agent-engineering
codex plugin add agent-engineering@agent-engineering
```

**Claude Code**

```sh
claude plugin marketplace add otaviobarros/agent-engineering
claude plugin install agent-engineering@agent-engineering
```

Install the complete plugin to keep its shared references. All nine skills can
be invoked independently; copying a single skill folder is not supported.

## Teach it how your project works

**Recommended first step: `setup-project`.** Give your agent a map of your
code, standards, architecture, and checks. Turn hidden conventions into clear guidance.
Find gaps before they become repeated mistakes.

> Use setup-project to explore this codebase and interview me about gaps and
> improvements. Propose a documentation baseline and default workflow adoption.
> Write accepted docs and instruction references. Preserve our existing standards.

It uses a low-cost discovery agent when available, checks the findings, and asks
focused questions with recommendations. You choose the practices to adopt and
whether matching tasks should use the plugin workflow by default. Accepted docs
and references in `AGENTS.md` or `CLAUDE.md` carry those choices into later tasks.
Existing authorities still govern; setup runs no project tests or implementation.

Setup is optional and does not run automatically on installation.

## Bring a task. Choose the finish line.

**Take an issue to a draft PR.** Replace `ISSUE_URL` with a link, or describe the
change directly.

> Use deliver-change to implement ISSUE_URL. Follow project standards and ask
> about material decisions. Once required checks and independent review pass,
> commit, push, and open a draft PR linked to the issue. Do not merge or deploy.

Plan → implement → verify → independently review → remediate when needed → publish.
The handoff shows what changed, what was checked, findings, and remaining gaps.

**Want to inspect the work first?** Replace the publication request with:

> Leave everything uncommitted for my review. Do not push or create a PR.

**Think it through before touching code.**

> Use plan-change to plan checkout quantity validation. Define scope, acceptance
> criteria, and checks. Return the plan for review before making changes.

**Put useful feedback where the work happens.**

> Use review-pr to review PR #42 and post prioritized findings as threads with a
> summary. Approve only if the required review is complete, current, and clean.
> If that clean result cannot receive formal approval, leave an explicit approval
> comment with the reason. Preserve the code.

Reviews analyze your changes and existing check evidence. Tests run during review
only when you ask. Full delivery still includes verification.

Issue and task links need access through your host's tools. If access is missing,
provide the task text. A link alone does not select a workflow or authorize
tracker comments, status changes, or task closure.

## Pick the result you need

| Skill | What you get |
|---|---|
| `setup-project` | Codebase discovery, focused questions, and engineering guidance you choose to adopt. |
| `plan-change` | Clear scope, acceptance criteria, and open decisions before code. |
| `implement-change` | Scoped code, tests, and docs from an accepted plan. |
| `verify-change` | What passed, what failed, and what remains unverified. |
| `review-change` | Validated findings with impact and evidence. |
| `review-pr` | Prioritized PR threads, a concise summary, and a justified review decision. |
| `remediate-findings` | Confirmed defects corrected, verified, and independently reviewed again. |
| `publish-change` | Authorized commits, push, and a draft PR, with remote effects verified. |
| `deliver-change` | The full workflow, with your scope and stopping point preserved. |

## Execution and data handling

The plugin contains human-readable skills and shared references. It bundles no
executables, hooks, MCP servers, telemetry, or publisher-operated backend.
The agent host executes tools under its own permissions and your authorized scope.
Skills can guide the agent to read and write project files, run tests and shell
commands, and use Git or connected services. This includes reading your project's
requirements and governing instructions.

Project files, Git metadata, and issue or PR content may contain names, usernames,
commit email addresses, or other personal information. Authorized publishing and
review can send code, commits, PR descriptions, and review comments to GitHub or
your configured Git remote through connectors, APIs, or CLI tools. Project checks
may also contact services configured by your project. Review the project's tools
and configuration before authorizing execution.

The publisher receives no agent activity through the plugin itself. Local files,
host transcripts, and remote records have separate storage and retention rules.
Read the [privacy policy](PRIVACY.md) for details and third-party policy links.

## Help and evaluation

Use a supported Codex or Claude Code installation with access to a model and
your working directory. No separate plugin account or subscription is required.
Tests need your project's runtime and dependencies. Git operations need Git;
GitHub operations need an authenticated host tool and access to the target repository.

Try the examples above in a disposable repository with fictional data. Planning
should return a plan; the no-publication variant should leave changes uncommitted.
If you request report-only review, expect findings without posted comments. Verify
the diff, Git history, and host tool actions against your explicit limits.

- Skills missing: check installation and activation in the current host session.
- Shared references missing: reinstall the complete plugin instead of a copied skill.
- Commands fail: check the working directory, dependencies, and project check command.
- GitHub unavailable: authenticate your own account or provide the task text locally.
- Independent review unavailable: expect an explicit gap, not a completed-review claim.

For directory evaluation, use a disposable repository and your own host account.
The plugin has no service login or shared testing credentials. Arrange any dedicated
account requirement through the submission contact; do not share production access.

Report ordinary problems through [GitHub Issues](https://github.com/otaviobarros/agent-engineering/issues).
For vulnerabilities, use the private channel in [Security](SECURITY.md).

## Your project. Your rules.

Setup is optional. Existing project authorities remain in place. Each standalone
skill stops at its phase boundary. Limits such as “do not commit” persist across
the workflow and resumed work.

These skills guide agents; the host controls permissions and execution. Missing
required checks or independent review leave dependent delivery incomplete.
Merge, release, deployment, and monitoring require separate authorization.

**Experimental.** Results depend on the model, host capabilities, and project.

[Report an issue](https://github.com/otaviobarros/agent-engineering/issues) ·
[Workflow contract](https://github.com/otaviobarros/agent-engineering/blob/main/references/workflow-contract.md) ·
[MIT License](https://github.com/otaviobarros/agent-engineering/blob/main/LICENSE) ·
[Privacy policy](PRIVACY.md)
