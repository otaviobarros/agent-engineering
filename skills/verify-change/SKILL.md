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
- **Traceability.** Cite each covering check by file and test name. Confirm that
  each fixed defect has a named regression test. Plan each check's evidence level
  on the [coverage map](../../references/verification.md#coverage-map) ladder.
- **Adopted test IDs.** The project has adopted a test-ID convention → check ID
  uniqueness with the project's own mechanism. Mechanism missing or not run →
  required validation gap. No adopted convention → trace by file and test name only.
- Missing coverage, defect-detection evidence, or adopted ID validation → report
  the gap and propose scoped work. Editing the candidate, adding infrastructure, or
  installing dependencies needs implementation authority.

**Checkpoint 2:** each criterion and material risk has evidence, a check to run, or
a gap. Criterion IDs stay separate from any test-case IDs.

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

Finish the freshness check and return the report with its
[coverage map](../../references/verification.md#coverage-map):

```text
Candidate checked: revision and content identities
Freshness: before/after identities | unchanged | changed (renewed checks) | unverified
Coverage map:
criterion | file::test @ level; ... | result | limitation
Gaps: criteria with no covering check, or none
Value cards: one per test the change adds
Next action:
```

One row per requested criterion, using the contract's result states. Each level
rests on a run or citation in this report. Reuse an implementer's value card only
after checking its `Fails when` claim against the evidence. A criterion
awaiting independent review is `pending`, with review as the next check; update it
when review evidence arrives. Every criterion without a supported pass stays a
visible gap downstream. Fictional example:

```text
AC-2 expired reset link refused | tests/test_reset.py::test_expired_reset_link_is_refused @ defect-detected; browser reset form @ reproduced | pass | staging clock only
AC-3 reset email sent | tests/test_reset.py::test_reset_email_queued @ substitute | inconclusive | mail relay mocked
```

**Done when** every requested criterion has a coverage-map row with a supported
result or a gap, and every added test has a value card. Failed,
unavailable, or inconclusive required checks leave dependent delivery incomplete.
Verification replaces neither independent review nor publication authority. A
standalone request stops here.
