---
name: plan-change
description: Plan a software change or revise an existing plan. Define acceptance criteria, authorized scope, coherent slices, and verification needs. Use for planning requests; planning alone does not start implementation.
---

# Plan change

Produce a plan grounded in the project's requirements and current implementation.
Reuse accepted decisions and valid plans. Keep detail proportional to the change.

Before beginning, read the [shared workflow contract](../../references/workflow-contract.md).
The plugin includes this reference. Keep the plugin directory layout intact.

## 1. Establish scope and ownership

Identify the requested outcome, planning authority, exclusions, and the selected
owner of the requirements and plan. Separate desired behavior from observations
and assumptions. If an accepted plan covers the request, revalidate affected
inputs and propose only necessary amendments.

Done when the source of the requirements and the scope are clear. List unresolved
questions that could change the plan. Inspect observable facts before asking the
user to supply them. Ask for missing intent or material decisions under the shared
contract. Keep dependent work pending and investigate unaffected parts.

## 2. Inspect the affected behavior

Trace the relevant entrypoints, callers, data, contracts, tests, and documentation.
Identify the boundaries and recovery behavior that the change touches. For an
uncertain interface, sketch how its caller would use it before choosing its shape.
Read executable configuration for checks. Consult current primary documentation
when dependency-specific facts matter, using the project's configured tools.

For a bug, gather the existing original-failure evidence or identify the smallest
safe reproduction needed. With planning authority, run relevant read-only checks
when permitted. Creating repro files, provisioning dependencies, or modifying
application code requires appropriate authority; propose these if outside scope.

Done when the plan points to inspected code and places to test the behavior.
Distinguish observations from hypotheses and state what the inspection could not establish.

## 3. Define acceptance and decisions

Draft observable acceptance criteria and exclusions for the selected owner.
Use existing criterion IDs where present. For each behavior, describe the expected
result and the independent basis for that expectation.

For material product or architecture decisions, present the relevant alternatives,
tradeoffs, and recommendation to the authorized decision maker. Proceed with
routine choices already authorized.

Done when each criterion describes an observable result and material decisions
are accepted or explicitly pending. A pending decision does not establish readiness.

## 4. Plan coherent slices and verification

For each slice, name the affected areas, prerequisites, expected result, tests,
and required documentation. Use one slice for a small change. Include migration,
compatibility, rollout, recovery, or external dependency work only where needed.

For each material risk, state the assumption that makes the slice safe and the
check that could disprove it. Distinguish existing proof from planned verification.

Map each criterion to applicable checks under the shared contract. Identify existing
case IDs, new coverage, original-failure evidence, and how critical checks will
demonstrate defect detection. For checks that run an application, identify the
real interface, readiness and isolation needs, relevant side effects, and cleanup
that retains evidence. Reference existing project procedures rather than copying
commands into a second authority.

Name missing test infrastructure or test-ID mechanisms and propose bounded work
to address the gap. Planning does not install them.

Identify independent review needs and specialist triggers. State which required
checks, tools, or environments are unavailable and what would resolve each gap.
A planned check is not a passed check.

Done when each criterion has a verification route or explicit gap, each slice has
an observable end condition, and material risks name an assumption and a check.
State dependencies and blockers.

## 5. Return the plan and stop

Use the project's existing plan format and authorized destination. If persistence
is not authorized, return the draft in the response. Reference existing authorities
instead of creating duplicate editable requirements.

Include the outcome, scope, criteria, inspected evidence, decisions, slices with
tests and documentation, review needs, blockers, and next action. Use the shared
contract's writing guidance. Keep routine plans short; expand where needed.

Report readiness as ready within authorized scope, pending decision, or blocked,
with the reason. A ready plan is not a new grant of implementation permission.
When invoked as a standalone planning phase, stop here. A separately authorized
full-delivery workflow may continue after this phase's conditions are satisfied.
