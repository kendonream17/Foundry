# F3-01 Add PromptRun Schema

## Goal
Add schema types for logging model prompts and responses.

## Files To Read
- `src/core/api-contract.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add `runtimePromptRunSchema`.
2. Include `id`, `workspaceId`, `taskId`, `role`, `modelProfileId`, `prompt`, `response`, `status`, timestamps, and optional `contextBundleId`.
3. Export inferred type.

## Forbidden Changes
- Do not add persistence yet.
- Do not change task session schemas.

## Acceptance Criteria
- Schema compiles and is exported.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- F2-01

## Recommended Owner
Smaller local model

