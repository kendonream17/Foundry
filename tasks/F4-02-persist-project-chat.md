# F4-02 Persist Project Chat

## Goal
Persist project-level Plan/Architect conversations.

## Files To Read
- `src/state/workspace-state.ts`
- `src/fs/locked-file-system.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/state/workspace-state.ts`
- Optional test file

## Exact Instructions
1. Add workspace-scoped project chat file path helper.
2. Add load/save/list helpers.
3. Use atomic JSON writes and existing lock patterns.
4. Default to empty conversations.

## Forbidden Changes
- Do not alter `board.json` or `sessions.json`.
- Do not add model calls.

## Acceptance Criteria
- Project chat can be loaded and saved independently of board state.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F4-01

## Recommended Owner
Codex

