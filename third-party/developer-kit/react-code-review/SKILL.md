---
name: react-code-review
description: Use when software developers review React components, hooks, pages, forms, state management, accessibility, TypeScript integration, or React pull requests before merge.
---

# React Code Review

> Upstream: `giuseppe-trisciuoglio/developer-kit` — `plugins/developer-kit-typescript/skills/react-code-review/SKILL.md`

Review React source-code changes for correctness, architecture, accessibility, performance, and production readiness. Respect the React version and existing project conventions.

**Software-development scope only:** use for React, TypeScript, JavaScript, frontend tests, build configuration, browser behavior, and code-review workflows. Do not use for visual-brand critique, marketing copy, general design writing, resumes, documents, or non-code content.

## Review areas

### Component architecture

- Components have one clear responsibility.
- Data access, business logic, and rendering are not unnecessarily mixed.
- Props remain focused and strongly typed.
- Shared abstractions are justified by real reuse.
- Client and server component boundaries are valid.

### Hooks and state

- Hooks follow the Rules of Hooks.
- Effect dependencies are complete and cleanup is present where required.
- Effects are not used for derivable state.
- Async work handles cancellation, stale responses, and unmounts.
- State is colocated and not lifted without need.
- Server state follows the project's established fetching/cache layer.

### React 19

When the project uses React 19, review Actions, `use`, `useOptimistic`, `useFormStatus`, transitions, Suspense, and error-boundary behavior. Do not recommend React 19 APIs to older projects.

### Accessibility

- Prefer semantic HTML before ARIA.
- Controls are keyboard operable and visibly focusable.
- Inputs have programmatic labels and accessible errors.
- Dialogs, menus, and popovers manage focus correctly.
- Loading and status changes are exposed appropriately.

### Performance

- Identify measured or clearly material re-render problems.
- Avoid recommending memoization without evidence.
- Check list keys, large imports, code splitting, request waterfalls, and expensive work during render.
- Detect repeated network calls and unbounded client-side processing.

### TypeScript

- Avoid `any`, unsafe casts, and impossible states.
- Verify event, ref, component, API-response, and form types.
- Ensure frontend expectations match backend contracts.

## Verification

Run the project's applicable commands, such as:

```bash
npm run lint
npm run typecheck
npm test
npm run build
```

For user-facing changes, verify the flow in a real browser and inspect console and network errors.

## Output

Classify findings as:

- **Critical:** broken behavior, security, data loss, or inaccessible core flow;
- **Warning:** correctness, architecture, performance, or maintainability problem;
- **Suggestion:** optional improvement with measurable value.

Every finding must include file/line, failure scenario, evidence, and a concrete correction. Avoid subjective style comments and speculative rewrites.