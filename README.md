# Heaven Skills 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-36-brightgreen)](#available-skills)
[![First Party](https://img.shields.io/badge/First%20Party-2-lightblue)](#first-party-skills)
[![Third Party](https://img.shields.io/badge/Third%20Party-34-orange)](#third-party-skills)
[![Command Code](https://img.shields.io/badge/Command%20Code-Compatible-6b46c1)](https://www.commandcode.ai)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-000?logo=anthropic)](https://docs.anthropic.com/en/docs/claude-code/skills)
[![Cline](https://img.shields.io/badge/Cline-Compatible-000?logo=sublimetext)](https://github.com/cline/cline)
[![skills.sh](https://img.shields.io/badge/skills.sh-indexed-f0db4f)](https://www.skills.sh)

Curated collection of AI agent skills for Command Code, Claude Code, Cline, OpenCode, Hermes, and more. Organized into first-party (custom-built) and third-party (community & vendor) categories.

## Quick Install

Install any skill via npm:

```bash
npx skills add haseeb-heaven/heaven-skills/[category]/[skill-name]
```

Example:
```bash
# Install your own pr-review skill
npx skills add haseeb-heaven/heaven-skills/first-party/pr-review

# Install an AWS skill
npx skills add haseeb-heaven/heaven-skills/third-party/aws/aws-cdk

# Install an engineering skill  
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
│   ├── pr-review/            AI-powered PR review with severity classification
│   └── implementor/          Structured implementation workflow
│
└── third-party/              ⬅  Community & vendor skills synced here
    ├── aws/                  16 official AWS skills
    ├── engineering/          8 engineering workflow skills
    └── utilities/            10 general utility skills
```

## Available Skills

### First-Party Skills

Custom-built skills authored by **haseeb-heaven**.

| Skill | Description | Install Command |
|-------|-------------|-----------------|
| [**pr-review**](first-party/pr-review/SKILL.md) | AI-powered pull request review — analyzes diffs, identifies bugs, suggests improvements with severity levels | `npx skills add haseeb-heaven/heaven-skills/first-party/pr-review` |
| [**implementor**](first-party/implementor/SKILL.md) | Structured implementation workflow — breaks down requirements, writes clean code, validates with tests | `npx skills add haseeb-heaven/heaven-skills/first-party/implementor` |

### Third-Party Skills: AWS Ecosystem (16)

Official skills maintained by **Amazon Web Services**.

| Skill | Description | Install Command |
|-------|-------------|-----------------|
| [**amazon-bedrock**](third-party/aws/amazon-bedrock/SKILL.md) | Build generative AI apps with AWS Bedrock | `.../third-party/aws/amazon-bedrock` |
| [**aws-billing-and-cost-management**](third-party/aws/aws-billing-and-cost-management/SKILL.md) | Analyze costs, find savings opportunities | `.../third-party/aws/aws-billing-and-cost-management` |
| [**aws-blocks**](third-party/aws/aws-blocks/SKILL.md) | Guide building full-stack apps on AWS Blocks | `.../third-party/aws/aws-blocks` |
| [**aws-cdk**](third-party/aws/aws-cdk/SKILL.md) | Author/deploy/troubleshoot CDK stacks (TS/Python) | `.../third-party/aws/aws-cdk` |
| [**aws-cloudformation**](third-party/aws/aws-cloudformation/SKILL.md) | Author/validate/deploy CloudFormation templates | `.../third-party/aws/aws-cloudformation` |
| [**aws-compute**](third-party/aws/aws-compute/SKILL.md) | Provision/scale EC2 instances & auto-scaling | `.../third-party/aws/aws-compute` |
| [**aws-containers**](third-party/aws/aws-containers/SKILL.md) | Deploy/manage ECS, EKS, App Runner containers | `.../third-party/aws/aws-containers` |
| [**aws-deployment**](third-party/aws/aws-deployment/SKILL.md) | CI/CD pipelines (CodePipeline, CodeDeploy, CodeBuild) | `.../third-party/aws/aws-deployment` |
| [**aws-messaging-and-streaming**](third-party/aws/aws-messaging-and-streaming/SKILL.md) | SQS, SNS, Kinesis, EventBridge event-driven architecture | `.../third-party/aws/aws-messaging-and-streaming` |
| [**aws-observability**](third-party/aws/aws-observability/SKILL.md) | CloudWatch, X-Ray, Application Signals monitoring | `.../third-party/aws/aws-observability` |
| [**aws-sdk-js-v3-usage**](third-party/aws/aws-sdk-js-v3-usage/SKILL.md) | JavaScript/TypeScript SDK v3 reference guide | `.../third-party/aws/aws-sdk-js-v3-usage` |
| [**aws-sdk-python-usage**](third-party/aws/aws-sdk-python-usage/SKILL.md) | Python/boto3 SDK reference guide | `.../third-party/aws/aws-sdk-python-usage` |
| [**aws-sdk-swift-usage**](third-party/aws/aws-sdk-swift-usage/SKILL.md) | Swift SDK development guide | `.../third-party/aws/aws-sdk-swift-usage` |
| [**aws-serverless**](third-party/aws/aws-serverless/SKILL.md) | Lambda, API Gateway, Step Functions serverless patterns | `.../third-party/aws/aws-serverless` |
| [**launch-with-aws**](third-party/aws/launch-with-aws/SKILL.md) | Migrate web apps to production-ready AWS infrastructure | `.../third-party/aws/launch-with-aws` |
| [**signing-in-to-aws**](third-party/aws/signing-in-to-aws/SKILL.md) | SSO login, IAM credentials, assumed roles, MFA | `.../third-party/aws/signing-in-to-aws` |

### Third-Party Skills: Engineering Toolkit (8)

Community-engineered skills for software development workflows.

| Skill | Description | Install Command |
|-------|-------------|-----------------|
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

| Skill | Description | Install Command |
|-------|-------------|-----------------|
| [**find-skills**](third-party/utilities/find-skills/SKILL.md) | Discover and compare available community skills | `.../third-party/utilities/find-skills` |
| [**loopy**](third-party/utilities/loopy/SKILL.md) | Loopy conversational bot automation & workflows | `.../third-party/utilities/loopy` |
| [**git-guardrails-claude-code**](third-party/utilities/git-guardrails-claude-code/SKILL.md) | Set up Claude Code git hooks & quality guardrails | `.../third-party/utilities/git-guardrails-claude-code` |
| [**migrate-to-shoehorn**](third-party/utilities/migrate-to-shoehorn/SKILL.md) | Migrate test files between frameworks & formats | `.../third-party/utilities/migrate-to-shoehorn` |
| [**scaffold-exercises**](third-party/utilities/scaffold-exercises/SKILL.md) | Generate exercise boilerplate for coding challenges & tutorials | `.../third-party/utilities/scaffold-exercises` |
| [**setup-pre-commit**](third-party/utilities/setup-pre-commit/SKILL.md) | Configure Husky pre-commit hooks for linting, formatting, testing | `.../third-party/utilities/setup-pre-commit` |
| [**no-mistakes**](third-party/utilities/no-mistakes/SKILL.md) | Validate code against best practices — security, error handling, edge cases | `.../third-party/utilities/no-mistakes` |
| [**opentui**](third-party/utilities/opentui/SKILL.md) | Build terminal UIs with OpenTUI (Rust TUI framework) | `.../third-party/utilities/opentui` |
| [**obsidian-vault**](third-party/utilities/obsidian-vault/SKILL.md) | Search, create & manage Obsidian vault notes programmatically | `.../third-party/utilities/obsidian-vault` |
| [**grilling**](third-party/utilities/grilling/SKILL.md) | Relentlessly clarify ambiguous requirements before implementation | `.../third-party/utilities/grilling` |

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

**Author:** Original Author / Organization
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full contribution guide.

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for details on adding new skills or improving existing ones.

Please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before participating.

## License

[MIT](LICENSE) — Free to use, modify, and distribute.

---

Built and maintained by **[haseeb-heaven](https://github.com/haseeb-heaven)**.
