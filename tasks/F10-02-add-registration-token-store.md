# F10-02 Add Registration Token Store

## Goal
Create storage and validation for future remote worker registration tokens.

## Files To Read
- `src/security/passcode-manager.ts`
- `src/config/runtime-config.ts`
- `src/fs/locked-file-system.ts`

## Files To Modify
- `src/workers/worker-registration-token-store.ts`
- Optional test file

## Exact Instructions
1. Add create/list/revoke/validate token helpers.
2. Store hashed tokens only.
3. Keep token store independent of passcode manager.

## Forbidden Changes
- Do not expose API yet.
- Do not weaken existing passcode behavior.

## Acceptance Criteria
- Tokens can be created and validated in tests.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F10-01

## Recommended Owner
Codex

