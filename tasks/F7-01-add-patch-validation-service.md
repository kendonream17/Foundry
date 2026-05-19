# F7-01 Add Patch Validation Service

## Goal
Validate patch proposals before user approval/application.

## Files To Read
- `src/workspace/git-utils.ts`
- `src/workspace/path-sandbox.ts`
- `src/workspace/task-worktree.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/patches/patch-apply.ts`
- Optional test file

## Exact Instructions
1. Add a validation function that checks patch paths stay inside the repo.
2. Reject absolute paths and parent traversal.
3. Respect project off-limits globs if available.
4. Run `git apply --check` in the target worktree/repo.

## Forbidden Changes
- Do not apply the patch.
- Do not use destructive Git commands.

## Acceptance Criteria
- Bad paths are rejected.
- Invalid patches fail validation without mutation.

## Tests / Checks
- `npm run typecheck`
- Focused integration test if practical

## Difficulty
High

## Dependencies
- F1-04
- F6-04

## Recommended Owner
Codex

