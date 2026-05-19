# F11-01 Add Split Task Card Action

## Goal
Allow a task card to be split into child task cards.

## Files To Read
- `web-ui/src/state/board-state.ts`
- `web-ui/src/state/board-state.test.ts`
- `web-ui/src/types/board.ts`

## Files To Modify
- `web-ui/src/state/board-state.ts`
- `web-ui/src/state/board-state.test.ts`
- UI integration file selected later

## Exact Instructions
1. Add a pure board-state helper for splitting one card into multiple cards.
2. Preserve baseRef and relevant settings.
3. Add optional parent task ID if the schema supports it by then.

## Forbidden Changes
- Do not add Architect generation logic.
- Do not auto-start child tasks.

## Acceptance Criteria
- Board-state test proves split preserves board validity.

## Tests / Checks
- `npm --prefix web-ui run test -- board-state`
- `npm --prefix web-ui run typecheck`

## Difficulty
Medium

## Dependencies
- Optional dependency on task card parent fields

## Recommended Owner
Smaller local model

