# F9-03 Add Framework Detector

## Goal
Detect basic language/framework hints for a project.

## Files To Read
- `package.json`
- `web-ui/package.json`
- `src/workspace/search-workspace-files.ts`

## Files To Modify
- `src/context/framework-detect.ts`
- Optional test file

## Exact Instructions
1. Detect common project markers: Node package, Vite, React, TypeScript, Python, Rust, Go.
2. Return structured hints.
3. Keep this read-only.

## Forbidden Changes
- Do not install dependencies.
- Do not shell out unless necessary.

## Acceptance Criteria
- Detector returns useful hints for this repo.

## Tests / Checks
- `npm run typecheck`
- Focused vitest if added

## Difficulty
Low

## Dependencies
- F9-01

## Recommended Owner
Smaller local model

