# Verification rules

Phase reference of the [shared workflow contract](workflow-contract.md).

- **Criteria.** Define observable acceptance criteria before implementation. Take
  expected results from requirements or an independently justified oracle, never
  from the output under test.
- **Risks.** For each material risk, name the assumption that makes the change
  safe and a check that could disprove it. Untested → unverified.
- **Check choice.** Integration tests for real boundaries, E2E for important
  journeys, unit or property tests for pure rules. Feature TDD is optional.
- **Bugs.** A fix needs original-failure evidence; unavailable reproduction is a
  stated limitation, and a setup crash is not reproduction. Verify through the
  interface where the failure occurred; a substitute interface covers only what it
  exercises.
- **Defect detection.** Critical new behavior and bug regressions need
  *defect-detected* evidence: an executed run showing their tests catch a
  plausible defect, such as a failing run against the unfixed code.
- **Real interface.** Start and drive the real user or caller interface with
  project procedures. Check readiness and instance ownership first, inspect side
  effects as well as output, isolate interfering runs, retain evidence, then clean
  up resources the run created. Missing procedure → propose it in scope rather
  than build a verification system.
- **Traceability.** Keep the plan's criterion IDs. Map each criterion to its
  covering checks by file and test name; several checks can cover one criterion.
  A fixed defect gets a regression test whose name states the protected behavior.
  The [coverage map](#coverage-map) records the result.
- **Test IDs.** Separate test-case IDs are optional. The project has adopted a
  test-ID convention → follow it, keep criterion IDs separate, and check ID
  uniqueness with the project's own mechanism. No adopted convention → file and
  test names carry traceability alone.
- **Records.** Read commands from executable configuration. Record what ran, the
  candidate and configuration, the result state, and limitations. Changed code,
  tests, configuration, requirements, or environment → new evidence for affected
  checks. An unavailable required check stays a gap. Test counts and coverage do
  not establish acceptance.
- **Reporting gaps.** Name each criterion whose required check did not run as
  unverified in every summary, status line, and user-requested format. Name a mock,
  stand-in, or local preview as a substitute. "Checks pass" never covers a check
  that did not run.

## Coverage map

The coverage map is a section of the verification report, keyed to the plan's
criterion IDs. Return it in the report; it is never a separate file in the project.

**Rows.** One row per criterion. List each covering check by file and test name
with its evidence level. A required check that did not run has level `none`. A
criterion with no covering check is a gap row with `none`, and its result is
never `pass`.

**Evidence ladder.** Give each check the highest level its evidence supports:

1. *Defect-detected:* reproduced, and an executed run shows the test fails on a
   plausible defect. For a regression test, it fails at the base by assertion and
   passes after the fix.
2. *Reproduced:* an executed run on the current candidate shows the criterion's
   behavior through the interface the criterion names.
3. *Substitute:* an executed run where a mock, stand-in, or local preview
   replaces the behavior the criterion names. A mock of an unrelated dependency
   leaves the level unchanged.
4. *Traced:* source reading cites each step from trigger to result at
   `file:line`. Nothing ran.

`pass` needs at least one *reproduced* check for the behavior the criterion
names, and *defect-detected* where the defect-detection rule applies. Weaker
evidence keeps the criterion `inconclusive` or `unavailable`, with the
missing check named.

**Value cards.** Each test the change adds gets a value card:

```text
Test: file::test_name (criteria)
Protects: the behavior a user or caller relies on
Fails when: the plausible regression that breaks it
Missed before: why existing coverage did not catch that regression
Does not prove: what a pass leaves unverified
```

`Fails when` is a claim until a run shows it; the check's evidence level records
whether it ran. A test that no plausible regression fails protects nothing: name
it as a gap.
