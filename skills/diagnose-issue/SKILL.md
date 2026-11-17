---
name: diagnose-issue
description: Diagnose a bug, failing check, or unexplained behavior from a working reproduction to an evidenced root cause. Use for debugging requests or before fixing a defect whose cause is unknown. Diagnosis stops before the fix and hands off a named regression test.
---

# Diagnose issue

Find why the system fails, prove it, and hand the fix to the next phase. First
read the [contract core](references/workflow-contract.md) and the
[verification rules](references/verification.md).

## Evidence levels

Rate every claim about the cause:

1. Asserted: no pointer.
2. Located: points to a `file:line`.
3. Walked: the failure path traced from input to symptom through the code.
4. Executed: a check against the real code confirmed the claim.
5. Reproduced: the claim confirmed through the interface where the failure occurred.

A confirmed root cause needs level 3 or higher, and level 4 or higher for the
causal claim itself. Report lower-level claims as hypotheses.

## 1. Scope and authority

- Identify the symptom, its reporter, the expected behavior and its source, the
  workspace, the candidate, and the limits. Start the contract's freshness check.
- Diagnosis may read code, run existing checks, and write probes in `.scratch/`
  or another disposable location. Edits to project files need explicit authority:
  a test edit for the regression test, and implementation authority for a fix.
- Expected behavior is unclear → ask the requirements owner; keep the diagnosis
  open on that question.

**Checkpoint 1:** the symptom, the expected behavior, and the permitted actions
are stated.

## 2. Build a red loop

Build one command that goes red on the reported symptom before you form any
theory. A good loop is:

- red on the exact symptom, by assertion or observed output; a setup crash or an
  unrelated error is not red;
- deterministic, or red at a measured rate for flaky failures;
- tight: it runs in seconds when the failure allows it.

Prefer an existing test or command. Otherwise write a probe in scratch, using the
interface where the failure occurred. Run it and record the command, the
candidate, and the red output.

No red loop after a bounded attempt → report what you tried, why it stays green,
and what input or environment is missing. Continue only with claims at level 3 or
lower, labeled as unconfirmed.

**Checkpoint 2:** a recorded run of the loop shows the symptom, or the missing
reproduction is a stated gap.

## 3. Hypothesize and narrow

Keep a hypothesis log, one row per hypothesis:

```text
hypothesis | prediction | test | result | level
```

- Write the prediction before the test. Each test changes one variable.
- Narrow with the cheapest discriminating test: shrink the input, bisect history
  with `git bisect` on the loop, toggle configuration, or add temporary logging in
  a disposable copy.
- Two refuted hypotheses on one premise → write the premise down and test it
  directly.
- Remove temporary instrumentation from project files and keep the probes in
  scratch.

**Checkpoint 3:** one hypothesis survives with a passed prediction, and each
rejected hypothesis has its refuting result.

## 4. Confirm the root cause

Confirm with a causal check: change only the suspected cause in a disposable copy
or scratch probe, and observe the loop turn green; restore it and observe red
again. The cause must explain every reported symptom; name any symptom it leaves
unexplained.

Causal check unavailable → the cause stays a hypothesis at its evidence level.

**Checkpoint 4:** the root cause has a `file:line`, the walked failure path, and a
level 4 or 5 causal check, or it is reported as an unconfirmed hypothesis.

## 5. Hand off and stop

Define the regression test: its file, its name stating the protected behavior,
and its assertion. With test-edit authority, add it and record a red run against
the current code. Without that authority, propose it.

Finish the freshness check and return:

```text
Symptom and loop: command | candidate | red output
Root cause: file:line | mechanism | evidence level
Rejected hypotheses: hypothesis | refuting result
Regression test: file::name | assertion | red run or proposed
Fix direction: smallest change that turns the loop green, and its risks
Gaps and next action:
```

**Done when** the report names a root cause at level 4 or higher with its
regression test, or names the missing evidence. Diagnosis changes no production
code. A standalone request stops here; the fix continues through plan-change or
implement-change, which use the loop and the regression test as original-failure
evidence.
