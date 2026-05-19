# F5-04 Add Workers tRPC Router

## Goal
Expose worker listing and heartbeat through tRPC.

## Files To Read
- `src/trpc/app-router.ts`
- `src/server/runtime-server.ts`
- `src/workers/worker-registry.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/trpc/app-router.ts`
- `src/server/runtime-server.ts`
- `src/trpc/workers-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`

## Exact Instructions
1. Add a new workers API module.
2. Add `workers.list` and `workers.heartbeat`.
3. Instantiate/share the worker registry from runtime server dependencies.
4. Keep auth/security consistent with existing local runtime APIs.

## Forbidden Changes
- Do not add remote worker registration yet.
- Do not modify project APIs.

## Acceptance Criteria
- UI can query workers list.
- Heartbeat updates registry.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Medium

## Dependencies
- F5-03

## Recommended Owner
Codex

