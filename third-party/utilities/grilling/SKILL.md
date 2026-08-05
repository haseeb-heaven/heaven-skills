---
name: grilling
description: >-
  Grill the user relentlessly to clarify ambiguous requirements, expose hidden assumptions,
  and ensure alignment before implementation. Asks pointed questions about constraints,
  edge cases, success criteria, and trade-offs. Use when requirements feel vague, scope
  creep is likely, or you need stakeholder commitment on decisions.
version: 1
---

# Grilling

Grill the user relentlessly to clarify ambiguous requirements, expose hidden assumptions, and ensure alignment before implementation.

## When NOT to Use

- Simple, well-defined tasks with clear acceptance criteria
- During active debugging sessions — focus on solving, not questioning
- When the user explicitly says "just do it" (respect that signal)
- Late-night/urgent situations where speed matters more than clarity

## The Grilling Framework

### Phase 1: Constraint Discovery
Before writing any code, establish boundaries:

| Question Category | Questions to Ask |
|------------------|-----------------|
| **Scope** | What exactly needs to be built? What's explicitly OUT of scope? |
| **Timeline** | When does this need to ship? Is there a hard deadline? |
| **Users** | Who will actually use this? Technical proficiency level? |
| **Data** | How much data? From where? What format? Quality? |
| **Integration** | What systems must this work with? APIs? Databases? |
| **Compliance** | GDPR, HIPAA, SOC2, accessibility requirements? |

### Phase 2: Assumption Testing
Challenge every implicit assumption:

```
User: "We just need a search feature."

🔥 GRILL:
- Search what? Entire database or specific fields?
- Exact match or fuzzy? Should "color" match "colour"?
- Real-time results or paginated?
- Do users expect filters/sorting alongside search?
- What happens with zero results?
- Performance targets: <100ms? <1s?
- Mobile or desktop primarily?
- Do we need search analytics?
```

### Phase 3: Edge Case Exploration
Push for failure scenarios:

| Category | Example Questions |
|----------|-----------------|
| Input | "What if the field is empty/null/too long?" |
| Volume | "What happens with 1M records vs 10 records?" |
| Concurrency | "What if two people edit simultaneously?" |
| Network | "What if the API returns 500? Times out?" |
| Security | "Can a user see another user's data accidentally?" |
| State | "What if the app crashes mid-operation?" |

### Phase 4: Decision Lock-In
Get explicit commitments before proceeding:

```markdown
## Decisions Made (Commitments)

| # | Decision | By Whom | Confirmed |
|---|----------|---------|-----------|
| 1 | Use SQLite, not PostgreSQL | @stakeholder ✅ | Yes |
| 2 | Pagination over infinite scroll | @product-owner ✅ | Yes |
| 3 | No real-time search (batch nightly) | @tech-lead ✅ | Yes |

## Open Questions
| # | Question | Owner | Deadline |
|---|----------|-------|----------|
| 1 | Do we need full-text search? | @product-owner | EOD Friday |
```

## Grilling Techniques

| Technique | When to Use | Example |
|-----------|-------------|---------|
| **Five Whys** | Requirements feel shallow | "Why do you need export?" → "Why?" x5 |
| **Concrete Examples** | Abstract descriptions | "Can you show me an example of the expected output?" |
| **Negation Test** | Scope ambiguity | "So we should NOT build X? Can you confirm?" |
| **Constraint Stress Test** | Feasibility unknown | "If we only had 1 second response time, would this still work?" |
| **Post-Mortem Preview** | Risk identification | "Imagine this shipped and failed catastrophically — why would that happen?" |

## Output Format

After grilling session, summarize:

```markdown
## Requirements Clarification Summary

### Clarified Requirements
1. [Requirement] — [Clarified details from Q&A]
2. [Requirement] — ...

### Confirmed Constraints
- [Constraint]: [Detail]

### Assumptions Documented
- We assume: [assumption] — confirmed by [@person]
- We DO NOT assume: [non-assumption] — explicitly ruled out

### Decisions Locked
- [Decision] — confirmed by [@person] on [date]

### Remaining Risks
- [Risk]: Impact, mitigation, owner
```

## Golden Rules

1. **Grill first, build second** — Never start coding without completing this process for non-trivial features
2. **Be respectful but persistent** — You're helping, not being difficult. Phrase questions as clarification requests.
3. **Document everything** — Verbal agreements disappear; written confirmations survive
4. **Know when to stop** — If you've grilled for 2+ hours with no resolution, escalate to a meeting
5. **Accept "I don't know"** — Sometimes the right answer is "we'll figure it out during implementation" with a small experiment first
