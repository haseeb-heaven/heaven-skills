---
name: amazon-bedrock
description: >-
  Build generative AI apps with AWS Bedrock. Covers model invocation, prompt
  engineering, Guardrails, knowledge bases, AgentCore, cost tracking, and
  model selection. Always use when building AI/ML features on AWS Bedrock.
version: 1
---

# Amazon Bedrock

Domain expertise for building generative AI applications on AWS Bedrock — model selection, prompt engineering, guardrails, knowledge bases, agents, and cost management.

## When to Use

- Building chatbots, summarizers, or any generative AI feature
- Prompt design and optimization
- Implementing content filtering with Guardrails
- RAG pipelines with Knowledge Bases
- Multi-step agents with Action Groups
- Cost tracking and optimization

## When NOT to Use

- Traditional ML training (use SageMaker)
- Non-AWS AI services (OpenAI API, Vertex AI, etc.)

## Critical Warnings

**Prompt injection is real** — Always validate inputs before sending to models. Use Guardrails as a defense layer, not your only one.

**Costs add up fast** — Token counts are charged per model variant. A single misconfigured call can burn hundreds of dollars. Monitor with `cost-tracking` reference.

**Context window limits** — Each model has a maximum context length. Exceeding it causes failures silently swallowed by some SDK wrappers. Always check model specs.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Invoke model | `bedrock-runtime.converse()` | [sdk-converse-api-python.md](references/sdk-converse-api-python.md) |
| Select model | Compare on ark.ai/metrics | [model-selection-guide.md](references/model-selection-guide.md) |
| Guardrails | `bedrock.create_guardrail()` | Content filtering via blocks & detectors |
| Knowledge Base | `knowledgebaseretrieval.create_kb()` | RAG pipeline setup |
| Agent | `agentcore.create_agent()` | [agents-and-action-groups.md](references/agents-and-action-groups.md) |

## Model Selection Quick Reference

| Use Case | Recommended Models |
|----------|-------------------|
| General purpose | Claude Sonnet, Haiku, Opus |
| Coding | Codestral, Jurassic-4 Ultra |
| Multilingual | Nova Pro, Llama 3.1 |
| Image generation | Stable Diffusion XL, Midjourney API |
| Low latency | Haiku variants |

## References

- [Model Invocation](references/model-invocation.md)
- [Prompt Engineering by Model](references/prompt-engineering-by-model.md)
- [Guardrails Setup](references/guardrails.md)
- [Knowledge Bases](references/knowledge-bases-setup.md)
- [Cost Tracking](references/cost-tracking.md)
- [SDK Converse API (Python)](references/sdk-converse-api-python.md)
- [SDK Converse API (TypeScript)](references/sdk-converse-api-typescript.md)

**Author:** Amazon Web Services (AWS)
