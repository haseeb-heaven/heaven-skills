---
name: resolving-merge-conflicts
description: >-
  Use when you need to resolve merge conflicts systematically without losing work.
  Covers understanding conflict causes, comparing code paths, choosing correct changes,
  preserving intent from both branches, and verifying merged code compiles and tests pass.
  Use when git reports CONFLICT status or when merging PRs with overlapping changes.
version: 1
---

# Resolving Merge Conflicts

Systematic approach to resolving merge conflicts that preserves intent from both branches and prevents data loss.

## When NOT to Use

- Automated merge tools can handle it — simple whitespace or non-overlapping line additions
- The conflicting code is clearly wrong in one branch — just take the correct version
- You don't understand either branch's intent — ask the author before deciding

## The Four Conflict Types

| Type | What Happened | Resolution Strategy |
|------|--------------|-------------------|
| **Add/Add** | Both branches created the same file at the same path | Combine if different content; pick one if identical |
| **Modify/Modify** | Both changed the same lines | Compare intents, merge semantically, keep what makes sense |
| **Delete/Delete** | Both deleted a file added on the base branch | Usually keep both deletes (file stays gone) |
| **Modify/Delete** | One changed a file the other deleted | Decide: keep the change (update the delete) or keep the deletion |

## Resolution Process

### Step 1: Understand the Conflict
```bash
git diff --name-only --diff-filter=U   # Files with conflicts
git status                             # Detailed conflict info
```
Read the conflict markers carefully. Lines between `<<<<<<<`, `=======`, and `>>>>>>>` show both versions.

### Step 2: Analyze Each Side
For each conflict:
1. Read the **ours** section (current branch) — what was your intent?
2. Read the **theirs** section (incoming branch) — what was their intent?
3. Check the commit messages on both sides for context
4. Ask: "Do these changes overlap semantically or just cosmetically?"

### Step 3: Resolve
Choose one of these strategies:

| Strategy | When to Use | How |
|----------|-------------|-----|
| **Keep ours** | Your change is newer, theirs is stale | Delete theirs section |
| **Keep theirs** | Their change addresses something urgent | Delete ours section |
| **Combine** | Both changes are valid and complementary | Keep both, fix any syntax issues |
| **Rewrite** | Neither version is quite right | Write a new version that satisfies both needs |

### Step 4: Verify
After resolving all conflicts:
```bash
git diff                              # Review final merged result
npm test / pytest / cargo test        # Ensure tests pass
./build                               # Ensure build succeeds
code --open .                         # Spot-check for obvious issues
```

### Step 5: Commit
```bash
git add <resolved-files>
git commit -m "Merge <branch>: resolve conflicts in [files]"
```

## Common Pitfalls

- **Taking everything from one side blindly** — This discards valid work. Always compare.
- **Leaving conflict markers** — `<<<<<<< HEAD` in production code means the merge wasn't completed.
- **Not running tests after merge** — Semantic merges may break logic even if they compile.
- **Merging master into feature repeatedly** — Prefer rebasing feature onto master for cleaner history.

## Prevention Tips

1. **Pull frequently** — Daily pulls from main prevent large conflict accumulation
2. **Small, focused commits** — Smaller diffs = smaller conflicts
3. **Communicate** — Tell teammates you're changing shared files early
4. **Use feature flags** — Decouple deployment from activation to avoid integration conflicts

**Source:** [mattpocock/skills](https://github.com/mattpocock/skills) — Skills for Real Engineers