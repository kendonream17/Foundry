# F9-01 Add FileIndexEntry Schema

## Goal
Define project file index entries for future context optimization.

## Files To Read
- `src/core/api-contract.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add `runtimeFileIndexEntrySchema`.
2. Include path, language, framework hints, symbols, summary, mtime, size, and off-limits flag.
3. Export inferred type.

## Forbidden Changes
- Do not implement scanning yet.

## Acceptance Criteria
- Schema compiles and is exported.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- F1-02

## Recommended Owner
Smaller local model

