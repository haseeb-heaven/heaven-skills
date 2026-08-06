---
name: remove-ai-slops
description: Use when software developers need to clean AI-generated source code, simplify agent-written implementation changes, or prepare a code diff for production review.
---

# Remove AI Slops

> Upstream: `code-yeongyu/oh-my-openagent` — `packages/shared-skills/skills/remove-ai-slops/SKILL.md`

Clean a bounded source-code diff while preserving observable software behavior.

**Software-development scope only:** use for application code, tests, scripts, configuration, migrations, build files, and developer tooling. Do not use for prose, articles, marketing copy, resumes, general documents, research summaries, or non-code content.

**Safety invariant:** establish green regression coverage before deleting or restructuring code.

## Scope

Default to the branch diff:

```bash
git diff $(git merge-base origin/main HEAD)...HEAD --name-only
```

Exclude generated files, vendored dependencies, binaries, lockfiles, and unrelated changes.

## Deletion ladder

For each changed unit, decide in this order:

1. Delete it if the behavior is unnecessary.
2. Reuse an existing project implementation.
3. Replace it with a standard-library, platform, or existing-dependency feature.
4. Simplify it in place only when it must remain.

## Slop categories

Review for:

- comments that merely restate code;
- broad or empty exception handling;
- defensive checks with no reachable failure condition;
- deep nesting, nested ternaries, long parameter lists, and god functions;
- pass-through wrappers and speculative abstractions;
- wrong-layer imports and hidden coupling;
- unused code, debug output, and stale compatibility paths;
- copy-paste duplication and repeated literals;
- obviously equivalent performance waste such as repeated work in loops or N+1 calls;
- missing behavioral tests;
- oversized modules with multiple responsibilities.

Preserve boundary validation, security controls, I/O handling, nullable database handling, business-rule comments, and intentional rollback paths.

## Required process

1. Identify public behavior for every in-scope source file.
2. Find or add the narrowest regression tests that lock that behavior.
3. Run the relevant tests and require a green baseline.
4. Produce a file-by-file cleanup plan before editing.
5. Apply the smallest behavior-preserving changes.
6. Run formatting, lint, type checks, unit/integration tests, and configured security scans.
7. Revert any cleanup that cannot be proven safe.

## Completion report

Report:

- files reviewed;
- slop removed by category;
- intentionally retained code and why;
- commands run with exit codes;
- remaining risks or deferred cleanup.

Never claim cleanup is safe without fresh verification evidence.