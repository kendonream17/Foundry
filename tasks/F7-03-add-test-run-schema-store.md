# F7-03 Add TestRun Schema And Store

## Goal
Persist test command runs and outputs.

## Files To Read
- `src/core/api-contract.ts`
- `src/state/workspace-state.ts`
- `src/fs/locked-file-system.ts`

## Files To Modify
- `src/core/api-contract.ts`
- `src/test-runs/test-run-store.ts`
- Optional state path helper file

## Exact Instructions
1. Add `runtimeTestRunSchema`.
2. Add storage helpers to list/create/update test runs.
3. Include command, status, output, exit code, task ID, optional patch proposal ID, timestamps.

## Forbidden Changes
- Do not execute commands yet.
- Do not change existing terminal command behavior.

## Acceptance Criteria
- Test runs can be persisted and retrieved.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F6-04

## Recommended Owner
Smaller local model

