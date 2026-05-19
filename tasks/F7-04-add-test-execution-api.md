# F7-04 Add Test Execution API

## Goal
Run a configured test command and store output.

## Files To Read
- `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `src/server/runtime-server.ts`
- `src/workspace/git-utils.ts`
- `src/test-runs/test-run-store.ts`

## Files To Modify
- `src/test-runs/test-runner.ts`
- `src/trpc/app-router.ts`
- `src/trpc/workspace-api.ts` or `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`

## Exact Instructions
1. Add a test run mutation.
2. Run a user-configured command in a project or task worktree.
3. Capture stdout/stderr and exit code.
4. Store the result through F7-03 store.

## Forbidden Changes
- Do not run commands without explicit user request.
- Do not add auto-fix behavior.

## Acceptance Criteria
- Test command output is stored and returned.
- Nonzero exit code is represented as failed, not as an API crash.

## Tests / Checks
- `npm run typecheck`
- Focused integration test with harmless command

## Difficulty
Medium

## Dependencies
- F7-03

## Recommended Owner
Codex

