# Review and remediation rules

Phase reference of the [shared workflow contract](workflow-contract.md).

## Test execution during review

Review analyzes source, diffs, requirements, tests, and existing check evidence.
Run project tests only when the user explicitly requests test execution for this
review. The limit covers focused tests, suites, test-triggering wrappers,
delegated reviewers, and disposable environments; existing test requirements are
not a request. Implementation, verification, and remediation keep their own test
scope. Report tests not run separately. Skipped execution alone does not make a
source review incomplete. A conclusion depends on missing execution evidence →
report the gap rather than run tests unrequested. Required verification and
publication gates still apply.

## Independent review

- Fresh review covers five axes: Standards, Spec, Bugs, Quality, Security.
- Reviewers get requirements, policy, the candidate, and neutral context, never
  the implementer's preferred verdict.
- One fresh reviewer can cover a small change. Add specialists for
  security/privacy, money, schema or migrations, concurrency, public contracts,
  and material architecture changes.
- Self-review is never independent. Required independent review unavailable →
  report the gap.

## Findings

- Validate reachability, expected behavior, impact, and counterevidence.
  Reviewer agreement does not prove a finding, a lone finding still needs
  assessment, and uncertainty is not proof of a false positive. Deduplicate root causes.
- Dispositions: validated, refuted, inconclusive, fixed/verified, or explicitly
  accepted-unresolved.
- Ask before retaining a real unresolved defect or making a material redesign;
  project policy may prohibit acceptance.

## Remediation rounds

At most three autonomous rounds. A round starts with corrective edits and ends at
a verification and re-review verdict or abandonment. Resuming before a verdict
stays in the round; correcting after an unsuccessful verdict starts the next. Keep
the count across resumption, agents, workspaces, and sessions. Stop earlier on
recurrence, no progress, or material conflict, and report incomplete work honestly.
