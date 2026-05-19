# F11-03 Add Task Completion Disposition

## Goal
Allow completed tasks to be either retained as complete or deleted/archived based on user choice.

## Files To Read
- `web-ui/src/state/board-state.ts`
- `web-ui/src/state/board-state.test.ts`
- `web-ui/src/types/board.ts`
- `web-ui/src/hooks/use-board-interactions.ts`
- `web-ui/src/components/board-card.tsx`
- `web-ui/src/components/card-detail-view.tsx`
- `src/core/api-contract.ts`
- `src/workspace/task-worktree.ts`

## Files To Modify
- `src/core/api-contract.ts`
- `web-ui/src/types/board.ts`
- `web-ui/src/state/board-state.ts`
- `web-ui/src/state/board-state.test.ts`
- UI integration files selected after reading current board/detail actions

## Exact Instructions
1. Add an explicit task completion disposition to task/card state, using additive optional fields so existing cards still load.
2. Support at least two user-visible outcomes after a task is finished:
   - Mark complete: keep the card available for history/audit.
   - Delete/archive: remove the card from the active board history the user sees.
3. Preserve current worktree safety behavior. If deletion/archive removes a worktree, route through existing cleanup logic rather than bypassing it.
4. Add UI actions from the review/completed task surface so the user can choose the outcome.
5. Keep the existing Done/Trash behavior working until the new disposition model fully replaces it.

## Forbidden Changes
- Do not delete task worktrees directly from UI code.
- Do not remove existing `trash` column support in the first implementation.
- Do not auto-delete completed tasks.
- Do not change patch approval or test execution behavior.

## Acceptance Criteria
- A completed task can be retained as complete.
- A completed task can be deleted/archived by explicit user action.
- Existing cards without the new fields still load.
- Existing move-to-trash cleanup behavior remains intact.

## Tests / Checks
- `npm run typecheck`
- `npm --prefix web-ui run typecheck`
- `npm --prefix web-ui run test -- board-state`

## Difficulty
Medium

## Dependencies
- F7-04
- F7-05

## Recommended Owner
Codex

