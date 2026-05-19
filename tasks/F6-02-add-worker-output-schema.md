# F6-02 Add Worker Output Schema

## Goal
Define structured worker task result format.

## Files To Read
- `src/core/api-contract.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add schema for worker task result.
2. Include summary, explanation, proposed patch text, changed files, follow-up questions, test suggestions, and confidence.
3. Keep this separate from patch proposal persistence.

## Forbidden Changes
- Do not call models.
- Do not apply patches.

## Acceptance Criteria
- Worker result schema compiles.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- F6-01

## Recommended Owner
Smaller local model

