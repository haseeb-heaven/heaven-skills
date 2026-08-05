---
name: setup-pre-commit
description: >-
  Set up Husky pre-commit hooks for code quality enforcement across all languages.
  Covers configuration for linting, formatting, type checking, testing, and security
  scanning before commits are accepted. Use when initializing a project or adding
  quality gates to an existing repository.
version: 1
---

# Setup Pre-Commit

Set up Husky pre-commit hooks that enforce code quality automatically before every commit.

## When NOT to Use

- Repositories without automated tooling (linters, formatters, tests)
- Solo projects where the developer never makes mistakes
- Monorepos where hook overhead impacts CI performance significantly

## Setup Process

### Step 1: Install Husky
```bash
npx husky-init && npm install
# Or globally:
npm install -g husky
husky install
```

### Step 2: Create Hook Scripts

| Hook | File | Purpose | Command |
|------|------|---------|---------|
| **Pre-commit** | `.husky/pre-commit` | Block bad commits | `lint-staged` |
| **Commit-msg** | `.husky/commit-msg` | Enforce message format | `commitlint` |
| **Pre-push** | `.husky/pre-push` | Final validation | `npm test` |

### Step 3: Configure lint-staged

`package.json` or `.lintstagedrc.json`:
```json
{
  "*.{js,ts,jsx,tsx}": ["eslint --fix", "prettier --write"],
  "*.{json,md,yml}": ["prettier --write"],
  "*.test.{js,ts}": ["vitest run"]
}
```

### Step 4: Add Commit Message Linting

`.commitlintrc.json`:
```json
{
  "extends": ["@commitlint/config-conventional"],
  "rules": {
    "type-enum": [2, "always", [
      "feat", "fix", "docs", "style", "refactor",
      "test", "chore", "perf", "ci"
    ]]
  }
}
```

### Step 5: Enable All Hooks
```bash
npx husky add .husky/pre-commit "npx lint-staged"
npx husky add .husky/commit-msg 'npx commitlint --edit $1'
npx husky add .husky/pre-push "npm test"
```

## Language-Specific Configurations

### TypeScript Projects
```json
// package.json hooks
{
  "*.{ts,tsx}": [
    "tsc --noEmit --pretty false",   // Type check staged files
    "eslint --fix",
    "prettier --write"
  ]
}
```

### Python Projects (using pre-commit framework)
```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pycqa/isort
    rev: 5.13.2
    hooks:
      - id: isort
  - repo: https://github.com/psf/black
    rev: 24.4.2
    hooks:
      - id: black
  - repo: https://github.com/pycqa/flake8
    rev: 7.0.0
    hooks:
      - id: flake8
```

### Go Projects
```yaml
repos:
  - repo: https://github.com/dnephin/pre-commit-golang
    rev: v1.2.0
    hooks:
      - id: go-fmt
      - id: go-vet
      - id: go-build
```

## Best Practices

1. **Fast hooks only on pre-commit** — Keep pre-commit under 5 seconds; move heavy checks to pre-push
2. **Auto-fix on stage** — Use `--fix` flags so hooks can auto-correct simple issues
3. **Fail fast** — Stop at the first failing hook rather than running everything
4. **Document bypass** — Tell teammates `git commit --no-verify` exists for emergencies
5. **Test hooks regularly** — A broken hook blocks everyone silently

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "command not found" | Ensure dependencies in `package.json` devDependencies |
| Hook runs on every file | Verify `lint-staged` config uses correct glob patterns |
| Slow commits | Remove heavy checks from pre-commit; move to pre-push |
| Hooks don't work after pull | Run `npx husky install` after major dependency changes |
