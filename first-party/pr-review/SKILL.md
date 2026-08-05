---
name: pr-review
description: >-
  AI-powered pull request review skill. Analyzes PR diffs, identifies issues,
  suggests improvements, checks best practices, and validates code quality
  before merge. Use when reviewing pull requests, examining code diffs, or
  evaluating proposed changes.
version: 1
---

# Pull Request Review Skill

Systematic approach to reviewing pull requests that catches real problems without wasting time on noise.

## Workflow

1. **Understand intent** — Read the PR description, linked issues, and any discussion comments to understand what the PR is trying to achieve. A review that misses the point is worse than no review.

2. **Read the diff** — Focus on changed lines. Ignore whitespace-only changes and auto-generated files unless they're suspicious. Understand the scope: is this a single small fix or a sweeping refactor?

3. **Check correctness** — Verify logic flow, edge cases, error handling, and data access patterns. Look for off-by-one errors, null/undefined paths, race conditions, and security concerns (SQL injection, XSS, path traversal).

4. **Assess readability** — Are variable names descriptive? Is the function doing one thing? Would someone unfamiliar with the code understand it in two weeks? Flag complex expressions, deep nesting, and magic numbers.

5. **Evaluate design** — Does the change follow existing patterns in the codebase? Is it adding new dependencies justified by the benefit? Does it introduce architectural coupling that shouldn't exist?

6. **Test strategy** — Does the PR include tests? Are they testing the right behavior (public interface) rather than implementation details? Do they cover edge cases, not just the happy path?

## Severity Levels

| Level | When to Use | Expectation |
|-------|-------------|-------------|
| 🔴 Blocker | Security issue, data loss, breaking API | Must be fixed before merge |
| 🟡 Concern | Suboptimal pattern, missing edge case, tech debt | Should be addressed, can merge after discussion |
| 💡 Suggestion | Style, naming, minor improvement | Author may accept or decline |

## What to Skip

- Comments about personal style preferences already established in the project
- Nitpicks on unchanged boilerplate (config files, generated code)
- "It would be nice if" without concrete reasoning — only flag things that hurt correctness, maintainability, or performance

## Output Format

Provide your review as a structured comment:

```
## PR Review Summary
- **Overall**: [Approve / Request Changes / Comment]
- **Changes Reviewed**: [Brief description of what you examined]

## Issues Found

### 🔴 Critical (Must Fix)
- [File:line]: [Issue description] → [Suggested fix]

### 🟡 Concerns (Should Address)
- [File:line]: [Issue description] → [Suggestion]

### 💡 Suggestions
- [Point]: [Improvement idea]

## Positive Notes
- [What was done well]
```
