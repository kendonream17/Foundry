# F5-05 Add Local Ollama Worker Discovery

## Goal
Register a local Ollama worker and discover available models.

## Files To Read
- `src/ollama/ollama-client.ts`
- `src/workers/worker-registry.ts`
- `src/config/runtime-config.ts`
- `src/server/runtime-server.ts`

## Files To Modify
- `src/workers/local-ollama-worker.ts`
- Integration point in `src/server/runtime-server.ts` or workers API setup

## Exact Instructions
1. Create a local worker service that probes the configured Ollama URL.
2. Register one local worker node with online/offline status.
3. Populate model list from Ollama when reachable.
4. Do not execute tasks.

## Forbidden Changes
- Do not start long-running loops without cleanup.
- Do not block runtime server startup if Ollama is offline.

## Acceptance Criteria
- Workers list shows one local worker.
- Offline Ollama is represented as offline rather than crashing.

## Tests / Checks
- `npm run typecheck`
- Focused mocked test if practical

## Difficulty
Medium

## Dependencies
- F5-01
- F5-04

## Recommended Owner
Codex

