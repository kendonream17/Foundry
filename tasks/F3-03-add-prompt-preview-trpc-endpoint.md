# F3-03 Add Prompt Preview tRPC Endpoint

## Goal
Expose prompt preview generation to the web UI.

## Files To Read
- `src/trpc/app-router.ts`
- `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`
- `src/prompt-runs/prompt-preview.ts`

## Files To Modify
- `src/trpc/app-router.ts`
- `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`

## Exact Instructions
1. Add request/response schemas for task prompt preview.
2. Add `runtime.previewTaskPrompt` or similarly named procedure.
3. Delegate prompt formatting to `src/prompt-runs/prompt-preview.ts`.

## Forbidden Changes
- Do not change `runtime.startTaskSession`.
- Do not require UI callers yet.

## Acceptance Criteria
- tRPC endpoint compiles.
- Endpoint returns prompt text and estimate.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Medium

## Dependencies
- F3-02

## Recommended Owner
Codex

