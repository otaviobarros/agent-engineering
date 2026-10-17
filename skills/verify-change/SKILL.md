---
name: verify-change
description: Verify a software change against acceptance criteria. Run relevant checks and report evidence, failures, and gaps. Use for verification requests or the verification phase of delivery; verification alone does not authorize fixes or publication.
---

# Verify change

Establish what the current candidate demonstrates and what remains unverified.
Read the [shared workflow contract](../../references/workflow-contract.md) before starting.
The plugin includes this reference. Keep its directory layout intact.

## 1. Establish the verification scope

Identify the requirements owner, acceptance criteria, workspace, candidate, and
explicit limits under the shared contract. Include relevant uncommitted inputs
in the candidate identity. Reuse existing evidence only while its inputs remain valid.

Inspect project instructions and executable check configuration. Establish which
commands, environments, and side effects are authorized. Preserve existing work.
Propose missing criteria or procedures for the selected owner; keep dependent
verification pending when the expected behavior requires an unresolved decision.

Done when each requested behavior has an authoritative expectation or an explicit
gap, and the permitted verification actions are clear.

## 2. Select checks and assess their evidence

Map acceptance criteria and material risks to existing checks. Apply the shared
contract's test selection, original-failure, independent-oracle, and defect-detection
requirements. Distinguish checks already supported by valid evidence from checks
that still need execution. Test names and coverage totals do not establish acceptance.

For integration/E2E and material regressions, verify stable case IDs using the
project's generated catalog and validation. Check missing IDs, duplicate IDs,
and duplicate definitions that test collection can hide. Require valid executable
evidence that the checker rejects all three failures. Reuse evidence whose inputs
remain valid; otherwise run probes in authorized disposable copies. If probes
cannot run within scope, report a required validation gap. Supplement collection
with source checks where needed. A handwritten mapping is not validation.

If required coverage, test-ID validation, or defect-detection evidence is missing,
report the gap and propose scoped work. Verification alone does not authorize
editing the candidate, adding infrastructure, or installing dependencies.

Done when each criterion and material risk has applicable evidence, an executable
check, or a stated gap. Keep criterion IDs separate from test-case IDs.

## 3. Run authorized checks

Before execution, record the current revision and content fingerprints for relevant
code, tests, requirements, and check configuration. Use these as the checked baseline.

Run checks that need new evidence through the applicable real caller or user
interface. Use project procedures for readiness, instance ownership, isolation,
side effects, and cleanup under the shared contract. Retain evidence before
cleaning up resources the run created.

Record the actual commands, candidate, relevant configuration and environment,
results, and limitations. Classify setup failures separately from application
failures. A substitute interface supports only the behavior it exercises.

On failure, preserve the evidence and identify the affected criteria. Fixes require
implementation or remediation authority. Continue useful unaffected checks within scope.

Done when selected checks have recorded outcomes or explicit execution gaps.

## 4. Check freshness, report, and stop

After checks finish, obtain the current revision and content fingerprints again.
Compare them with the checked baseline, including relevant staged, unstaged,
and untracked contents. Include relevant requirements,
configuration, and environment changes. HEAD and Git status alone cannot establish
unchanged contents. Renew affected evidence when inputs change. Keep superseded
results bound to their earlier candidate.

Return the candidate checked, criteria-to-evidence mapping, actual results,
limitations, freshness outcome, and next action. Distinguish pass, fail, pending,
unavailable, and inconclusive. Report any freshness comparison that could not be
completed; do not claim unchanged inputs without observed evidence. Report the
observed before/after identities and comparison result. Without that comparison,
report freshness as unverified and verification as incomplete.

Done when every requested criterion has a supported result or explicit gap.
Failed, unavailable, or inconclusive required checks leave dependent delivery
incomplete. Verification does not replace independent review or authorize publication.
For a standalone request, stop here. A separately authorized delivery workflow
can continue under the shared contract.
