---
name: git-guardrails-claude-code
description: >-
  Set up Claude Code hooks and guardrails for safe, automated code quality checks.
  Covers pre-commit hooks, pre-push validations, CI integration patterns, error handling
  rules, and commit message standards. Use when configuring Claude Code safety nets or
  automating code quality enforcement.
version: 1
---

# Git Guardrails for Claude Code

Set up Claude Code hooks and guardrails that enforce code quality before changes reach your repository.

## When NOT to Use

- Simple personal projects without team contribution — manual review is sufficient
- Rapid prototyping where speed matters more than correctness
- One-off scripts that won't be maintained

## Guardrail Types

| Type | Runs When | Purpose | Example |
|------|-----------|---------|---------|
| **Pre-commit** | `git commit` | Block bad commits | Lint check, format validation |
| **Pre-push** | `git push` | Final gate before sharing | Tests, security scan |
| **Commit-msg** | Commit creation | Enforce message format | Conventional commits validation |
| **Post-merge** | After merge | Auto-upstream dependencies | Update lockfiles after package install |

## Setup Process

### Step 1: Install Husky (or equivalent)
```bash
npx husky init        # For Node.js projects
# Or for other languages:
pip install pre-commit && pre-commit install
```

### Step 2: Define Hooks

| Hook File | Command | What It Checks |
|-----------|---------|---------------|
| `.husky/pre-commit` | `npm run lint` | Code style violations |
| `.husky/pre-push` | `npm test` | All tests pass |
| `.husky/commit-msg` | `commitlint -E HUSKY_GIT_PARAMS` | Conventional commit format |

### Step 3: Configure Claude Code Integration
Tell Claude Code which guardrails are active so it respects them during generation:

```markdown
<!-- In CLAUDE.md -->
## Guardrails Active
- Pre-commit runs: npm run lint --fix (auto-fixes enabled)
- Pre-push runs: npm test -- --ci (CI mode)
- Commit messages must follow: conventional-commits.org
```

### Step 4: Test the Hooks
```bash
echo "console.log('broken');" > test-broken.js
git add test-broken.js
git commit -m "test"  # Should fail if hook is configured
```

## Common Guardrail Patterns

### Auto-Fix Before Blocking
Instead of blocking on errors, attempt auto-fix first:
```bash
# .husky/pre-commit
npx eslint src/ --fix && npx prettier src/ --write
git add -u
```

### Staged Changes Only
Run checks only on staged files for speed:
```bash
# .husky/pre-commit
npx eslint $(git diff --cached --name-only --diff-filter=ACM)
npx prettier --check $(git diff --cached --name-only --diff-filter=ACM)
```

### Skip Hooks When Needed
```bash
git commit --no-verify    # Bypass pre-commit hook
git push --no-verify      # Bypass pre-push hook
```

## Output Format

When setting up guardrails, report:

```markdown
## Guardrail Configuration

### Installed Hooks
| Hook | Script | Status |
|------|--------|--------|
| pre-commit | [command] | ✅ Active |
| pre-push | [command] | ✅ Active |

### Test Results
- [x] Blocked a commit with lint errors
- [x] Blocked a push with failing tests
```
