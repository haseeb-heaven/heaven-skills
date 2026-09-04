# Heaven Skills 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-63-brightgreen)](#available-skills)
[![First Party](https://img.shields.io/badge/First%20Party-8-lightblue)](#first-party-skills)
[![Third Party](https://img.shields.io/badge/Third%20Party-55-orange)](#third-party-skills)
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
npx skills add haseeb-heaven/heaven-skills/first-party/smart-pr-pipeline
npx skills add haseeb-heaven/heaven-skills/first-party/self-healing-agents
npx skills add haseeb-heaven/heaven-skills/first-party/telegram/telegram-two-way

# Third-party: AWS
npx skills add haseeb-heaven/heaven-skills/third-party/aws/aws-cdk

# Third-party: engineering (mattpocock/skills)
npx skills add haseeb-heaven/heaven-skills/third-party/engineering/tdd

# Third-party: superpowers (obra/superpowers)
npx skills add haseeb-heaven/heaven-skills/third-party/superpowers/writing-plans

# Third-party: agent-skills (addyosmani/agent-skills)
npx skills add haseeb-heaven/heaven-skills/third-party/agent-skills/code-review-and-quality
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
│   ├── implementor/          Structured implementation workflow
│   ├── smart-pr-pipeline/    Guarded PR review, fix, validation, and CI loop
│   ├── self-healing-agents/  Bounded recovery for reliable AI agent workflows
│   └── telegram/             3 Telegram bot skills (send, two-way, chat-id)
│
└── third-party/              ⬅  Curated community & vendor skills
    ├── aws/                  3 AWS skills (CDK, deployment, observability)
    ├── engineering/          8 skills from mattpocock/skills
    ├── superpowers/          11 skills from obra/superpowers
    ├── agent-skills/         23 skills from addyosmani/agent-skills
    └── utilities/            10 general utility skills
```

## Available Skills

### First-Party Skills (8)

Custom-built skills authored by **haseeb-heaven**.

#### Core (5)

| Skill | Description | Install |
|-------|-------------|---------|
| [**greploop**](first-party/greploop/SKILL.md) | The grep → fix → re-grep loop for fixing repeated code issues at scale. Find every occurrence, fix them all, verify zero remain | `npx skills add haseeb-heaven/heaven-skills/first-party/greploop` |
| [**pr-review**](first-party/pr-review/SKILL.md) | AI-powered pull request review — analyzes diffs, identifies bugs, suggests improvements with severity levels | `npx skills add haseeb-heaven/heaven-skills/first-party/pr-review` |
| [**implementor**](first-party/implementor/SKILL.md) | Structured implementation workflow — breaks down requirements, writes clean code, validates with tests | `npx skills add haseeb-heaven/heaven-skills/first-party/implementor` |
| [**smart-pr-pipeline**](first-party/smart-pr-pipeline/SKILL.md) | Guarded PR review pipeline — coordinates review, fixes, tests, lint, CI, re-review, and human merge handoff without automatic merging | `npx skills add haseeb-heaven/heaven-skills/first-party/smart-pr-pipeline` |
| [**self-healing-agents**](first-party/self-healing-agents/SKILL.md) | Bounded recovery for reliable AI agent workflows — verifies steps, classifies failures, uses safe retries and fallbacks, decomposes repeated failures, and stops before risky actions | `npx skills add haseeb-heaven/heaven-skills/first-party/self-healing-agents` |

#### Telegram (3)

Telegram Bot API skills for one-way notifications, two-way interactive bots, and credential/ID lookup.

| Skill | Description | Install |
|-------|-------------|---------|
| [**telegram-send-message**](first-party/telegram/telegram-send-message/SKILL.md) | One-way — send message updates from a bot via curl (`sendMessage`), formatting, rate limits | `npx skills add haseeb-heaven/heaven-skills/first-party/telegram/telegram-send-message` |
| [**telegram-two-way**](first-party/telegram/telegram-two-way/SKILL.md) | Two-way — interactive bot: receive messages (`getUpdates`/webhooks) and reply, buttons, conversation state | `npx skills add haseeb-heaven/heaven-skills/first-party/telegram/telegram-two-way` |
| [**telegram-get-chat-id**](first-party/telegram/telegram-get-chat-id/SKILL.md) | Get the bot API key (BotFather) and read user/group/channel chat IDs via `getUpdates` | `npx skills add haseeb-heaven/heaven-skills/first-party/telegram/telegram-get-chat-id` |

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

### Third-Party Skills: Superpowers (11)

Curated from [**obra/superpowers**](https://github.com/obra/superpowers) — Jesse Vincent's "superpowers" skill collection for AI agents.

| Skill | Description | Install |
|-------|-------------|---------|
| [**brainstorming**](third-party/superpowers/brainstorming/SKILL.md) | Mandatory pre-work before any creative work — explores user intent, requirements, and constraints | `.../third-party/superpowers/brainstorming` |
| [**dispatching-parallel-agents**](third-party/superpowers/dispatching-parallel-agents/SKILL.md) | Delegate 2+ independent tasks to parallel subagents without shared state | `.../third-party/superpowers/dispatching-parallel-agents` |
| [**executing-plans**](third-party/superpowers/executing-plans/SKILL.md) | Execute a written implementation plan in a separate session with review checkpoints | `.../third-party/superpowers/executing-plans` |
| [**finishing-a-development-branch**](third-party/superpowers/finishing-a-development-branch/SKILL.md) | Decide how to integrate completed work — rebase, merge, or squash strategies | `.../third-party/superpowers/finishing-a-development-branch` |
| [**receiving-code-review**](third-party/superpowers/receiving-code-review/SKILL.md) | Handle review feedback with technical rigor — evaluate before implementing suggestions | `.../third-party/superpowers/receiving-code-review` |
| [**subagent-driven-development**](third-party/superpowers/subagent-driven-development/SKILL.md) | Execute plans by dispatching fresh implementer subagents per task | `.../third-party/superpowers/subagent-driven-development` |
| [**using-git-worktrees**](third-party/superpowers/using-git-worktrees/SKILL.md) | Isolated feature work via native git worktrees before executing plans | `.../third-party/superpowers/using-git-worktrees` |
| [**using-superpowers**](third-party/superpowers/using-superpowers/SKILL.md) | Meta-skill — how to find and invoke skills before any response | `.../third-party/superpowers/using-superpowers` |
| [**verification-before-completion**](third-party/superpowers/verification-before-completion/SKILL.md) | Run verification commands and confirm output before claiming work is complete | `.../third-party/superpowers/verification-before-completion` |
| [**writing-plans**](third-party/superpowers/writing-plans/SKILL.md) | Write comprehensive implementation plans before touching code | `.../third-party/superpowers/writing-plans` |
| [**writing-skills**](third-party/superpowers/writing-skills/SKILL.md) | Create, edit, and verify agent skills — TDD for skills | `.../third-party/superpowers/writing-skills` |

### Third-Party Skills: Agent Skills (23)

Curated from [**addyosmani/agent-skills**](https://github.com/addyosmani/agent-skills) — Addy Osmani's production-grade engineering skills.

| Skill | Description | Install |
|-------|-------------|---------|
| [**api-and-interface-design**](third-party/agent-skills/api-and-interface-design/SKILL.md) | Stable API & interface design — REST/GraphQL endpoints, type contracts, module boundaries | `.../third-party/agent-skills/api-and-interface-design` |
| [**browser-testing-with-devtools**](third-party/agent-skills/browser-testing-with-devtools/SKILL.md) | Test in real browsers via Chrome DevTools — DOM inspection, console errors, network | `.../third-party/agent-skills/browser-testing-with-devtools` |
| [**ci-cd-and-automation**](third-party/agent-skills/ci-cd-and-automation/SKILL.md) | Automate CI/CD pipelines — quality gates, test runners, deployment automation | `.../third-party/agent-skills/ci-cd-and-automation` |
| [**code-review-and-quality**](third-party/agent-skills/code-review-and-quality/SKILL.md) | Multi-axis code review before merging — quality, security, performance, maintainability | `.../third-party/agent-skills/code-review-and-quality` |
| [**code-simplification**](third-party/agent-skills/code-simplification/SKILL.md) | Simplify code for clarity without changing behavior — Chesterton's Fence, Rule of 500 | `.../third-party/agent-skills/code-simplification` |
| [**context-engineering**](third-party/agent-skills/context-engineering/SKILL.md) | Optimize agent context setup — rules files, session hygiene, output quality | `.../third-party/agent-skills/context-engineering` |
| [**debugging-and-error-recovery**](third-party/agent-skills/debugging-and-error-recovery/SKILL.md) | Systematic root-cause debugging — failing tests, broken builds, unexpected errors | `.../third-party/agent-skills/debugging-and-error-recovery` |
| [**deprecation-and-migration**](third-party/agent-skills/deprecation-and-migration/SKILL.md) | Manage deprecation & migration — removing old systems, migrating users | `.../third-party/agent-skills/deprecation-and-migration` |
| [**documentation-and-adrs**](third-party/agent-skills/documentation-and-adrs/SKILL.md) | Record architectural decisions (ADRs) and documentation for future engineers | `.../third-party/agent-skills/documentation-and-adrs` |
| [**doubt-driven-development**](third-party/agent-skills/doubt-driven-development/SKILL.md) | Adversarial fresh-context review of every non-trivial decision before it stands | `.../third-party/agent-skills/doubt-driven-development` |
| [**frontend-ui-engineering**](third-party/agent-skills/frontend-ui-engineering/SKILL.md) | Production-quality, accessible, responsive user-facing UIs | `.../third-party/agent-skills/frontend-ui-engineering` |
| [**git-workflow-and-versioning**](third-party/agent-skills/git-workflow-and-versioning/SKILL.md) | Structured git workflow — committing, branching, conflicts, multi-branch work | `.../third-party/agent-skills/git-workflow-and-versioning` |
| [**idea-refine**](third-party/agent-skills/idea-refine/SKILL.md) | Refine raw ideas into sharp, actionable concepts via divergent/convergent thinking | `.../third-party/agent-skills/idea-refine` |
| [**incremental-implementation**](third-party/agent-skills/incremental-implementation/SKILL.md) | Deliver changes incrementally — never write large code drops at once | `.../third-party/agent-skills/incremental-implementation` |
| [**interview-me**](third-party/agent-skills/interview-me/SKILL.md) | One-question-at-a-time interview to extract what the user actually wants | `.../third-party/agent-skills/interview-me` |
| [**observability-and-instrumentation**](third-party/agent-skills/observability-and-instrumentation/SKILL.md) | Logging, metrics, tracing, alerting — make production behavior visible | `.../third-party/agent-skills/observability-and-instrumentation` |
| [**performance-optimization**](third-party/agent-skills/performance-optimization/SKILL.md) | Optimize performance across frontend, backend, queries, and databases | `.../third-party/agent-skills/performance-optimization` |
| [**planning-and-task-breakdown**](third-party/agent-skills/planning-and-task-breakdown/SKILL.md) | Break specs into ordered, implementable tasks | `.../third-party/agent-skills/planning-and-task-breakdown` |
| [**security-and-hardening**](third-party/agent-skills/security-and-hardening/SKILL.md) | Harden code against vulnerabilities — user input, auth, storage, integrations | `.../third-party/agent-skills/security-and-hardening` |
| [**shipping-and-launch**](third-party/agent-skills/shipping-and-launch/SKILL.md) | Production launch prep — pre-launch checklist, monitoring, staged rollout | `.../third-party/agent-skills/shipping-and-launch` |
| [**source-driven-development**](third-party/agent-skills/source-driven-development/SKILL.md) | Ground every implementation decision in official, source-cited documentation | `.../third-party/agent-skills/source-driven-development` |
| [**spec-driven-development**](third-party/agent-skills/spec-driven-development/SKILL.md) | Create specs before coding — new projects, features, ambiguous requirements | `.../third-party/agent-skills/spec-driven-development` |
| [**using-agent-skills**](third-party/agent-skills/using-agent-skills/SKILL.md) | Meta-skill — discover which skill applies to the current task | `.../third-party/agent-skills/using-agent-skills` |

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
| [obra/superpowers](https://github.com/obra/superpowers) | Jesse Vincent's agent superpowers collection | superpowers/* (brainstorming, writing-plans, subagent-driven-development, etc.) |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | Production-grade engineering skills by Addy Osmani | agent-skills/* (code-review-and-quality, security-and-hardening, spec-driven-development, etc.) |
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
