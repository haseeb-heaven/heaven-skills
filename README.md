# Heaven Skills 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-24-brightgreen)](#available-skills)
[![First Party](https://img.shields.io/badge/First%20Party-3-lightblue)](#first-party-skills)
[![Third Party](https://img.shields.io/badge/Third%20Party-21-orange)](#third-party-skills)
[![skills.sh](https://skills.sh/b/haseeb-heaven/heaven-skills)](https://www.skills.sh)
[![Command Code](https://img.shields.io/badge/Command%20Code-Compatible-6b46c1)](https://www.commandcode.ai)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-000?logo=anthropic)](https://docs.anthropic.com/en/docs/claude-code/skills)
[![Cline](https://img.shields.io/badge/Cline-Compatible-000?logo=sublimetext)](https://github.com/cline/cline)

Curated collection of AI agent skills for Command Code, Claude Code, Cline, OpenCode, and more. Organized into **first-party** (custom-built by haseeb-heaven) and **third-party** (curated from trusted community sources).

Search all skills on [skills.sh](https://www.skills.sh) — the skill search engine for AI coding agents.

## Quick Install

Install any skill via npm:

```bash
npx skills add haseeb-heaven/heaven-skills/[category]/[skill-name]
```

Examples:
```bash
# First-party: custom skills
npx skills add haseeb-heaven/heaven-skills/first-party/greploop
npx skills add haseeb-heaven/heaven-skills/first-party/pr-review

# Third-party: AWS
npx skills add haseeb-heaven/heaven-skills/third-party/aws/aws-cdk

# Third-party: engineering (mattpocock/skills)
npx skills add haseeb-heaven/heaven-skills/third-party/engineering/tdd
```

## Directory Structure

```
heaven-skills/
├── README.md                 # You are here
├── LICENSE                   # MIT License
├── CONTRIBUTING.md           # How to contribute
├── CODE_OF_CONDUCT.md        # Community guidelines
│
├── first-party/              ⬅  Skills built by haseeb-heaven
│   ├── greploop/             Grep → fix → re-grep verification loop
│   ├── pr-review/            AI-powered PR review with severity classification
│   └── implementor/          Structured implementation workflow
│
└── third-party/              ⬅  Curated community & vendor skills
    ├── aws/                  3 AWS skills (CDK, deployment, observability)
    ├── engineering/          8 skills from mattpocock/skills
    └── utilities/            10 general utility skills
```

## Available Skills

### First-Party Skills (3)

Custom-built skills authored by **haseeb-heaven**.

| Skill | Description | Install |
|-------|-------------|---------|
| [**greploop**](first-party/greploop/SKILL.md) | The grep → fix → re-grep loop for fixing repeated code issues at scale. Find every occurrence, fix them all, verify zero remain | `npx skills add haseeb-heaven/heaven-skills/first-party/greploop` |
| [**pr-review**](first-party/pr-review/SKILL.md) | AI-powered pull request review — analyzes diffs, identifies bugs, suggests improvements with severity levels | `npx skills add haseeb-heaven/heaven-skills/first-party/pr-review` |
| [**implementor**](first-party/implementor/SKILL.md) | Structured implementation workflow — breaks down requirements, writes clean code, validates with tests | `npx skills add haseeb-heaven/heaven-skills/first-party/implementor` |

### Third-Party Skills: AWS (3)

Official skills maintained by **Amazon Web Services** — infrastructure management, production deployment, and usage monitoring.

| Skill | Description | Install |
|-------|-------------|---------|
| [**aws-cdk**](third-party/aws/aws-cdk/SKILL.md) | Managing — author, deploy & troubleshoot CDK stacks (TypeScript/Python), construct patterns, safe refactoring | `npx skills add haseeb-heaven/heaven-skills/third-party/aws/aws-cdk` |
| [**aws-deployment**](third-party/aws/aws-deployment/SKILL.md) | Push to Prod — CI/CD pipelines (CodePipeline, CodeBuild, CodeDeploy, CodeArtifact), blue/green & canary strategies | `npx skills add haseeb-heaven/heaven-skills/third-party/aws/aws-deployment` |
| [**aws-observability**](third-party/aws/aws-observability/SKILL.md) | Usage check — CloudWatch, X-Ray, Application Signals, dashboards, alarms, log insights | `npx skills add haseeb-heaven/heaven-skills/third-party/aws/aws-observability` |

### Third-Party Skills: Engineering (8)

Curated from [**mattpocock/skills**](https://github.com/mattpocock/skills) — "Skills for Real Engineers" (203k ⭐).

| Skill | Description | Install |
|-------|-------------|---------|
| [**code-review**](third-party/engineering/code-review/SKILL.md) | Review diffs since last commit — bugs, style, security, performance | `.../third-party/engineering/code-review` |
| [**codebase-design**](third-party/engineering/codebase-design/SKILL.md) | Shared vocabulary for architecture discussions (modules, boundaries, coupling) | `.../third-party/engineering/codebase-design` |
| [**diagnosing-bugs**](third-party/engineering/diagnosing-bugs/SKILL.md) | Systematic root cause analysis — binary search, hypothesis testing, isolation | `.../third-party/engineering/diagnosing-bugs` |
| [**domain-modeling**](third-party/engineering/domain-modeling/SKILL.md) | Extract entities, value objects, aggregates from business requirements | `.../third-party/engineering/domain-modeling` |
| [**prototype**](third-party/engineering/prototype/SKILL.md) | Build throwaway prototypes fast to validate ideas and reduce risk | `.../third-party/engineering/prototype` |
| [**research**](third-party/engineering/research/SKILL.md) | Systematic technical research with evidence-based recommendations | `.../third-party/engineering/research` |
| [**resolving-merge-conflicts**](third-party/engineering/resolving-merge-conflicts/SKILL.md) | Systematic merge conflict resolution preserving intent from both branches | `.../third-party/engineering/resolving-merge-conflicts` |
| [**tdd**](third-party/engineering/tdd/SKILL.md) | Test-driven development — red/green/refactor loop with anti-pattern detection | `.../third-party/engineering/tdd` |

### Third-Party Skills: Utilities (10)

General-purpose tools and helper skills.

| Skill | Description | Install |
|-------|-------------|---------|
| [**no-mistakes**](third-party/utilities/no-mistakes/SKILL.md) | Git push quality gate — from [**kunchenguid/no-mistakes**](https://github.com/kunchenguid/no-mistakes) (7.4k ⭐). Validates code before it reaches a clean PR | `.../third-party/utilities/no-mistakes` |
| [**find-skills**](third-party/utilities/find-skills/SKILL.md) | Discover and compare available community skills | `.../third-party/utilities/find-skills` |
| [**loopy**](third-party/utilities/loopy/SKILL.md) | Loopy conversational bot automation & workflows | `.../third-party/utilities/loopy` |
| [**git-guardrails-claude-code**](third-party/utilities/git-guardrails-claude-code/SKILL.md) | Set up Claude Code git hooks & quality guardrails | `.../third-party/utilities/git-guardrails-claude-code` |
| [**migrate-to-shoehorn**](third-party/utilities/migrate-to-shoehorn/SKILL.md) | Migrate test files between frameworks & formats | `.../third-party/utilities/migrate-to-shoehorn` |
| [**scaffold-exercises**](third-party/utilities/scaffold-exercises/SKILL.md) | Generate exercise boilerplate for coding challenges & tutorials | `.../third-party/utilities/scaffold-exercises` |
| [**setup-pre-commit**](third-party/utilities/setup-pre-commit/SKILL.md) | Configure Husky pre-commit hooks for linting, formatting, testing | `.../third-party/utilities/setup-pre-commit` |
| [**opentui**](third-party/utilities/opentui/SKILL.md) | Build terminal UIs with OpenTUI (Rust TUI framework) | `.../third-party/utilities/opentui` |
| [**obsidian-vault**](third-party/utilities/obsidian-vault/SKILL.md) | Search, create & manage Obsidian vault notes programmatically | `.../third-party/utilities/obsidian-vault` |
| [**grilling**](third-party/utilities/grilling/SKILL.md) | Relentlessly clarify ambiguous requirements before implementation | `.../third-party/utilities/grilling` |

## Curated Sources

This collection pulls recommended third-party skills from trusted, battle-tested sources:

| Source | Repo | Skills Included |
|--------|------|-----------------|
| [mattpocock/skills](https://github.com/mattpocock/skills) | "Skills for Real Engineers" — 203k ⭐ | engineering/* (code-review, tdd, research, prototype, etc.) |
| [kunchenguid/no-mistakes](https://github.com/kunchenguid/no-mistakes) | "git push no-mistakes" — 7.4k ⭐ | utilities/no-mistakes |
| Amazon Web Services | Official AWS agent skills | aws/* (cdk, deployment, observability) |
| [skills.sh](https://www.skills.sh) | The search engine for AI skills | Everything is installable via `npx skills add` |

## Supported Agents

These skills work across multiple AI coding agents. Install once, use everywhere.

| Agent | Status | Notes |
|-------|--------|-------|
| [Command Code](https://www.commandcode.ai) | ✅ Fully compatible | Native skill system — install via `npx skills add` |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code/skills) | ✅ Compatible | Skills stored in `~/.claude/skills/` |
| [Cline](https://github.com/cline/cline) | ✅ Compatible | Skills supported via `.cline/skills/` |
| [OpenCode](https://opencode.ai) | ✅ Compatible | Plugin-based — most skills work as plugins |
| [Hermes Agent](https://github.com/hermes-agent) | ✅ Compatible | Skill directory + headroom plugin integration |

## SKILL.md Format

Every skill follows the [skills.sh](https://www.skills.sh) convention:

```markdown
---
name: skill-name
description: >-
  Clear description of what the skill does and when to use it.
version: 1
---

# Skill Title

Detailed instructions, warnings, workflows, and references...

**Source:** [Author or upstream repo](link)
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full contribution guide.

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for details on adding new skills or improving existing ones.

Please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before participating.

## License

[MIT](LICENSE) — Free to use, modify, and distribute.

---

Built and maintained by **[haseeb-heaven](https://github.com/haseeb-heaven)**.
