---
name: migrate-to-shoehorn
description: >-
  Migrate test files from shoehorn format to alternative formats or structures. Handles
  file reorganization, import path updates, assertion library changes, fixture migrations,
  and verification that all tests still pass after transformation. Use when refactoring
  test infrastructure or standardizing test formats across a codebase.
version: 1
---

# Migrate to Shoehorn

Migrate test files between formats (shoehorn ↔ other frameworks) while preserving test behavior and coverage.

## When NOT to Use

- Moving between formats with incompatible assertion styles without a mapping layer
- Large-scale refactors where you should also change test logic — do migration and logic changes separately
- When test coverage is below 60% — stabilize first, then migrate

## Migration Strategy

### Phase 1: Audit
1. **Inventory existing tests** — List all test files, their frameworks, and assertion patterns
2. **Map constructs** — Create a translation table between old and new formats
3. **Identify blockers** — Features in old framework not available in new one

### Phase 2: Translation Table
Build a reference for converting between formats:

| Old Format | New Format | Notes |
|-----------|-----------|-------|
| `assert.equal(a, b)` | `expect(a).toBe(b)` | Direct mapping |
| `it('desc', fn)` | `describe/it` nesting | Structural change |
| `beforeEach(fn)` | `setUp()` / `beforeAll()` | Lifecycle hook rename |
| File fixtures (`test/fixtures/*.json`) | Inline test data or separate fixtures | Depends on size |

### Phase 3: Automated Conversion
For simple cases, use scripts:
```bash
# Example: Convert Jasmine → Jest
npx jasmine-ts-to-jest src/**/*.spec.ts
```

For complex cases, convert file-by-file:
1. Copy the file to its new location
2. Update imports and framework references
3. Convert test definitions line by line
4. Run tests to verify they pass with same results

### Phase 4: Verification
After conversion:
```bash
# Run new tests
npm run test:new-format

# Compare coverage reports
# Coverage should be within 2% of original

# Delete old test files only after green build
rm -rf src/**/*.old-spec.js
```

## Common Framework Pairs

| From | To | Key Differences |
|------|-----|----------------|
| Jasmine | Jest | `describe/it` syntax, spy functions |
| Mocha + Chai | Vitest | Native TypeScript support, Vite integration |
| Tape |AVA | Parallel execution, subtests |
| Shoehorn | Custom | Define target schema first |

## Output Format

```markdown
## Migration Report: [Old] → [New]

### Scope
- [N] test files converted
- [N] test cases migrated
- [N] assertions translated

### Changes Made
| File | Action | Result |
|------|--------|--------|
| auth.spec.js | Converted | ✅ Tests pass |

### Known Issues
- [Any limitations or manual steps remaining]

### Coverage Delta
- Before: [X]% | After: [Y]% (change: ±Z%)
```
