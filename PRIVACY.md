# Privacy policy

Effective date: October 17, 2026

agent-engineering provides instructions for coding agents in Codex and Claude Code.
The plugin has no telemetry, analytics, hosted backend, or bundled MCP servers.
The publisher does not collect or receive your prompts, source code, credentials,
or agent activity through the plugin itself.

Your agent host processes the instructions and the context you give it under its
own terms, privacy policy, and settings. The skills can guide the agent to read
project files, run tools, and interact with connected services within your
authorized scope. Those actions may store data locally or send it to services
such as GitHub. Each service's privacy policy and your configuration govern that
processing. This policy does not replace those policies.

## Data and retention

Project files, Git history, and issue or PR content may include names, usernames,
commit email addresses, or other personal information. Depending on your request,
the agent may read that information and write it into local artifacts or remote
records. Authorized Git pushes, PR creation, and review publication may send code,
Git metadata, descriptions, and comments to GitHub or your configured Git remote.
Project commands may contact additional services configured by your project.

The plugin has no publisher-controlled store of agent-session data and no
publisher-defined retention period for it. Local artifacts remain until you or
your tooling change or delete them. Agent transcripts follow the host's settings
and policies. Remote commits, PRs, and reviews follow the destination service's
retention and deletion rules. Disabling the plugin does not remove those records.

Consult the policies applicable to your host, account, and deployment:

- [Anthropic privacy policy](https://www.anthropic.com/legal/privacy)
- [OpenAI privacy policy](https://openai.com/policies/privacy-policy/)
- [GitHub privacy statement](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement)

For other Git hosts or project services, review their policies before authorizing
operations. Avoid providing secrets or personal information that the task does
not need.

## Support and security reports

If you open a [GitHub issue](https://github.com/otaviobarros/agent-engineering/issues),
the publisher can read the information you submit. Issues in this repository are
public. Share only the information needed to explain the problem; remove secrets,
personal information, and private project content. GitHub governs the storage and
handling of those reports under its
[privacy statement](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement).

For security concerns, use the private reporting channel in [Security](SECURITY.md).
Information you submit there is available to the maintainers and GitHub under
GitHub's advisory access and retention rules. It may be used to investigate and
coordinate a fix. Public disclosure should be coordinated with the maintainers.

For questions about this policy, open an issue without including sensitive data.
Updates to this policy will be published here with a revised effective date.
