---
name: implement-change
description: Implement an accepted software change plan with scoped code, tests, and documentation. Use for the implementation phase or to resume an authorized slice. Standalone implementation stops before independent review and publication.
---

# Implement change

Produce the authorized changes and usable verification inputs.
Read the [shared workflow contract](../../references/workflow-contract.md) before starting.
The plugin includes this reference. Keep its directory layout intact.

## 1. Confirm the plan and authority

Identify the requirements owner, accepted plan, acceptance criteria, authorized
slice, and explicit limits. Confirm the actual workspace, branch, revision, and
relevant existing changes under the shared contract. Preserve unrelated work,
including existing staged and untracked content.

Revalidate the accepted plan against current inputs. Inspect observable facts
before asking for missing intent. If criteria or material decisions remain
unresolved, report the decision needed and keep dependent implementation pending.
Continue unaffected authorized work. An accepted plan alone does not authorize edits.

Done when the slice has an accepted expected result and implementation authority,
or a clear blocker. Reuse valid decisions rather than creating a second plan.

## 2. Inspect the slice and establish evidence

Trace the affected entrypoints, callers, contracts, and existing test procedures.
Read executable check configuration. Identify the smallest coherent changes and
the applicable checks from the accepted plan. Use project conventions and existing
interfaces; obtain a decision before a material redesign or scope expansion.

For a bug fix, capture original-failure evidence before corrective edits when
available. State missing reproduction as a limitation. A setup failure does not
demonstrate the bug. Derive expected results from the requirements or an independent
oracle under the shared contract.

Done when the edits and test expectations are grounded in inspected code and
the accepted criteria. Record relevant pre-existing failures separately.

## 3. Implement the coherent slice

Make scoped code, test, and documentation changes. Preserve accepted behavior
outside the slice. Apply the shared contract's test selection, stable case identity,
criterion mapping, and defect-detection requirements. Feature TDD remains optional.
For a bug regression, exercise the interface where the original failure occurred.

Reuse project test mechanisms. Propose missing infrastructure and its scope before
adding it within existing authority. Report a required gap when that work exceeds
scope. Dependency installation, migrations, external effects, and experiments need
authority for their own actions; the plan does not expand execution permissions.

Run relevant development checks within authority. Record actual commands, candidate
inputs, outcomes, and limitations. Preserve evidence before cleaning up resources
the run created. Address scoped defects under the shared remediation limits;
continue useful unaffected work when a required check is blocked.

Done when the authorized edits, tests, and documentation are present, or incomplete
items are explicit. Passing a local check does not establish full verification.

## 4. Inspect the final changes and hand off

After the last edit and development check, inspect the final diff, relevant staged
and untracked contents, branch, and current revision.
Check the result against the accepted slice and existing work. Renew affected
check evidence when relevant inputs changed; retain earlier results against their
earlier candidate. Report incomplete freshness as a gap.

Return the implemented behavior, affected criteria, actual check
results, remaining work, and next action. Reference the authoritative plan and
evidence rather than creating duplicate editable requirements. Update records only
at authorized destinations; otherwise provide the handoff in the response.

Report the final inspection outcome with the observed branch, revision, relevant
dirty inputs, and scope/preservation result. If inspection is incomplete, name the
missing evidence and report the handoff as incomplete.

Done when changes and verification inputs are accounted for, with failures and
required gaps visible. Distinguish implementation completion from verification,
independent review, and delivery readiness. Standalone implementation stops here.
A separately authorized delivery workflow can continue with verify-change and
review-change. This skill does not authorize commits, pushes, or publication.
