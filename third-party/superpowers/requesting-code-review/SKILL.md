---
name: requesting-code-review
description: Use when completing tasks, implementing major features, fixing complex bugs, or preparing changes for merge.
---

# Requesting Code Review

> Upstream: `obra/superpowers` — `skills/requesting-code-review/SKILL.md`

Dispatch an independent reviewer with precise requirements and an exact commit range. Do not give the reviewer the implementation session history.

## Required workflow

1. Establish the review range:

```bash
BASE_SHA=$(git merge-base origin/main HEAD)
HEAD_SHA=$(git rev-parse HEAD)
```

2. Give the reviewer:
   - what was built;
   - the requirements or acceptance criteria;
   - `BASE_SHA` and `HEAD_SHA`;
   - relevant test commands and risk areas.
3. Require file-and-line evidence for every issue.
4. Fix Critical issues immediately and Important issues before proceeding.
5. Push back only with technical evidence, tests, or documented requirements.
6. Re-run review after substantive fixes.

## Reviewer prompt

```text
Review BASE_SHA...HEAD_SHA against the supplied requirements.
Inspect the complete diff and directly related callers, tests, schemas,
migrations, configuration, and boundaries.

Classify findings as Critical, Important, or Minor. For each finding include:
- file and line;
- defect and realistic failure scenario;
- evidence;
- required correction;
- test that proves the correction.

Do not praise, speculate, or report style preferences as defects.
Do not approve while Critical or Important findings remain.
```

## Red flags

Never skip review because a change appears small. Never trust an agent's completion claim without inspecting the diff and fresh verification evidence.