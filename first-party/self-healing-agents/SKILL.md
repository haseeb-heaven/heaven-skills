---
name: self-healing-agents
description: >-
  Use when an AI or coding agent must recover from tool failures, timeouts, empty or
  incorrect results, flaky validation, or repeated dead ends without bypassing user
  approval or safety boundaries.
version: 1
---

# Self-Healing Agents

## Overview

Self-healing means bounded recovery, not unrestricted autonomy. For every meaningful step, execute, inspect, classify any failure, apply the smallest permitted recovery, verify again, and record what happened.

**Core principle:** a successful tool call is not proof of a correct result.

## Recovery Loop

1. Define the step's expected result and acceptance check.
2. Run one narrowly scoped action.
3. Inspect exit status, output, warnings, changed files, and resulting state.
4. If the result is wrong or incomplete, assign a failure class below.
5. Apply one allowed recovery, then repeat the acceptance check.
6. Stop when the recovery budget is exhausted or a safety boundary is reached.
7. Write a compact recovery-log entry.

Expose tool errors to the agent with their useful details. Never replace a timeout, error, empty result, or validation message with “something went wrong.”

## Failure Classes and Recovery

| Failure | First recovery | Stop condition |
|---|---|---|
| `timeout` | Retry once with a bounded timeout or smaller scope | The operation times out again |
| `tool_error` | Retry a transient error; use a pre-approved equivalent fallback if the tool is unavailable | The fallback changes semantics, security, or evidence quality |
| `empty_result` | Check inputs, paths, filters, credentials, and assumptions | The expected artifact or evidence is still absent |
| `validation_failure` | Diagnose the specific failure, make a focused correction, rerun the same check | Repeated failures suggest the approach or requirement is wrong |
| `wrong_result` | Compare the output with requirements and source evidence; revise the approach | Do not keep guessing or declare success |
| `blocked` | Report the missing input, permission, dependency, or decision | Do not invent access or silently bypass the blocker |
| `risky_action` | Prepare the proposed action and ask for approval when approval is not already explicit | Never auto-execute to “unblock” the workflow |

Use limited retries and a total time/scope budget. A fallback must be genuinely equivalent for the task; do not silently trade away correctness, privacy, or security.

## Repeated Failure: Decompose

When the same operation keeps failing:

- isolate the smallest failing operation;
- separate discovery, implementation, and verification;
- reduce the file, input, or request scope;
- finish and verify one unit at a time;
- recombine only after the units pass.

Preserve the original acceptance criteria while decomposing. Do not “fix” repeated failure by weakening the requirement.

## Safety Stops

Pause before deleting or overwriting material data, resetting unrelated work, spending money, publishing or sending externally, changing permissions or credentials, applying hard-to-reverse migrations, or using an unapproved destructive fallback—unless the user explicitly authorized that exact action in the current scope.

Automatic recovery may inspect, diagnose, draft, or propose a risky action. It must not bypass approval. Ordinary reversible edits already requested by the user do not need an extra confirmation merely because a recovery loop is being used.

## Recovery Log

Record failures and fixes in task state or the project’s designated log without secrets or unnecessary personal data:

```json
{
  "step": "run targeted tests",
  "failure": {"class": "validation_failure", "message": "expected 3, received 2"},
  "attempt": 1,
  "action": "inspect fixture and implementation",
  "result": "stale fixture corrected",
  "verification": "targeted tests pass",
  "remaining_risk": "integration tests not run"
}
```

The log should prevent repeating the same mistake and expose root causes. Do not log tokens, passwords, or sensitive payloads.

## Completion Check

Report success only after the requested state is present, the narrowest relevant checks pass, and the final state has been inspected. If recovery stops, report what was attempted, the evidence gathered, what remains incomplete, and the safest next action.

## Common Mistakes

- Retrying a wrong result instead of examining evidence.
- Treating exit code 0 as correctness.
- Retrying indefinitely or changing scope silently.
- Using a fallback with different semantics.
- Hiding the original diagnostic from the agent.
- Decomposing the task until the acceptance criteria disappear.
- Claiming “self-healed” without rerunning verification.

Source inspiration: [Greg Isenberg’s public post](https://x.com/gregisenberg/status/2095670739852525966?s=46), supplied by the user.

**Author:** [haseeb-heaven](https://github.com/haseeb-heaven)
