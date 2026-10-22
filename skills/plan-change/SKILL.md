---
name: plan-change
description: Plan a software change or revise an existing plan. Define acceptance criteria, authorized scope, coherent slices, and verification needs. Use for planning requests; planning alone does not start implementation.
---

# Plan change

Produce a plan grounded in the project's requirements and current code. Reuse
accepted decisions and valid plans; keep detail proportional to the change. First
read the [contract core](../../references/workflow-contract.md) and the
[verification rules](../../references/verification.md).

## 1. Scope and ownership

- Identify the requested outcome, planning authority, exclusions, and the owner of
  the requirements and plan. Separate desired behavior from observations and
  assumptions.
- An accepted plan covers the request → revalidate affected inputs and propose
  only necessary amendments.
- List questions that could change the plan. Answer observable ones by
  inspection; ask for missing intent and material decisions.

**Checkpoint 1:** the requirements source and scope are clear.

## 2. Inspect the affected behavior

- Trace entrypoints, callers, data, contracts, tests, and docs, including the
  boundaries and recovery behavior the change touches. For an uncertain interface,
  sketch its caller's use before choosing its shape.
- Read executable check configuration. Consult current primary documentation with
  the project's tools when dependency facts matter.
- Bug → gather existing original-failure evidence or name the smallest safe
  reproduction. Read-only checks may run when permitted. Repro files, dependency
  provisioning, or application edits need their own authority; propose them.

**Checkpoint 2:** the plan cites inspected code and test locations, separates
observations from hypotheses, and states what inspection could not establish.

## 3. Acceptance and decisions

- Draft observable acceptance criteria and exclusions for the owner, reusing
  existing criterion IDs. Give each expected result its independent basis.
- Material product or architecture decision → present alternatives, tradeoffs, and
  a recommendation to the authorized decision maker. Routine authorized choices
  proceed.

**Checkpoint 3:** each criterion is observable, and each material decision is
accepted or explicitly pending. A pending decision blocks readiness.

## 4. Slices and verification

- Per slice: affected areas, prerequisites, expected result, tests, and required
  docs. A small change is one slice. Add migration, compatibility, rollout,
  recovery, or external-dependency work only where needed.
- Per material risk: the assumption and a disproving check. Separate existing
  proof from planned verification.
- Per criterion: checks under the verification rules (existing case IDs, new
  coverage, original-failure evidence, defect detection). For application runs,
  name the real interface, readiness and isolation needs, side effects, and
  evidence-preserving cleanup. Point to project procedures instead of copying
  commands.
- Name missing test infrastructure or test-ID mechanisms and propose bounded work;
  planning installs nothing.
- Name independent-review needs and specialist triggers, and for each unavailable
  check, tool, or environment, what would resolve it. A planned check is not a
  passed check.

**Checkpoint 4:** every criterion has a verification route or a gap. Every slice has
an observable end condition, and every material risk an assumption and a check.
Dependencies and blockers are stated.

## 5. Return the plan and stop

Use the project's plan format and authorized destination, else return the draft
in the response. Reference existing authorities instead of copying requirements.
Every plan, however small, includes:

- [ ] Outcome, scope, and exclusions
- [ ] Acceptance criteria, by ID or source when they exist
- [ ] Inspected evidence and open questions
- [ ] Decisions, accepted or pending
- [ ] Slices with tests and docs
- [ ] Criterion-to-check map
- [ ] Review needs, blockers, and next action
- [ ] Readiness: ready within authorized scope, pending decision, or blocked, with the reason

Keep prose short without dropping an item. A ready plan grants no implementation
permission. A standalone planning request stops here.
