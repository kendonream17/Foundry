# F1-03 Persist Project Rules JSON

## Goal
Persist project rules as a workspace-scoped JSON file.

## Files To Read
- `src/state/workspace-state.ts`
- `src/fs/locked-file-system.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/state/workspace-state.ts`
- tests only if needed under `test/` or existing relevant test location

## Exact Instructions
1. Add a workspace rules file path helper near existing board/session/meta helpers.
2. Add load and save helpers for project rules.
3. Use existing locked atomic JSON write patterns.
4. Return default empty rules when missing.

## Forbidden Changes
- Do not change board/session persistence behavior.
- Do not migrate existing state files.

## Acceptance Criteria
- Missing rules file loads default rules.
- Save writes valid JSON atomically.
- Existing workspace state load/save behavior is unchanged.

## Tests / Checks
- `npm run typecheck`
- Relevant `vitest` state tests if added

## Difficulty
Medium

## Dependencies
- F1-02

## Recommended Owner
Codex

