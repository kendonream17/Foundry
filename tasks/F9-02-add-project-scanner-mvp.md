# F9-02 Add Project Scanner MVP

## Goal
Create a basic scanner that lists project files and applies off-limits rules.

## Files To Read
- `src/workspace/search-workspace-files.ts`
- `src/workspace/path-sandbox.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/context/project-scanner.ts`
- Optional test file

## Exact Instructions
1. Create a scanner that walks project files.
2. Skip `.git`, `node_modules`, common build outputs, and project off-limits globs.
3. Infer language from extension.
4. Return `FileIndexEntry` records.

## Forbidden Changes
- Do not add embeddings.
- Do not read huge binary files.

## Acceptance Criteria
- Scanner returns stable file entries and respects exclusions.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Medium

## Dependencies
- F9-01

## Recommended Owner
Smaller local model

