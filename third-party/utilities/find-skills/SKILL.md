---
name: find-skills
description: >-
  Helps users discover and browse available community skills. Searches skill registries,
  filters by category and use case, compares feature sets, and recommends the best
  skill for a given task. Use when looking for new capabilities or comparing options.
version: 1
---

# Find Skills

Helps users discover, find, compare, and install community-built skills for AI coding agents.

## When NOT to Use

- Building custom skills from scratch — use the skill-builder instead
- Reviewing installed skills — list what's already configured separately
- Managing skill permissions — handled at the agent configuration level

## Discovery Workflow

### Step 1: Identify the Need
What capability are you looking for? Examples:
- "I need skills for working with databases"
- "Looking for CI/CD deployment skills"
- "Want skills for testing React components"

### Step 2: Search Sources
| Source | URL | What It Has |
|--------|-----|-------------|
| **skills.sh** | skills.sh | Community leaderboard with install counts |
| **npm registry** | npmjs.com/search?q=@anthropic/skill | Official SDK packages |
| **GitHub** | github.com/topics/ai-skill | Open source skill repositories |
| **Agent marketplaces** | Per-agent marketplace pages | Platform-specific skills |

### Step 3: Evaluate Options
For each candidate skill, check:
- **Install count** on skills.sh — more installs = more community validation
- **Last updated** — active maintenance matters
- **Author reputation** — known security/infra orgs are safer than anonymous
- **Skill contents** — read SKILL.md before installing to understand scope
- **Dependencies** — does it require additional tools or APIs?

### Step 4: Install
```bash
# From skills.sh registry
npx skills add [author]/[repo]/[skill-path]

# From GitHub directly
npx skills add https://github.com/[user]/[repo]/[path/to/skill]

# From local file
npx skills add ./local-skill-folder
```

## Comparison Framework

When choosing between similar skills, score each on:

| Criteria | Weight | Question |
|----------|--------|----------|
| Coverage | 30% | Does it handle all my use cases? |
| Active Maintenance | 25% | Updated in last 90 days? |
| Security | 20% | No shell commands on untrusted data? |
| Ease of Use | 15% | Simple install, clear docs? |
| Community | 10% | Star count, issues being answered |

## Output Format

```markdown
## Skill Recommendations for [Need]

### Best Match
**[Skill Name]** by [Author]
- Installs: [count]
- Last updated: [date]
- Link: [URL]
- Pros: [bullet points]
- Cons: [bullet points]

### Alternatives
| Skill | Author | Key Difference |
|-------|--------|---------------|
| [Name] | [Author] | [How it differs] |

### Install Command
[npx skills add command here]
```
