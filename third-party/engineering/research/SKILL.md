---
name: research
description: >-
  Investigate a technical question or problem systematically. Covers literature review,
  benchmark comparisons, API analysis, security research, dependency evaluation, and
  evidence-based recommendations. Use when evaluating technologies, researching solutions,
  or gathering information to inform a technical decision.
version: 1
---

# Research

Systematic approach to investigating technical questions and producing evidence-based findings.

## When NOT to Use

- Simple factual lookups — use search directly without this framework
- Implementation work — research informs but doesn't replace building
- Decisions where time is more valuable than accuracy — use heuristics instead

## Research Process

### Step 1: Frame the Question
Convert vague curiosity into a testable research question:
- ❌ "Should we use PostgreSQL?"
- ✅ "Does PostgreSQL provide sufficient geographic query support for our location-based feature at our expected data volume?"

A well-framed question has clear success criteria and a timebox.

### Step 2: Identify Sources
| Source Type | Examples | Credibility |
|------------|----------|-------------|
| Official docs | Framework READMEs, RFCs, specification pages | High |
| Benchmarks | Published performance studies, independent tests | Medium-High |
| Community | Stack Overflow, GitHub issues, blog posts | Medium |
| Expert opinion | Conference talks, senior engineer interviews | Medium |
| First-party testing | Your own POCs and benchmarks | Highest |

Always triangulate — never base decisions on a single source unless it's authoritative documentation.

### Step 3: Evaluate Findings
For each claim you encounter, assess:

| Criterion | Question to Ask |
|-----------|----------------|
| Recency | Is this still current for the version you're using? |
| Context | Does the source match your environment/requirements? |
| Bias | Who benefits from this recommendation? |
| Evidence | Is there data backing the claim, or just opinion? |
| Counterexamples | What do opposing views say? |

### Step 4: Synthesize
Combine findings into actionable conclusions:

```markdown
## Research Findings: [Topic]

### Background
[Why this research was needed]

### Key Findings
1. [Finding] — supported by [Source]
2. [Finding] — supported by [Source]
3. [Contradictory Finding] — supported by [Source]

### Recommendations
- [Recommendation] based on [Evidence]
- [Alternative] considered but rejected because [Reason]

### Open Questions
- [What wasn't resolved and needs further investigation]

### Sources
- [List with links]
```

## Timeboxing

| Research Scope | Max Time |
|---------------|----------|
| Library comparison (2 options) | 2 hours |
| Technology evaluation (3-4 options) | Half day |
| Security audit of a dependency | 2-4 hours |
| Architecture research (complex topic) | 1-2 days |