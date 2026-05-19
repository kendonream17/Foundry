# F5-02 Add Local Worker Schemas

## Goal
Add worker node and worker status contracts.

## Files To Read
- `src/core/api-contract.ts`
- `src/server/runtime-state-hub.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add schemas for `WorkerNode`, `WorkerStatus`, and worker model info.
2. Include fields for machine name, kind, online/offline status, Ollama URL, models, current task, last heartbeat, and simple metrics.
3. Export types.

## Forbidden Changes
- Do not change runtime state stream yet.
- Do not change agent IDs.

## Acceptance Criteria
- Worker types compile and are additive.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- F2-01

## Recommended Owner
Smaller local model

