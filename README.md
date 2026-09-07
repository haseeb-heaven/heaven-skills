<div align="center">

![Heaven Skills banner](https://capsule-render.vercel.app/api?type=waving&color=0:6D28D9,50:2563EB,100:06B6D4&height=230&section=header&text=Heaven%20Skills&fontSize=58&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=Reusable%20skills%20for%20modern%20AI%20coding%20agents&descAlignY=57&descSize=18)

# Heaven Skills

### A practical, curated skill library for agents that plan, build, review, debug, and ship software.

[![Skills](https://img.shields.io/badge/skills-69-22c55e?style=for-the-badge&logo=files&logoColor=white)](#-skill-catalog)
[![First Party](https://img.shields.io/badge/first--party-10-3b82f6?style=for-the-badge&logo=github&logoColor=white)](#-first-party-skills)
[![Curated](https://img.shields.io/badge/curated-59-f97316?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](#-curated-community-skills)
[![License](https://img.shields.io/badge/license-MIT-8b5cf6?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](LICENSE)

[![skills.sh](https://skills.sh/b/haseeb-heaven/heaven-skills)](https://skills.sh/haseeb-heaven/heaven-skills)

[**⚡ Quick start**](#-quick-start) · [**🧭 Browse skills**](#-skill-catalog) · [**🌐 Explore skills.sh**](https://skills.sh) · [**🤝 Contribute**](CONTRIBUTING.md)

</div>

---

## ✨ Why Heaven Skills?

Heaven Skills gives AI coding agents focused, reusable operating procedures instead of one-off prompts. Install the collection once, then invoke the right workflow for architecture, implementation, testing, security, code review, deployment, browser verification, or agent recovery.

<table>
<tr>
<td width="33%" align="center"><h3>🧠 10 Originals</h3><p>Purpose-built workflows authored and maintained by <a href="https://github.com/haseeb-heaven">haseeb-heaven</a>.</p></td>
<td width="33%" align="center"><h3>🌍 59 Curated</h3><p>Useful community and vendor skills organized behind one consistent catalog.</p></td>
<td width="33%" align="center"><h3>🤖 Multi-Agent</h3><p>Portable <code>SKILL.md</code> packages for the major AI coding-agent ecosystems.</p></td>
</tr>
</table>

> [!TIP]
> New here? Start with **`greploop`** for repeated fixes, **`self-healing-agents`** for resilient automation, or **`smart-pr-pipeline`** for guarded delivery.

## ⚡ Quick Start

### Install the collection

```bash
npx skills add haseeb-heaven/heaven-skills
```

### Install one skill

```bash
npx skills add haseeb-heaven/heaven-skills --skill greploop
npx skills add haseeb-heaven/heaven-skills --skill self-healing-agents
npx skills add haseeb-heaven/heaven-skills --skill smart-pr-pipeline
```

### Use a skill

```text
$greploop fix every outdated API call in this repository
$self-healing-agents make this workflow recover safely from transient failures
$smart-pr-pipeline review, validate, and prepare this branch for a human merge
```

<details>
<summary><strong>📁 Manual installation</strong></summary>

Copy a skill directory into the location recognized by your agent:

```text
.agents/skills/      # Universal project location
~/.codex/skills/     # Codex user skills
~/.claude/skills/    # Claude Code user skills
.cline/skills/       # Cline project skills
```

Restart or reload the agent after installing.

</details>

## 🤖 Agent Compatibility

| Agent | Compatibility | Recommended location |
|---|:---:|---|
| **OpenAI Codex** | ✅ | `~/.codex/skills/` or `.agents/skills/` |
| **Claude Code** | ✅ | `~/.claude/skills/` or `.claude/skills/` |
| **Cursor** | ✅ | `.cursor/skills/` or `.agents/skills/` |
| **Cline** | ✅ | `.cline/skills/` or `.agents/skills/` |
| **OpenCode** | ✅ | Agent/plugin skill directory |
| **GitHub Copilot** | ✅ | `.github/skills/` or `.agents/skills/` |
| **Gemini CLI** | ✅ | Agent-supported skill directory |
| **Windsurf / Goose / Amp** | ✅ | `.agents/skills/` |

> [!NOTE]
> Exact discovery paths can vary by agent version. The `npx skills` installer detects supported agents and offers compatible destinations.

## 🧭 Skill Catalog

### 🧠 First-Party Skills

Original workflows authored for Heaven Skills.

<details open>
<summary><strong>⭐ Core workflows — 7 skills</strong></summary>

| Icon | Skill | What it gives your agent |
|:---:|---|---|
| 🌌 | [**gpt-6-astra-guide**](first-party/gpt-6-astra-guide/SKILL.md) | Apply current GPT-6 Astra API migration, prompting, autonomy, and verification guidance. |
| 🔁 | [**greploop**](first-party/greploop/SKILL.md) | Find every occurrence, fix the complete set, and re-grep until zero matches remain. |
| 🛠️ | [**implementor**](first-party/implementor/SKILL.md) | Turn requirements into scoped implementation work with validation and clean handoff. |
| 🔎 | [**pr-review**](first-party/pr-review/SKILL.md) | Review pull-request changes and report actionable, severity-ranked findings. |
| 🧪 | [**production-pr-review**](first-party/production-pr-review/SKILL.md) | Inspect production-facing changes for correctness, regression risk, security, and operability. |
| ♻️ | [**self-healing-agents**](first-party/self-healing-agents/SKILL.md) | Classify failures, retry safely, switch tactics, decompose repeated failures, and stop before risky actions. |
| 🚦 | [**smart-pr-pipeline**](first-party/smart-pr-pipeline/SKILL.md) | Coordinate review, fixes, tests, lint, CI, re-review, and a human-controlled merge handoff. |

</details>

<details open>
<summary><strong>✈️ Telegram automation — 3 skills</strong></summary>

| Icon | Skill | What it gives your agent |
|:---:|---|---|
| 🪪 | [**telegram-get-chat-id**](first-party/telegram/telegram-get-chat-id/SKILL.md) | Obtain bot credentials safely and resolve user, group, or channel chat IDs. |
| 📤 | [**telegram-send-message**](first-party/telegram/telegram-send-message/SKILL.md) | Send formatted one-way Telegram notifications through the Bot API. |
| 💬 | [**telegram-two-way**](first-party/telegram/telegram-two-way/SKILL.md) | Build interactive bots using updates or webhooks, buttons, replies, and conversation state. |

</details>

### 🌍 Curated Community Skills

These are organized snapshots or adaptations from respected community and vendor projects. Use the **local** link to inspect the version in this repository and the **source** link to follow upstream development.

<details>
<summary><strong>🏗️ Production engineering — Addy Osmani · 23 skills</strong></summary>

**Source:** [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) · [Browse on skills.sh](https://skills.sh/addyosmani/agent-skills)

| Skill | Focus |
|---|---|
| [api-and-interface-design](third-party/agent-skills/api-and-interface-design/SKILL.md) | Stable APIs, contracts, endpoints, and module boundaries |
| [browser-testing-with-devtools](third-party/agent-skills/browser-testing-with-devtools/SKILL.md) | Runtime browser inspection, console, DOM, and network validation |
| [ci-cd-and-automation](third-party/agent-skills/ci-cd-and-automation/SKILL.md) | Pipelines, quality gates, test runners, and deployment automation |
| [code-review-and-quality](third-party/agent-skills/code-review-and-quality/SKILL.md) | Correctness, security, performance, and maintainability review |
| [code-simplification](third-party/agent-skills/code-simplification/SKILL.md) | Reduce unnecessary complexity without changing behavior |
| [context-engineering](third-party/agent-skills/context-engineering/SKILL.md) | Rules files, session context, and reliable agent behavior |
| [debugging-and-error-recovery](third-party/agent-skills/debugging-and-error-recovery/SKILL.md) | Evidence-driven root-cause debugging and recovery |
| [deprecation-and-migration](third-party/agent-skills/deprecation-and-migration/SKILL.md) | Safe replacement and removal of old systems |
| [documentation-and-adrs](third-party/agent-skills/documentation-and-adrs/SKILL.md) | Durable documentation and architectural decisions |
| [doubt-driven-development](third-party/agent-skills/doubt-driven-development/SKILL.md) | Adversarial review of non-trivial decisions |
| [frontend-ui-engineering](third-party/agent-skills/frontend-ui-engineering/SKILL.md) | Accessible, responsive, production-quality UI engineering |
| [git-workflow-and-versioning](third-party/agent-skills/git-workflow-and-versioning/SKILL.md) | Branching, commits, conflicts, and versioning discipline |
| [idea-refine](third-party/agent-skills/idea-refine/SKILL.md) | Turn raw ideas into sharp, actionable concepts |
| [incremental-implementation](third-party/agent-skills/incremental-implementation/SKILL.md) | Deliver small, verifiable changes instead of large code drops |
| [interview-me](third-party/agent-skills/interview-me/SKILL.md) | Extract requirements through one focused question at a time |
| [observability-and-instrumentation](third-party/agent-skills/observability-and-instrumentation/SKILL.md) | Logs, metrics, traces, alerting, and production visibility |
| [performance-optimization](third-party/agent-skills/performance-optimization/SKILL.md) | Measure and improve frontend, backend, query, and database performance |
| [planning-and-task-breakdown](third-party/agent-skills/planning-and-task-breakdown/SKILL.md) | Convert specifications into ordered implementation tasks |
| [security-and-hardening](third-party/agent-skills/security-and-hardening/SKILL.md) | Threat modeling and application hardening |
| [shipping-and-launch](third-party/agent-skills/shipping-and-launch/SKILL.md) | Pre-launch checks, monitoring, staging, and rollout |
| [source-driven-development](third-party/agent-skills/source-driven-development/SKILL.md) | Ground implementation decisions in authoritative documentation |
| [spec-driven-development](third-party/agent-skills/spec-driven-development/SKILL.md) | Define expected behavior before implementation |
| [using-agent-skills](third-party/agent-skills/using-agent-skills/SKILL.md) | Discover and invoke the right workflow for the task |

</details>

<details>
<summary><strong>⚡ Superpowers · 12 skills</strong></summary>

**Source:** [obra/superpowers](https://github.com/obra/superpowers) · [Browse on skills.sh](https://skills.sh/obra/superpowers)

| Skill | Focus |
|---|---|
| [brainstorming](third-party/superpowers/brainstorming/SKILL.md) | Explore intent and design before creative implementation |
| [dispatching-parallel-agents](third-party/superpowers/dispatching-parallel-agents/SKILL.md) | Delegate independent work safely |
| [executing-plans](third-party/superpowers/executing-plans/SKILL.md) | Execute written plans through review checkpoints |
| [finishing-a-development-branch](third-party/superpowers/finishing-a-development-branch/SKILL.md) | Choose how completed work should be integrated |
| [receiving-code-review](third-party/superpowers/receiving-code-review/SKILL.md) | Evaluate review feedback with technical rigor |
| [requesting-code-review](third-party/superpowers/requesting-code-review/SKILL.md) | Request structured review before integration |
| [subagent-driven-development](third-party/superpowers/subagent-driven-development/SKILL.md) | Execute plans using focused implementer agents |
| [using-git-worktrees](third-party/superpowers/using-git-worktrees/SKILL.md) | Isolate feature work with Git worktrees |
| [using-superpowers](third-party/superpowers/using-superpowers/SKILL.md) | Discover and apply process skills consistently |
| [verification-before-completion](third-party/superpowers/verification-before-completion/SKILL.md) | Require fresh evidence before completion claims |
| [writing-plans](third-party/superpowers/writing-plans/SKILL.md) | Produce detailed, executable implementation plans |
| [writing-skills](third-party/superpowers/writing-skills/SKILL.md) | Create and verify dependable agent skills |

</details>

<details>
<summary><strong>🧱 Engineering discipline — Matt Pocock · 8 skills</strong></summary>

**Source:** [mattpocock/skills](https://github.com/mattpocock/skills) · [Browse on skills.sh](https://skills.sh/mattpocock/skills)

| Skill | Focus |
|---|---|
| [code-review](third-party/engineering/code-review/SKILL.md) | Review changed code for material defects |
| [codebase-design](third-party/engineering/codebase-design/SKILL.md) | Modules, boundaries, coupling, and architecture vocabulary |
| [diagnosing-bugs](third-party/engineering/diagnosing-bugs/SKILL.md) | Hypothesis testing, isolation, and root-cause analysis |
| [domain-modeling](third-party/engineering/domain-modeling/SKILL.md) | Entities, value objects, aggregates, and business rules |
| [prototype](third-party/engineering/prototype/SKILL.md) | Build disposable probes to reduce uncertainty |
| [research](third-party/engineering/research/SKILL.md) | Evidence-based technical investigation |
| [resolving-merge-conflicts](third-party/engineering/resolving-merge-conflicts/SKILL.md) | Preserve intent while resolving conflicts |
| [tdd](third-party/engineering/tdd/SKILL.md) | Red, green, refactor with meaningful tests |

</details>

<details>
<summary><strong>☁️ AWS · 3 official skills</strong></summary>

**Source:** [aws/agent-toolkit-for-aws](https://github.com/aws/agent-toolkit-for-aws) · [Browse on skills.sh](https://skills.sh/aws/agent-toolkit-for-aws)

| Icon | Skill | Focus |
|:---:|---|---|
| 🏛️ | [aws-cdk](third-party/aws/aws-cdk/SKILL.md) | Author, deploy, troubleshoot, and refactor CDK stacks |
| 🚀 | [aws-deployment](third-party/aws/aws-deployment/SKILL.md) | CI/CD, CodePipeline, CodeBuild, blue/green, and canary delivery |
| 📊 | [aws-observability](third-party/aws/aws-observability/SKILL.md) | CloudWatch, X-Ray, Application Signals, dashboards, and alarms |

</details>

<details>
<summary><strong>🧰 Utilities · 10 skills</strong></summary>

| Icon | Skill | Focus | Related source/listing |
|:---:|---|---|---|
| 🧭 | [find-skills](third-party/utilities/find-skills/SKILL.md) | Discover and compare community skills | [vercel-labs/skills](https://github.com/vercel-labs/skills) |
| 🛡️ | [git-guardrails-claude-code](third-party/utilities/git-guardrails-claude-code/SKILL.md) | Git hooks and quality guardrails | [mattpocock/skills](https://github.com/mattpocock/skills) |
| 🔥 | [grilling](third-party/utilities/grilling/SKILL.md) | Expose ambiguous requirements and hidden assumptions | [mattpocock/skills](https://github.com/mattpocock/skills) |
| 🔄 | [loopy](third-party/utilities/loopy/SKILL.md) | Conversational bot and messaging workflows | [skills.sh listing](https://skills.sh/sickn33/agentic-awesome-skills/loopy) |
| 👟 | [migrate-to-shoehorn](third-party/utilities/migrate-to-shoehorn/SKILL.md) | Migrate test structures while preserving behavior | [mattpocock/skills](https://github.com/mattpocock/skills) |
| ✅ | [no-mistakes](third-party/utilities/no-mistakes/SKILL.md) | Pre-merge code-quality validation | [kunchenguid/no-mistakes](https://github.com/kunchenguid/no-mistakes) |
| 💎 | [obsidian-vault](third-party/utilities/obsidian-vault/SKILL.md) | Programmatic Obsidian knowledge management | [mattpocock/skills](https://github.com/mattpocock/skills) |
| 🖥️ | [opentui](third-party/utilities/opentui/SKILL.md) | Build rich terminal user interfaces | [anomalyco/opentui](https://github.com/anomalyco/opentui) |
| 🎓 | [scaffold-exercises](third-party/utilities/scaffold-exercises/SKILL.md) | Generate structured programming exercises | [mattpocock/skills](https://github.com/mattpocock/skills) |
| 🪝 | [setup-pre-commit](third-party/utilities/setup-pre-commit/SKILL.md) | Configure pre-commit lint, format, test, and security checks | [mattpocock/skills](https://github.com/mattpocock/skills) |

</details>

<details>
<summary><strong>🎯 Specialized review skills · 3 skills</strong></summary>

| Icon | Skill | Focus | Upstream |
|:---:|---|---|---|
| 🧹 | [remove-ai-slops](third-party/anti-slop/remove-ai-slops/SKILL.md) | Remove unnecessary agent-generated code while preserving behavior | [code-yeongyu/oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent) |
| ⚛️ | [react-code-review](third-party/developer-kit/react-code-review/SKILL.md) | Review React architecture, hooks, accessibility, and production readiness | [giuseppe-trisciuoglio/developer-kit](https://github.com/giuseppe-trisciuoglio/developer-kit) |
| 🔐 | [security-and-hardening](third-party/zineyu/security-and-hardening/SKILL.md) | Threat-model and harden software trust boundaries | [zineyu/skills](https://github.com/zineyu/skills) |

</details>

## 🗺️ Repository Map

```text
heaven-skills/
├── first-party/                 # 10 original Heaven Skills
│   ├── gpt-6-astra-guide/
│   ├── greploop/
│   ├── implementor/
│   ├── pr-review/
│   ├── production-pr-review/
│   ├── self-healing-agents/
│   ├── smart-pr-pipeline/
│   └── telegram/                # 3 Telegram skills
│
├── third-party/                 # 59 curated community skills
│   ├── agent-skills/            # 23
│   ├── anti-slop/               # 1
│   ├── aws/                     # 3
│   ├── developer-kit/           # 1
│   ├── engineering/             # 8
│   ├── superpowers/             # 12
│   ├── utilities/               # 10
│   └── zineyu/                  # 1
│
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
└── LICENSE
```

## 🧩 Skill Format

Every package is centered on a `SKILL.md` file with YAML metadata and focused operating instructions:

```markdown
---
name: skill-name
description: When and why an agent should use this skill.
---

# Skill Name

Workflow, constraints, safety rules, examples, and verification steps.
```

Optional scripts, references, templates, and assets can live beside the skill file and load only when required.

## 🔍 Discover More

| Directory | Use it for |
|---|---|
| [**skills.sh**](https://skills.sh) | Search the open skill ecosystem, compare adoption, and install skills |
| [**Heaven Skills on skills.sh**](https://skills.sh/haseeb-heaven/heaven-skills) | Open this repository's skills.sh source page |
| [**Agent Skills specification**](https://agentskills.io) | Understand the portable skill format |
| [**GitHub topic search**](https://github.com/topics/agent-skills) | Discover source repositories and community projects |

## 🤝 Contributing

Contributions are welcome. You can improve an existing workflow, propose a focused new skill, correct upstream attribution, or add tested supporting resources.

1. Read [CONTRIBUTING.md](CONTRIBUTING.md).
2. Follow the existing `SKILL.md` structure.
3. Keep instructions scoped, actionable, and safe.
4. Verify every relative link and supporting file.
5. Open a pull request explaining the problem the skill solves.

Please follow the [Code of Conduct](CODE_OF_CONDUCT.md).

## 🔒 Trust and Safety

> [!IMPORTANT]
> Skills are instructions that may influence an agent with access to files, shells, credentials, browsers, or external services. Read a skill before installing it, review bundled scripts, verify its upstream source, and use least-privilege permissions.

Curated skills may be adapted snapshots rather than byte-for-byte mirrors of their upstream versions. Upstream projects remain the source of truth for their current releases, licenses, dependencies, and security guidance.

## 📄 License

Heaven Skills is released under the [MIT License](LICENSE). Third-party material remains subject to its applicable upstream license and attribution requirements.

---

<div align="center">

### Built with care by [Haseeb Heaven](https://github.com/haseeb-heaven)

If this library helps your agents ship better software, consider giving the repository a ⭐.

[![GitHub followers](https://img.shields.io/github/followers/haseeb-heaven?style=social)](https://github.com/haseeb-heaven)
[![GitHub stars](https://img.shields.io/github/stars/haseeb-heaven/heaven-skills?style=social)](https://github.com/haseeb-heaven/heaven-skills/stargazers)

![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:06B6D4,50:2563EB,100:6D28D9&height=120&section=footer)

</div>
