# F11-02 Add Merge Task Cards Action

## Goal
Allow multiple task cards to be merged into one.

## Files To Read
- `web-ui/src/state/board-state.ts`
- `web-ui/src/state/board-state.test.ts`
- `web-ui/src/types/board.ts`

## Files To Modify
- `web-ui/src/state/board-state.ts`
- `web-ui/src/state/board-state.test.ts`
- UI integration file selected later

## Exact Instructions
1. Add a pure board-state helper to merge selected cards.
2. Combine prompts in a clear format.
3. Preserve baseRef when all cards share one; otherwise require caller to provide baseRef.

## Forbidden Changes
- Do not delete worktrees.
- Do not change drag/drop behavior.

## Acceptance Criteria
- Board-state test proves merge removes source cards and creates one valid card.

## Tests / Checks
- `npm --prefix web-ui run test -- board-state`
- `npm --prefix web-ui run typecheck`

## Difficulty
Medium

## Dependencies
- None

## Recommended Owner
Smaller local model

