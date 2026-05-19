# F5-01 Add Ollama HTTP Client

## Goal
Add a typed backend client for local Ollama.

## Files To Read
- `src/config/runtime-config.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/ollama/ollama-client.ts`
- Optional test file

## Exact Instructions
1. Create `src/ollama/ollama-client.ts`.
2. Implement typed functions for listing models via `/api/tags` and chat/generate via Ollama API.
3. Accept base URL as an explicit parameter.
4. Add timeout/error handling.

## Forbidden Changes
- Do not wire into task execution yet.
- Do not add UI.

## Acceptance Criteria
- Client compiles and can be unit tested with mocked fetch.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F2-02

## Recommended Owner
Smaller local model

