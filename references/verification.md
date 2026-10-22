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
- **Defect detection.** Critical new behavior and bug regressions need executable
  evidence that their tests catch a plausible defect, such as a failing run
  against the unfixed code.
- **Real interface.** Start and drive the real user or caller interface with
  project procedures. Check readiness and instance ownership first, inspect side
  effects as well as output, isolate interfering runs, retain evidence, then clean
  up resources the run created. Missing procedure → propose it in scope rather
  than build a verification system.
- **Test IDs.** Integration/E2E cases and material regressions get stable
  behavioral IDs. Keep an ID across renames and moves, retire it explicitly, and
  never reuse it. Check missing or duplicate IDs through generated catalogs. Reuse
  project mechanisms; propose a missing one and its scope before adding it. Keep
  criterion IDs separate from test-case IDs; link cases to criteria so several
  checks can cover one criterion.
- **Records.** Read commands from executable configuration. Record what ran, the
  candidate and configuration, the result state, and limitations. Changed code,
  tests, configuration, requirements, or environment → new evidence for affected
  checks. An unavailable required check stays a gap. Test counts and coverage do
  not establish acceptance.
- **Reporting gaps.** Name each criterion whose required check did not run as
  unverified in every summary, status line, and user-requested format. Name a mock,
  stand-in, or local preview as a substitute. "Checks pass" never covers a check
  that did not run.
