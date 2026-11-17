# Publication rules

Phase reference of the [shared workflow contract](workflow-contract.md).

- **Each external write.** Before it, confirm scope, exact candidate, current
  evidence, destination, and actual permissions. Inspect staged content; keep
  commits coherent with their tests and docs. After it, read back the remote
  effect; command success alone proves nothing.
- **Uncertain outcome.** After an interrupted or uncertain write, inspect actual
  state before another effect-producing attempt. A matching observed effect
  satisfies that operation only. An absent effect does not show the earlier
  attempt cannot still execute: retry only after establishing that, within
  current authority. Otherwise stop retries and report what must be resolved. A
  new agent, session, or renewed permission does not reset this.
- **Pull requests.** New PRs are drafts. Mark ready only with readiness authority,
  when required checks and independent review pass at the current revision.
  Before resolving authorized threads, re-review the current head and
  independently verify fixes. Review-only work preserves application code; publish
  comments or formal approval only within actual authorization.
