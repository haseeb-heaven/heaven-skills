# Contributing to Heaven Skills

Thank you for your interest in contributing! All contributions are welcome — whether it's adding new skills, improving existing ones, or fixing documentation.

## How Skills Work

Skills are markdown instruction sets that AI coding agents (Command Code, Claude Code, Cline, etc.) can load to gain domain expertise. Each skill lives in its own folder with a `SKILL.md` file following the [skills.sh format](https://www.skills.sh).

## Adding a New Skill

### 1. Choose the Right Category

```
heaven-skills/
├── first-party/        → Skills YOU created
└── third-party/        → Skills from other sources (organized by topic)
    ├── aws/            → AWS ecosystem skills
    ├── engineering/    → Engineering workflow skills
    └── utilities/      → General utility skills
```

### 2. Create the Structure

```bash
mkdir -p third-party/[category]/[skill-name]
```

### 3. Write SKILL.md

Every skill needs this minimum structure:

```markdown
---
name: skill-name
description: >-
  Clear one-liner describing what the skill does and when to use it.
version: 1
---

# Skill Title

## When to Use
When the user needs help with...

## When NOT to Use
Avoid using for...

## Instructions / Workflow
Step-by-step guidance the AI should follow.

## References (optional)
Links to additional docs or related skills.

**Author:** [Your name or org]
```

### 4. Test Locally

```bash
npx skills add ./third-party/[category]/[skill-name]
```

### 5. Submit Your Changes

```bash
git add .
git commit -m "feat(skill): add [skill-name]"
git push
```

## Conventions

### SKILL.md Format
- YAML frontmatter is **required** (`name`, `description`, `version`)
- Use `>-` for multi-line descriptions to fold them into one line
- Version starts at `1` and increments only on breaking changes
- Include a **Author** attribution line at the bottom

### Commit Messages
Follow [Conventional Commits](https://www.conventionalcommits.org/):

| Type | Description | Example |
|------|-------------|---------|
| `feat(skill):` | Add new skill | `feat(skill): add aws-s3-helper` |
| `fix(skill):` | Fix issues in a skill | `fix(skill): correct lambda timeout` |
| `docs:` | Documentation changes | `docs: update README badges` |
| `chore:` | Maintenance | `chore: bump version numbers` |
| `refactor(skill):` | Improve without changing behavior | `refactor(skill): restructure tdd` |

### Quality Checklist

Before submitting:
- [ ] SKILL.md has valid YAML frontmatter
- [ ] Description explains WHAT the skill does and WHEN to use it
- [ ] Contains practical instructions, not just theory
- [ ] No hardcoded secrets, API keys, or sensitive data
- [ ] Follows existing naming conventions
- [ ] Tested locally with `npx skills add`
- [ ] Added to README.md if new category/skill

## Attribution

When including third-party skills, always attribute the original author in the SKILL.md footer:

```markdown
**Source:** [author-or-org/repo](https://github.com/author-or-org/repo) — short description
```

### Recommended Third-Party Sources

Prefer skills from these battle-tested, community-verified repositories:

| Source | What It Contains |
|--------|------------------|
| [mattpocock/skills](https://github.com/mattpocock/skills) | Engineering skills — tdd, code-review, research, prototype, diagnosing-bugs, etc. |
| [kunchenguid/no-mistakes](https://github.com/kunchenguid/no-mistakes) | `no-mistakes` — git push quality gate for clean PRs |
| [skills.sh](https://www.skills.sh) | Search engine for discovering more skills to curate |

If you're unsure of the original author, use `Unknown` rather than omitting attribution.

## Questions?

Open an issue on GitHub if you have questions about contributing. Be as specific as possible about what you'd like to do.
