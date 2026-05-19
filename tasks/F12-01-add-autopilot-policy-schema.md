# F12-01 Add Autopilot Policy Schema

## Goal
Define disabled-by-default autopilot policy settings for later automation.

## Files To Read
- `src/core/api-contract.ts`
- `src/config/runtime-config.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add an autopilot policy schema with fields for enabled flag, allowed actions, max loop count, and approval requirements.
2. Default should be disabled.
3. Do not wire it into config yet unless explicitly scoped later.

## Forbidden Changes
- Do not enable autopilot behavior.
- Do not auto-apply patches.

## Acceptance Criteria
- Schema compiles and makes automation opt-in.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- None

## Recommended Owner
Smaller local model

