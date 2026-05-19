# F4-01 Add Project Chat Data Model

## Goal
Add project-level chat/conversation schemas for Plan and Architect modes.

## Files To Read
- `src/core/api-contract.ts`
- Existing `runtimeTaskChatMessageSchema` in `src/core/api-contract.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add schemas for project chat conversation and message.
2. Include role/mode, workspace ID, message content, timestamps, model profile ID, and optional prompt run ID.
3. Reuse existing task chat concepts where practical, but keep this project-scoped.

## Forbidden Changes
- Do not modify Cline task chat schemas.
- Do not add persistence yet.

## Acceptance Criteria
- New schemas export TypeScript types.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- F2-01

## Recommended Owner
Smaller local model

