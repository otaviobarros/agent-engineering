# Review and remediation rules

Phase reference of the [shared workflow contract](workflow-contract.md).

## Test execution during review

Run project tests only when the user explicitly requests test execution for this
review. The limit covers suites, test-triggering wrappers, delegated reviewers,
and disposable environments. Existing test requirements are not a request.
Report tests not run. A conclusion that depends on missing execution evidence →
report the gap. Skipped execution alone does not make a source review incomplete.
Implementation, verification, and remediation keep their own test
scope.

## Independence

Reviewers get requirements, policy, the candidate, and neutral context, never the
implementer's preferred verdict. Self-review is never independent. Required
independent review unavailable → report the gap.

## Findings

- Validate reachability, expected behavior, impact, and counterevidence.
  Agreement does not prove a finding; uncertainty does not refute one.
- Label each finding **Important** (fix before merge), **Nit** (optional, at most
  three per review), or **Pre-existing** (present at the base, not worsened; never
  blocks). Omit style-only and cleanup comments unless a project rule requires them.
- Deduplicate root causes. Report a defect class once, with every instance.
- Dispositions: validated, refuted, inconclusive, fixed/verified, or explicitly
  accepted-unresolved. Record the author's response: fixed, wrong, intentional, or
  did not matter.
- Propose a lint rule, check, or instruction line for a finding that recurs across
  changes.
- Ask before retaining a real unresolved defect or making a material redesign;
  project policy may prohibit acceptance.

## Re-review

After the first full review, re-review the corrections and the behavior they
affect. Widen only when corrections are large, change the design, or touch
high-risk areas. Do not repeat a posted finding; reopen it only on evidence of a
regression.

## Remediation rounds

At most three autonomous rounds. A round starts with corrective edits and ends at
a verification and re-review verdict or abandonment. Resuming before a verdict
stays in the round; correcting after an unsuccessful verdict starts the next. Keep
the count across resumption, agents, workspaces, and sessions. Stop earlier on
recurrence, no progress, or material conflict, and report incomplete work.
