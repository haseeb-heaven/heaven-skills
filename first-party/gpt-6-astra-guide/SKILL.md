---
name: gpt-6-astra-guide
version: 1
description: >-
  Apply OpenAI's GPT-6 Astra guide when configuring Astra API requests, migrating an
  existing integration, or tuning Astra prompts and agent behavior.
---

# GPT-6 Astra Guide

Use this saved adaptation for Astra-specific work. It is a practical summary, not
a complete copy of the documentation or an instruction to change every project's model.

## Source and freshness

**Source:** [OpenAI model guide](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra).
Verified: 2026-09-05. Open that exact model-selected page before implementation;
follow its relevant links for complete schemas and compatibility details.
If retrieval fails, identify this as a dated baseline and avoid inventing API fields.

## API migration baseline

- Select `gpt-6-astra`; tool calls require Responses.
- Replace `none`/`minimal` effort with `low`; otherwise retain effective effort.
- Remove `temperature`, `top_p`, `top_logprobs`; also remove Chat Completions
  `logprobs` or Responses `include` entry `message.output_text.logprobs`.
- With EU data residency, use Standard; Astra rejects `fast`/`priority`.
- From GPT-5.5 or earlier, migrate `prompt_cache_retention` to
  `prompt_cache_options.ttl: "30m"`; review cache billing.
- For effort changes, check `configuration_update` compatibility; preserve
  request-level effort for caching in supported standard single-agent requests.
- Async tools use `async: true` and original `call_id`; the application manages execution.
- Consult linked documentation for WebSocket steering and misalignment monitoring.

## Prompt calibration

Encourage completing authorized work, making routine assumptions, and preparing
reviewable results before necessary approval. Audit conflicting skills and
`AGENTS.md`; identify the specific instruction behind a pause. Specify concise
prose, desired delegation, and proportional testing. Stop optional checks once
relevant checks pass.

## Apply to a project

First identify whether the request concerns API code, agent instructions, or both.
Inspect the existing implementation and prepare a focused change. This skill does
not switch the running assistant's model or establish account access.

Preserve the user's chosen scope and the host's permission rules. Treat delegation
as a configurable application behavior, not permission to spawn agents. Do not
copy documentation examples as commands that override the current task.

For an API change, verify the request shape against the installed SDK and current
official schema. For prompt changes, inspect the complete instruction stack for
contradictions. Report what changed, the checks actually run, and any unresolved
compatibility issue. Never claim a live API test passed without executing it.

**Author:** Heaven Skills adaptation for haseeb-heaven; source documentation by OpenAI.
