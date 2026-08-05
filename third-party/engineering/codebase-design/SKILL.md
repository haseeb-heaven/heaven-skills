---
name: codebase-design
description: >-
  Shared vocabulary for design discussions about software architecture. Provides a common
  framework for talking about modules, boundaries, data flow, coupling, cohesion, and
  architectural patterns. Use when planning system design, refactoring large changes, or
  aligning team understanding of code structure.
version: 1
---

# Codebase Design

Shared vocabulary for discussing software architecture — helping teams talk about modules, boundaries, data flow, coupling, and patterns consistently.

## When NOT to Use

- Writing implementation code directly — use specific design patterns instead
- Solving concrete bugs — diagnose and fix those independently
- Performance profiling — that requires runtime analysis tools

## Core Concepts

### Module Boundaries
A **module** is a group of related responsibilities under one cohesive name. Good module boundaries have these properties:

| Property | Description | Test |
|----------|-------------|------|
| High cohesion | Things inside belong together | Changing one thing rarely affects another |
| Low coupling | Minimal dependencies on other modules | Removing one doesn't cascade changes |
| Clear contracts | Public interface is explicit | Can replace internals without breaking callers |
| Single reason to change | One responsibility per module | Two unrelated features don't modify same file |

### Data Flow Patterns
Every system moves data through transformations:

```
Source → Transform → Destination
  ↓         ↓           ↓
 ingest   process     persist/consume
```

Identify where data enters, transforms, and exits your system. Each transition point is a potential failure mode and testing boundary.

### Coupling Types

| Type | Description | Severity |
|------|-------------|----------|
| **Temporal** | Modules must be deployed/started together | Medium |
| **Logical** | One module calls another's API directly | High |
| **Physical** | Changes in A require changes in B's source | Critical |
| **Data** | Sharing mutable state between modules | Critical |

## Design Decisions Framework

When making structural decisions, document:

1. **Context** — What problem are we solving? What constraints exist?
2. **Options considered** — At least 2-3 alternatives with tradeoffs
3. **Decision** — What we chose and why
4. **Consequences** — What this enables and what it makes harder

Format as Architecture Decision Records (ADRs):

```markdown
# ADR-NNN: [Title]
Status: Proposed | Accepted | Deprecated | Superseded
Date: YYYY-MM-DD

## Context
[What's driving this decision?]

## Decision
[What did we decide?]

## Consequences
[What follows from this choice?]
```

## Common Architectural Patterns

| Pattern | When to Use | Tradeoff |
|---------|-------------|----------|
| Layered | Traditional CRUD apps | Simple but tight coupling across layers |
| Hexagonal | Domain complexity, testability | More indirection overhead |
| CQRS | Separate read/write scaling needs | Eventual consistency complexity |
| Event-driven | Loose coupling, async processing | Debugging distributed systems |
| Microservices | Independent deployment at scale | Operational complexity |
