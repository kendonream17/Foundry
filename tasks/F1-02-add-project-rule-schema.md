# F1-02 Add ProjectRule Schema

## Goal
Add API-contract types for project-specific rules such as off-limits globs and test commands.

## Files To Read
- `src/core/api-contract.ts`
- `src/core/api-validation.ts`
- `src/trpc/workspace-api.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add a `runtimeProjectRuleSchema` or equivalent project-rules schema.
2. Include fields for `offLimitsGlobs`, `contextIncludeGlobs`, `contextExcludeGlobs`, `preferredTestCommands`, and `updatedAt`.
3. Export inferred TypeScript type.
4. Keep the schema additive.

## Forbidden Changes
- Do not change existing board, session, or config schemas.
- Do not add runtime behavior.

## Acceptance Criteria
- TypeScript exports a project rules type.
- Existing schemas remain backward-compatible.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Medium

## Dependencies
- None

## Recommended Owner
Codex

