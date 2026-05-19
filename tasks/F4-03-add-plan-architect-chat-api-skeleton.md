# F4-03 Add Plan/Architect Chat API Skeleton

## Goal
Add tRPC procedures for project-level Plan/Architect chat with stub responses.

## Files To Read
- `src/trpc/app-router.ts`
- `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`
- `src/state/workspace-state.ts`

## Files To Modify
- `src/trpc/app-router.ts`
- `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`
- New focused service file if useful

## Exact Instructions
1. Add procedures for starting/listing a project chat and sending a message.
2. Store user messages using persistence from F4-02.
3. Return a deterministic stub assistant response.
4. Include selected mode: Plan or Architect.

## Forbidden Changes
- Do not call Ollama.
- Do not modify Cline chat behavior.

## Acceptance Criteria
- UI can call the API and receive stored messages plus a stub response.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Medium

## Dependencies
- F4-02

## Recommended Owner
Smaller local model

