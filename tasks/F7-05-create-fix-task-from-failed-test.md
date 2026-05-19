# F7-05 Create Fix Task From Failed Test

## Goal
Create a follow-up task draft from a failed test run.

## Files To Read
- `web-ui/src/state/board-state.ts`
- `web-ui/src/hooks/use-task-editor.ts`
- `src/test-runs/test-run-store.ts`
- `src/core/api-contract.ts`

## Files To Modify
- A focused service/helper file for fix task draft generation
- UI/hook file selected after reading current board creation flow

## Exact Instructions
1. Build a helper that takes a failed `TestRun` and creates a task draft prompt.
2. Include command, exit code, relevant output excerpt, and original task ID.
3. Require user approval before creating the new backlog card.

## Forbidden Changes
- Do not automatically start the fix task.
- Do not mutate existing task prompts.

## Acceptance Criteria
- Failed test run can produce a reviewable fix task draft.

## Tests / Checks
- `npm --prefix web-ui run typecheck`
- Relevant board-state tests if helper touches board state

## Difficulty
Medium

## Dependencies
- F7-04

## Recommended Owner
Smaller local model

