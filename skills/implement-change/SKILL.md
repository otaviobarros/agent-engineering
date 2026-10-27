---
name: implement-change
description: Implement an accepted software change plan with scoped code, tests, and documentation. Use for the implementation phase or to resume an authorized slice. Standalone implementation stops before independent review and publication.
---

# Implement change

Produce the authorized changes and usable verification inputs. First read the
[contract core](../../references/workflow-contract.md) and the
[verification rules](../../references/verification.md).

## 1. Confirm the plan and authority

- Identify the requirements owner, accepted plan, criteria, authorized slice, and
  limits. Confirm workspace, branch, revision, and existing staged and untracked
  changes.
- Revalidate the plan against current inputs and reuse its valid decisions. Open
  criterion or material decision → report it and keep dependent work pending.
- An accepted plan alone does not authorize edits.

**Checkpoint 1:** the slice has an accepted expected result and implementation
authority, or a clear blocker.

## 2. Ground the slice

- Trace affected entrypoints, callers, contracts, test procedures, and executable
  check configuration. Follow project conventions and existing interfaces; use
  the plan's checks. Material redesign or scope expansion → get a decision.
- After reading affected code, follow this reuse-first ladder. Take the first
  option that fully meets the accepted criteria:
  1. Skip what the request does not need, including unrequested features and
     speculative options; name what you skip.
  2. Search the codebase for an existing helper or pattern before writing a helper,
     parser, formatter, or validator. State what you found or did not find;
     reuse it the way surrounding code does.
  3. Use a standard library or platform feature.
  4. Use an installed dependency. Never add one for a few lines.
  5. Otherwise, write the minimum code that works.

  Never cut validation at trust boundaries, error handling that prevents data
  loss, security, or accessibility. New non-trivial logic still needs a test.
- Bug fix → capture original-failure evidence before corrective edits when
  available; otherwise state the limitation.

**Checkpoint 2:** edits and test expectations rest on inspected code and accepted
criteria. Pre-existing failures are recorded separately.

## 3. Implement

- Make scoped code, test, and documentation changes; keep accepted behavior
  outside the slice. Apply the verification rules. A bug regression exercises the
  interface where the original failure occurred.
- Reuse project test mechanisms. Propose missing infrastructure and its scope
  before adding it within authority; beyond scope it is a required gap.
- Dependency installation, migrations, external effects, and experiments need
  their own authority; the plan does not expand execution permission.
- Run relevant development checks within authority and record command, candidate,
  outcome, and limitation. Keep evidence before cleaning up resources you created.
- Fix scoped defects within the three-round limit in the
  [review rules](../../references/review.md#remediation-rounds). A blocked
  required check leaves unaffected work free to continue.

**Checkpoint 3:** authorized edits, tests, and docs are present, or incomplete items
are explicit. A passing local check is not full verification.

## 4. Inspect and hand off

After the last edit and check, compare the final diff, staged and untracked
contents, branch, and revision with the slice and existing work. Run the
contract's freshness check for earlier evidence. Then hand off in an authorized
record or the response:

```text
Behavior implemented:
Criteria affected: (reference the plan)
Checks: command | candidate | result | limitation
Not verified: criteria whose required check did not run, and why
Final inspection: branch, revision, dirty inputs, scope and preservation result
Remaining work, gaps, next action:
```

If the task mentions speculative or future needs, include a `Not built: …`
line naming what you left out.

Carry `Not verified` into any status the user asks for.

Incomplete inspection → name the missing evidence and mark the handoff incomplete.

**Done when** changes and verification inputs are accounted for, with failures and
gaps visible, and every criterion whose required check did not run is listed under
`Not verified` in the handoff and any requested status. Implementation completion is not verification, review, or delivery
readiness. A standalone request stops here; authorized delivery continues with
verify-change and review-change. No commits, pushes, or publication.
