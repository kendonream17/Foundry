# F7-02 Add Apply Patch API

## Goal
Apply an approved patch proposal through a backend-controlled API.

## Files To Read
- `src/trpc/workspace-api.ts`
- `src/trpc/app-router.ts`
- `src/patches/patch-apply.ts`
- `src/patches/patch-proposal-store.ts`
- `src/workspace/task-worktree.ts`

## Files To Modify
- `src/trpc/app-router.ts`
- `src/trpc/workspace-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`
- `src/patches/patch-apply.ts`

## Exact Instructions
1. Add an apply patch mutation.
2. Require a patch proposal ID and explicit approval flag.
3. Validate before applying.
4. Apply in the intended task worktree or selected safe target.
5. Update proposal status.

## Forbidden Changes
- Do not auto-apply from worker execution.
- Do not modify main repo unless the API target explicitly allows it.

## Acceptance Criteria
- Approved proposal can be applied.
- Failed validation does not mutate files.

## Tests / Checks
- `npm run typecheck`
- Integration test if practical

## Difficulty
High

## Dependencies
- F7-01

## Recommended Owner
Codex

