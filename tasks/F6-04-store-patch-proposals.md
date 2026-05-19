# F6-04 Store Patch Proposals

## Goal
Persist patch proposals for review and later approval.

## Files To Read
- `src/state/workspace-state.ts`
- `src/core/api-contract.ts`
- `src/fs/locked-file-system.ts`

## Files To Modify
- `src/patches/patch-proposal-store.ts`
- `src/state/workspace-state.ts` if path helpers belong there
- Optional test file

## Exact Instructions
1. Add workspace-scoped storage for patch proposals.
2. Support list, get, create, update status.
3. Use atomic JSON write patterns.
4. Keep proposals independent of board state.

## Forbidden Changes
- Do not apply patches.
- Do not alter existing diff generation.

## Acceptance Criteria
- Patch proposals can be persisted and retrieved by task ID.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F6-01

## Recommended Owner
Codex

