---
name: production-pr-review
description: Use when a pull request is proposed for production deployment, especially for security-sensitive, data-processing, multi-tenant, billing, migration, API-contract, or end-to-end user-flow changes.
version: 1
---

# Production PR Review

## Overview

Treat every production pull request as a release gate, not a style review.

**Core principle:** no merge recommendation without fresh evidence from the exact review range.

## Non-Negotiable Rules

- Review the complete `origin/main...HEAD` diff.
- Read directly related callers, schemas, migrations, tests, configuration, and deployment files.
- Do not trust an agent, CI summary, or previous test run without checking current evidence.
- Do not say “looks good,” “should work,” “production ready,” or “all tests pass” without fresh command output.
- Do not edit code until the initial findings are complete.
- Do not merge with unresolved BLOCKER or HIGH findings.
- Ignore cosmetic preferences unless they affect correctness, accessibility, security, performance, or maintainability.

## Review Workflow

### 1. Establish Scope

```bash
BASE_SHA=$(git merge-base origin/main HEAD)
HEAD_SHA=$(git rev-parse HEAD)
git diff --stat "$BASE_SHA...$HEAD_SHA"
git diff "$BASE_SHA...$HEAD_SHA"
```

Identify:

- intended user behavior;
- acceptance criteria;
- changed trust boundaries;
- affected routes, services, schemas, migrations, storage, and UI flows.

### 2. Discover Repository Gates

Read the project’s actual commands from:

- `package.json`;
- `pyproject.toml`;
- `Makefile`;
- CI workflow files;
- Docker files;
- repository documentation.

Do not invent replacement commands when the repository already defines authoritative ones.

### 3. Run Fresh Verification

Run every applicable gate and record the command, exit code, and relevant output.

#### Backend

- formatter check;
- lint;
- static typing;
- unit tests;
- integration tests;
- migration validation;
- production application startup.

#### Frontend

- formatter check;
- lint;
- TypeScript type check;
- unit and component tests;
- production build;
- end-to-end tests.

#### Repository and Deployment

- secret scan;
- dependency or vulnerability scan;
- Docker/build validation;
- CI status;
- environment-variable review;
- health-check and rollback review.

A passing linter does not prove the build succeeds. A passing build does not prove the user flow works.

### 4. Verify the Full User Story

Trace the changed behavior through every boundary:

```text
browser → frontend → API → service → database/storage → response → browser
```

Check:

- UI trigger and loading/error/empty states;
- request URL, method, headers, and payload;
- server-side validation and authorization;
- transaction and storage behavior;
- response schema and status codes;
- frontend rendering of success and failure;
- browser console, network failures, and server logs.

Stop at the first broken boundary, document evidence, and require a correction before continuing.

### 5. Review Production Risks

#### Correctness

- malformed and boundary inputs;
- missing `await` or blocking work in async code;
- race conditions and stale state;
- partial failures and retry behavior;
- idempotency and duplicate requests;
- frontend/backend contract drift;
- broad exception handling and swallowed failures.

#### Security and Privacy

- authorization at the server boundary;
- cross-user and cross-tenant data isolation;
- injection, XSS, CSRF, SSRF, path traversal, and unsafe redirects;
- secrets or personal data in logs, fixtures, analytics, or errors;
- unsafe file names, MIME assumptions, parser behavior, archive expansion, and upload limits;
- token, session, OAuth, billing, and webhook handling.

#### Data and Database

- migration safety and rollback strategy;
- destructive schema changes;
- transaction boundaries;
- indexes and query plans;
- N+1 queries;
- optimistic concurrency and lost updates;
- retention, deletion, and ownership rules.

#### Maintainability

- repository conventions and module boundaries;
- unjustified dependencies;
- duplicated business rules;
- hidden configuration or hard-coded production values;
- TODOs, placeholders, disabled tests, mocked production paths, or dead code.

#### Testing Quality

Reject tests that:

- only restate implementation logic;
- mock the behavior under test;
- cover only the happy path;
- pass without exercising the changed code;
- depend on order, time, network, or shared state without control.

Require a regression test for every confirmed defect.

## Severity Model

| Severity | Definition | Merge Policy |
|---|---|---|
| BLOCKER | Security breach, data loss, privacy exposure, broken migration, outage risk, or core flow failure | Must fix |
| HIGH | Correctness defect, authorization gap, race condition, incompatible contract, or missing critical coverage | Must fix |
| MEDIUM | Material resilience, performance, operability, or maintainability problem | Fix before release unless explicitly accepted |
| LOW | Non-blocking improvement with concrete value | Optional |
| VERIFIED | Behavior confirmed by fresh evidence | Record evidence |

## Finding Format

Every finding must include:

- severity;
- file and line;
- exact defect;
- realistic failure scenario;
- evidence;
- required correction;
- test that proves the correction.

Avoid vague comments such as “consider improving this” or “might be an issue.”

## Required Output

```markdown
## Verdict
MERGE / DO NOT MERGE

## Blocking Findings
BLOCKER and HIGH findings only.

## Other Findings
MEDIUM and LOW findings.

## Verification Evidence
| Command | Exit Code | Result | Relevant Output |
|---|---:|---|---|

## End-to-End Flow
| Boundary | Status | Evidence |
|---|---|---|
| Browser rendering | PASS/FAIL/UNVERIFIED | ... |
| Frontend request | PASS/FAIL/UNVERIFIED | ... |
| API validation | PASS/FAIL/UNVERIFIED | ... |
| Authorization | PASS/FAIL/UNVERIFIED | ... |
| Database/storage | PASS/FAIL/UNVERIFIED | ... |
| Response contract | PASS/FAIL/UNVERIFIED | ... |
| Final UI state | PASS/FAIL/UNVERIFIED | ... |

## Deployment Readiness
Migrations, environment variables, build artifacts, health checks, rollback, and observability.

## Unverified Areas
Anything that could not be tested and the exact reason.
```

## Merge Decision

Recommend `MERGE` only when:

- no unresolved BLOCKER or HIGH findings remain;
- required tests, lint, types, and production builds pass freshly;
- changed migrations are safe;
- authorization and tenant isolation are verified where applicable;
- sensitive data is not exposed;
- the changed user flow is verified end to end;
- deployment and rollback requirements are understood;
- every unverified area is explicitly disclosed.
