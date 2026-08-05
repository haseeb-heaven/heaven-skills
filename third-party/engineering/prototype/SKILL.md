---
name: prototype
description: >-
  Build a throwaway prototype quickly to validate ideas, test approaches, or demonstrate concepts.
  Focuses on speed over quality, discards code after validation, and captures learnings for
  the real implementation. Use when exploring uncertain requirements, comparing technical approaches,
  or need to prove feasibility before committing to production code.
version: 1
---

# Prototype

Build throwaway prototypes fast to validate ideas and reduce risk before building production features.

## When NOT to Use

- Known requirements with clear acceptance criteria — skip straight to implementation
- Features where you'll reuse the code — if it's reusable, build it properly from the start
- Customer-facing demos requiring polish — use a demo/staging environment instead

## Core Principles

| Principle | What It Means | What to Avoid |
|-----------|--------------|---------------|
| **Fast first** | Ship something working in hours, not days | Perfektionism kills exploration |
| **Discardable** | Written to be thrown away | No cleanup needed after validation |
| **Focused** | One question, one variable under test | Feature creep during prototyping |
| **Learned from** | Captures what was validated/invalidated | Code that sits unused after |

## Process

### Step 1: Define the Question
What specific uncertainty does this prototype address?
- "Can we process 10K records/min with library X?"
- "Does user understand this UI pattern?"
- "Is this API response format workable?"

Write one sentence. If you can't, you're actually designing, not prototyping.

### Step 2: Build the Skeleton
1. Set up the minimal environment — single file projects, inline styles, fake data
2. Implement only the path that tests your hypothesis
3. Hardcode everything you can — no config files, no databases, no auth
4. Add error handling only for the exact failure case you're testing

### Step 3: Run the Test
Execute the prototype against your target scenario. Collect measurable results:
- Time to complete
- Success/failure rate
- User feedback scores
- Performance benchmarks

### Step 4: Decide & Capture
- **Pass** → Document findings, inform production design
- **Fail** → Document what didn't work, adjust approach, build new prototype
- **Maybe** → Narrow scope, refine hypothesis, iterate

### Step 5: Clean Up
Delete the prototype. Archive findings in project notes. Don't leave junk.

## Common Prototyping Shortcuts

| Area | Production Approach | Prototype Shortcut |
|------|-------------------|-------------------|
| Data | Real database, migrations | In-memory store, hardcoded JSON |
| Auth | OAuth, sessions | Bypass, admin-only, static token |
| UI | Design system, responsive | Plain HTML/CSS, hardcoded widths |
| APIs | Proper error codes, pagination | Console.log, status 200 always |
| Deployment | CI/CD pipeline | localhost, direct run |

## Output Format

```markdown
## Prototype Report: [Title]

### Question Addressed
[The specific uncertainty being tested]

### Approach
[Brief description of what was built and how]

### Results
- [Measurable outcome 1]
- [Measurable outcome 2]

### Findings
- [What we learned]
- [What still needs investigation]

### Decision
- [Next steps based on results]

### Prototype Location
[File path or link — will be deleted after review]
```
