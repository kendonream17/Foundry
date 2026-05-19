# F5-03 Add Worker Registry Service

## Goal
Create an in-memory backend registry for worker nodes.

## Files To Read
- `src/server/workspace-registry.ts`
- `src/server/runtime-state-hub.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/workers/worker-registry.ts`
- Optional test file

## Exact Instructions
1. Create `src/workers/worker-registry.ts`.
2. Support list, upsert heartbeat, set current task, clear current task, and mark stale workers offline.
3. Keep it workspace-independent for MVP unless a workspace ID is explicitly needed.

## Forbidden Changes
- Do not add networking.
- Do not call Ollama.

## Acceptance Criteria
- Registry can track one local worker and multiple future workers.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F5-02

## Recommended Owner
Codex

