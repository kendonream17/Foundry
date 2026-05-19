# F3-02 Add Prompt Preview Builder Skeleton

## Goal
Create a backend helper that can build a deterministic prompt preview for an existing task.

## Files To Read
- `src/trpc/runtime-api.ts`
- `src/core/api-contract.ts`
- `web-ui/src/hooks/use-task-sessions.ts`

## Files To Modify
- `src/prompt-runs/prompt-preview.ts`
- Optional focused test file

## Exact Instructions
1. Create `src/prompt-runs/prompt-preview.ts`.
2. Export a function that accepts task prompt, title, base ref, role, and optional context summary.
3. Return an object containing prompt text and a simple token/character estimate.
4. Do not call any model.

## Forbidden Changes
- Do not modify task start behavior.
- Do not add UI.

## Acceptance Criteria
- Function is deterministic and covered by a simple unit test if practical.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F3-01

## Recommended Owner
Smaller local model

