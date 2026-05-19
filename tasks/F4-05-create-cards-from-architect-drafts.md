# F4-05 Create Cards From Architect Drafts

## Goal
Convert approved Architect task drafts into backlog cards.

## Files To Read
- `web-ui/src/state/board-state.ts`
- `web-ui/src/hooks/use-task-editor.ts`
- `web-ui/src/components/task-inline-create-card.tsx`
- `src/core/api-contract.ts`

## Files To Modify
- `web-ui/src/state/board-state.ts`
- One UI/hook integration file chosen after reading current flow

## Exact Instructions
1. Add a helper that converts one or more Architect drafts into backlog cards.
2. Preserve existing card fields and defaults.
3. Require user approval from the UI before adding cards.
4. Do not auto-start generated tasks.

## Forbidden Changes
- Do not change drag/drop rules.
- Do not change existing manual task creation behavior.

## Acceptance Criteria
- Approved drafts create backlog cards.
- Manual task creation still works.

## Tests / Checks
- `npm --prefix web-ui run typecheck`
- Existing `board-state` tests

## Difficulty
Medium

## Dependencies
- F4-04

## Recommended Owner
Codex

