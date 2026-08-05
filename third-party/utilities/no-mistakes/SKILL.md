---
name: no-mistakes
description: >-
  Validate code changes against best practices, common pitfalls, and project conventions
  before they reach production. Covers security checks, error handling verification,
  edge case analysis, performance review, and dependency safety. Use when preparing
  code for merge, reviewing PRs, or running a quality gate before deployment.
version: 1
---

# No Mistakes

Validate code changes against best practices, preventing common bugs from reaching production.

## When NOT to Use

- Early prototype code — premature validation kills innovation speed
- Massive refactors — validate incrementally, not as a final gate
- Non-code deliverables (design docs, specs) — different review criteria

## Validation Checklist

### Security
- [ ] No hardcoded secrets, API keys, or passwords
- [ ] User input is sanitized before use in queries, templates, or commands
- [ ] Authentication/authorization checked at every protected endpoint
- [ ] Dependencies have no known CVEs (`npm audit`, `pip-audit`)
- [ ] File operations validate paths (no path traversal)

### Error Handling
- [ ] Every external call has try/catch or promise rejection handler
- [ ] Errors include context (file, line, input data) for debugging
- [ ] No swallowed exceptions (`catch(e) {}`) without logging
- [ ] Timeout handling for network/database operations
- [ ] Database transactions roll back on partial failure

### Edge Cases
- [ ] Empty arrays/objects/null handled explicitly
- [ ] Pagination covers last page with fewer items
- [ ] Race conditions considered for concurrent users
- [ ] Large inputs tested for memory/CPU limits
- [ ] Unicode/special characters don't break parsing

### Performance
- [ ] No N+1 database query patterns
- [ ] Loops don't contain synchronous blocking operations
- [ ] Results are cached where appropriate (memoization, Redis, browser cache)
- [ ] Memory-intensive operations stream rather than loading everything
- [ ] No unnecessary re-renders in UI code

### Code Quality
- [ ] New code follows existing naming conventions
- [ ] Functions do one thing; files aren't larger than ~300 lines
- [ ] Comments explain why, not what (the code shows what)
- [ ] Test files match implementation file structure
- [ ] No debug statements, console.logs, or commented-out code

## Running Validation

```bash
# Quick checks (fast, run frequently)
npx eslint src/                          # Linting
npx tsc --noEmit                        # Type check
npx prettier --check src/               # Format check

# Deeper checks (slower, run before merge)
npm test                                # All tests pass
npm run audit                           # Dependency vulnerabilities
npx ts-node scripts/validate-changes.ts # Custom validation script
```

## Severity Classification

| Level | Description | Action |
|-------|-------------|--------|
| 🔴 Critical | Will cause runtime failure, data loss, or security breach | Must fix |
| 🟡 Warning | Likely causes issues under specific conditions | Should fix |
| 💡 Suggestion | Improves maintainability but won't break anything | Optional |

## Output Format

```markdown
## No-Mistakes Validation Report

### Result: [PASS / WARN / FAIL]

### Issues Found
| Severity | File | Line | Issue | Recommendation |
|----------|------|------|-------|---------------|
| 🔴 | api/users.ts | 42 | Missing null check | Add `if (!user) throw new NotFoundError()` |

### Passed Checks
- ✅ Security scan clean
- ✅ All tests passing
- ✅ Linting clean
- ✅ Type checking passed

### Overall Confidence Score: X/10
[Rationale for score]
```

**Source:** [kunchenguid/no-mistakes](https://github.com/kunchenguid/no-mistakes) — "git push no-mistakes" — clean PRs by default
