---
name: greploop
description: >-
  The grep → fix → re-grep loop for fixing repeated code issues at scale. Use when a
  problem appears in many places across the codebase (same pattern, same bug, same
  convention violation) and you need to find every occurrence, fix them all, and
  verify nothing was missed. Faster and more reliable than eyeballing files one by one.
version: 1
---

# GrepLoop — Find, Fix, Verify

The disciplined loop for eliminating a class of bug or pattern across an entire codebase. Instead of fixing occurrences ad-hoc as you spot them, you treat the search query as the source of truth and iterate until the query returns zero results.

## The Loop

```
┌──────────────┐
│ 1. GREP       │  Find every occurrence of the pattern
└──────┬───────┘
       ▼
┌──────────────┐
│ 2. FIX        │  Fix each occurrence (or fix the root cause)
└──────┬───────┘
       ▼
┌──────────────┐
│ 3. RE-GREP    │  Verify: query should now return 0 (or expected-only) results
└──────┬───────┘
       │  still matches?
       ▼
   repeat 2 → 3
```

**Exit condition:** the grep returns zero unexpected matches, and the relevant tests/build pass.

## When to Use

- **Same bug in N places** — `user.email` accessed before a null check, in 7 files
- **Convention migration** — `var x` → `let x`, `assert.equal` → `expect().toBe`, renamed import paths
- **Deprecation cleanup** — an API removed in v2 still used in 15 spots
- **Security sweep** — `innerHTML =` assignments, `eval(` calls, hardcoded secrets, `0.0.0.0` binds

## When NOT to Use

- A one-off fix in a single file — just fix it directly
- The pattern is intentional in some places — you'll need a denylist/exclude approach instead
- Dynamic patterns that grep can't express (semantic, cross-file) — use AST tools (`rg --multiline`, `eslint`, `gofmt -r`, codemods)

## How to Run It

### Step 1: GREP — Write the sharpest query

Make the pattern as specific as possible so results are actual problems, not lookalikes.

```bash
# Bad: matches every "user." access — too broad
rg "user\." src/

# Good: matches the null-unsafe access pattern only
rg "user\.email" src/ --glob "*.ts"

# Include context to review matches quickly
rg -n -C 2 "innerHTML\s*=" src/
```

**Always review the full match list before fixing.** Decide: which matches are real problems vs. which are false positives? If more than ~20% are false positives, sharpen the query.

### Step 2: FIX — Every occurrence or the root cause

Two strategies:

1. **Fix each occurrence** (mechanical, same change everywhere) — safest for isolated bugs
2. **Fix the root cause** (change one shared function/helper the others call) — better when the bug is in shared code; re-grep to confirm occurrences disappear

For each fix:
- Keep the change minimal — same shape as surrounding code
- Don't fix adjacent (unrelated) problems you spot along the way — note them and move on (scope discipline)

### Step 3: RE-GREP — Verify zero

```bash
# The same query from Step 1 — now should be empty (or only expected false positives)
rg "user\.email" src/ --glob "*.ts"
```

**The query is the contract.** If it still matches, you missed something. Fix and repeat. Never skip this step — the loop only closes when re-grep is clean.

### Step 4: Confirm the build/tests

```bash
npm test && npm run build   # or your equivalent
```

A clean grep is necessary but not sufficient — the fixes must not break behavior.

## Output Format

Report the loop's result:

```markdown
## GrepLoop Report

### Pattern
`[the grep query]`

### Scope
- N files, M occurrences found

### Fixes
| File | What Changed |
|------|-------------|
| src/a.ts | Added null guard before `user.email` |
| src/b.ts | Same |

### Verification
- [x] Re-grep: 0 remaining matches
- [x] Tests pass
- [x] Build passes

### Left Intentionally (false positives / denylisted)
- [list, with reasons]
```
