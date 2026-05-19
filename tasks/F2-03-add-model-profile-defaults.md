# F2-03 Add Model Profile Defaults

## Goal
Create a small helper that derives default model profiles from runtime config.

## Files To Read
- `src/core/api-contract.ts`
- `src/config/runtime-config.ts`

## Files To Modify
- `src/agents/model-profiles.ts`
- Optional test file under `test/` or `src/agents/`

## Exact Instructions
1. Create `src/agents/model-profiles.ts`.
2. Export a function that returns default local Ollama model profile placeholders from runtime config.
3. Do not require Ollama model discovery in this task.

## Forbidden Changes
- Do not add API routes.
- Do not modify UI.

## Acceptance Criteria
- Helper compiles and returns stable defaults.

## Tests / Checks
- `npm run typecheck`
- Add/run focused unit test if practical

## Difficulty
Low

## Dependencies
- F2-01
- F2-02

## Recommended Owner
Smaller local model

