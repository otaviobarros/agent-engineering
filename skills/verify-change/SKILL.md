---
name: verify-change
description: Verify a software change against acceptance criteria. Run relevant checks and report evidence, failures, and gaps. Use for verification requests or the verification phase of delivery; verification alone does not authorize fixes or publication.
---

# Verify change

Establish what the current candidate demonstrates and what remains unverified.
First read the [contract core](../../references/workflow-contract.md) and the
[verification rules](../../references/verification.md).

## 1. Scope

- Identify the requirements owner, criteria, workspace, candidate, and limits.
  Reuse evidence only while its inputs remain valid.
- Read project instructions and executable check configuration; establish the
  authorized commands, environments, and side effects.
- Missing criteria or procedures → propose them to the owner. Expectation depends
  on an open decision → keep that verification pending.

**Checkpoint 1:** each requested behavior has an authoritative expectation or a
gap, and the permitted actions are clear.

## 2. Select checks

- Map each criterion and material risk to checks. Separate checks with valid
  evidence from checks that need a run.
- **Test-ID gate.** For integration/E2E cases and material regressions, validate
  stable IDs with the project's generated catalog. Require valid executable
  evidence that the checker rejects all three: a missing ID, a duplicate ID, and a
  duplicate definition that test collection can hide. Reuse valid evidence, else
  probe in authorized disposable copies; add source checks where collection falls
  short. A handwritten mapping is not validation. Probes impossible in scope →
  required validation gap.
- Missing coverage, ID validation, or defect-detection evidence → report the gap
  and propose scoped work. Editing the candidate, adding infrastructure, or
  installing dependencies needs implementation authority.

**Checkpoint 2:** each criterion and material risk has evidence, a check to run, or
a gap. Criterion IDs stay separate from test-case IDs.

## 3. Run

1. Start the contract's freshness check.
2. Run checks that need new evidence through the real interface, per the
   verification rules.
3. Record commands, candidate, configuration, environment, results, and
   limitations. Classify setup failures apart from application failures.
4. Failure → keep the evidence and name the affected criteria. Fixes need
   implementation or remediation authority. Continue unaffected checks.

**Checkpoint 3:** each selected check has an outcome or an execution gap.

## 4. Check freshness, report, and stop

Finish the freshness check and return:

```text
Candidate checked: revision and content identities
Freshness: before/after identities | unchanged | changed (renewed checks) | unverified
criterion | evidence/check | result | limitation
Next action:
```

One row per requested criterion, using the contract's result states. A criterion
awaiting independent review is `pending`, with review as the next check; update it
when review evidence arrives. Every criterion without a supported pass stays a
visible gap downstream. Fictional example:

```text
AC-2 expired reset link refused | test_reset.py::test_expired (AUTH-E2E-007), browser | pass | staging clock only
```

**Done when** every requested criterion has a supported result or a gap. Failed,
unavailable, or inconclusive required checks leave dependent delivery incomplete.
Verification replaces neither independent review nor publication authority. A
standalone request stops here.
