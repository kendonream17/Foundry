# F9-04 Add Context Bundle Builder

## Goal
Build task-specific context bundles for local workers.

## Files To Read
- `src/context/project-scanner.ts`
- `src/context/framework-detect.ts`
- `src/workspace/get-workspace-changes.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/context/context-bundle.ts`
- `src/core/api-contract.ts` if ContextBundle schema has not been added yet
- Optional test file

## Exact Instructions
1. Add `ContextBundle` schema if missing.
2. Select files based on task prompt, filenames, current diff paths, and project rules.
3. Include file snippets or full contents under a limit.
4. Return token/character estimate and exclusion notes.

## Forbidden Changes
- Do not add embeddings.
- Do not include off-limits files.
- Do not call models.

## Acceptance Criteria
- Builder produces a small deterministic bundle for a task.
- Bundle respects context limit and exclusions.

## Tests / Checks
- `npm run typecheck`
- Focused unit tests

## Difficulty
High

## Dependencies
- F9-02
- F9-03

## Recommended Owner
Codex

