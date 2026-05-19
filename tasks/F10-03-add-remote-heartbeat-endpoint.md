# F10-03 Add Remote Heartbeat Endpoint

## Goal
Accept heartbeat updates from remote workers.

## Files To Read
- `src/trpc/workers-api.ts`
- `src/workers/worker-registry.ts`
- `src/workers/worker-registration-token-store.ts`

## Files To Modify
- `src/trpc/workers-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`

## Exact Instructions
1. Add a remote heartbeat mutation.
2. Require registration token validation.
3. Upsert worker node status and capabilities.
4. Keep local worker heartbeat working.

## Forbidden Changes
- Do not execute remote tasks yet.
- Do not expose token values in responses.

## Acceptance Criteria
- Valid token updates worker registry.
- Invalid token is rejected.

## Tests / Checks
- `npm run typecheck`
- Focused API/service test if practical

## Difficulty
Medium

## Dependencies
- F10-02

## Recommended Owner
Codex

