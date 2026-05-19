# F1-04 Add Project Rules API

## Goal
Expose project rules through workspace-scoped tRPC procedures.

## Files To Read
- `src/trpc/app-router.ts`
- `src/trpc/workspace-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`
- `src/state/workspace-state.ts`

## Files To Modify
- `src/trpc/app-router.ts`
- `src/trpc/workspace-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`

## Exact Instructions
1. Add request/response schemas for `getProjectRules` and `saveProjectRules`.
2. Add workspace API methods that call the persistence helpers from F1-03.
3. Add tRPC procedures under the workspace router.
4. Keep procedures workspace-scoped.

## Forbidden Changes
- Do not add UI.
- Do not change existing `saveState` or `loadState`.

## Acceptance Criteria
- tRPC types compile.
- Rules can be loaded and saved for a workspace.

## Tests / Checks
- `npm run typecheck`
- `npm run test -- workspace`

## Difficulty
Medium

## Dependencies
- F1-02
- F1-03

## Recommended Owner
Codex

