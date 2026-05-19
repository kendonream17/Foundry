# F8-03 Add Task Assignment Dropdown

## Goal
Allow user to assign a task to a worker from a dropdown.

## Files To Read
- `web-ui/src/components/task-agent-model-picker.tsx`
- `web-ui/src/components/task-inline-create-card.tsx`
- `web-ui/src/hooks/use-task-editor.ts`
- `web-ui/src/types/board.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/core/api-contract.ts`
- `web-ui/src/types/board.ts`
- `web-ui/src/hooks/use-task-editor.ts`
- UI component selected after reading picker structure

## Exact Instructions
1. Add optional `assignedWorkerId` to task card schema/types.
2. Add dropdown using workers list.
3. Save worker assignment on task create/edit.
4. Keep agent selection separate from worker assignment.

## Forbidden Changes
- Do not remove `agentId`.
- Do not add drag/drop assignment.
- Do not start workers automatically.

## Acceptance Criteria
- Created/edited cards can store assigned worker ID.
- Existing cards without assignment still load.

## Tests / Checks
- `npm run typecheck`
- `npm --prefix web-ui run typecheck`
- Board-state tests if updated

## Difficulty
Medium

## Dependencies
- F5-04
- F8-01

## Recommended Owner
Codex

