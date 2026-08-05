---
name: scaffold-exercises
description: >-
  Create exercise directories and boilerplate for coding challenges, tutorials, or
  training materials. Generates folder structures with starter code, test scaffolds,
  README instructions, and solution templates. Use when building learning content,
  coding bootcamps, or internal team exercises.
version: 1
---

# Scaffold Exercises

Create exercise directories and boilerplate for coding challenges, tutorials, and training materials.

## When NOT to Use

- Production code projects — use standard project scaffolding tools instead
- Documentation without interactive elements — write markdown directly
- One-off scripts with no educational value — keep it simple

## Exercise Anatomy

Every well-structured exercise contains these components:

```
exercise-name/
├── README.md          # Instructions, requirements, examples
├── src/               # Starter code (empty or partial)
│   └── index.js       # Entry point with stubs
├── tests/             # Test files
│   └── index.test.js  # Tests that validate the solution
├── solutions/         # Reference solution (hidden until solved)
│   └── index.js
└── hints.md           # Progressive hints (optional)
```

## Creation Process

### Step 1: Define Requirements
Write clear, specific instructions:
- **What** the student should build (not how)
- **Input/Output examples** with at least 3 cases
- **Edge cases** they should handle
- **Difficulty level** (beginner/intermediate/advanced)

### Step 2: Generate Structure
```bash
#!/bin/bash
create_exercise() {
  local name=$1
  local dir="$name"
  
  mkdir -p "$dir/src" "$dir/tests" "$dir/solutions"
  
  cat > "$dir/README.md" << EOF
# $name

## Instructions
[Write clear instructions here]

## Examples
\`\`\`
Input:  [example]
Output: [expected]
\`\`\`

## Requirements
- [Requirement 1]
- [Requirement 2]

## Running Tests
npm test

## Difficulty: [Level]
EOF

  echo "// TODO: Implement this function
export function solve(input) {
  throw new Error('Not implemented');
}" > "$dir/src/index.js"

  echo "import { describe, it, expect } from 'vitest';
import { solve } from '../src/index.js';

describe('$name', () => {
  it('handles basic case', () => {
    expect(solve('input')).toBe('expected');
  });
});" > "$dir/tests/index.test.js"

  echo "// Solution reference
export function solve(input) {
  // Working implementation
  return /* result */;
}" > "$dir/solutions/index.js"
}
```

### Step 3: Write Tests
Tests should be strict enough to reject incorrect solutions but flexible enough to allow different approaches:
- Check output values, not exact string formatting
- Allow different valid implementations (e.g., loop vs recursion)
- Include edge cases that commonly fail

### Step 4: Write Hints
Progressive hints that unlock understanding without giving away the answer:
1. **Hint 1**: Remind about relevant language features
2. **Hint 2**: Suggest an algorithmic approach
3. **Hint 3**: Point to a common pitfall
4. **Spoiler**: Show key code pattern (but not full solution)

## Quality Checklist

- [ ] README has clear input/output examples
- [ ] Tests cover happy path AND edge cases
- [ ] Starter code compiles/runs (even if tests fail)
- [ ] Solution actually passes all tests
- [ ] Difficulty matches target audience
- [ ] No typos or unclear instructions
