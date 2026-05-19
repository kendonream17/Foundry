# F9-05 Add Context Preview UI

## Goal
Show context bundle details before sending work to a model.

## Files To Read
- `web-ui/src/components/prompt-preview/`
- `web-ui/src/components/detail-panels/diff-viewer-panel.tsx`
- `web-ui/src/hooks/use-task-sessions.ts`

## Files To Modify
- Prompt/context preview UI components
- Minimal integration file selected after reading current prompt preview flow

## Exact Instructions
1. Show included files, excluded files, token/character estimate, and warnings.
2. Let user cancel before model execution.
3. Keep UI read-only for MVP.

## Forbidden Changes
- Do not add file editing in preview.
- Do not bypass prompt preview confirmation.

## Acceptance Criteria
- User can inspect context bundle before worker execution.

## Tests / Checks
- `npm --prefix web-ui run typecheck`

## Difficulty
Medium

## Dependencies
- F9-04
- F3-04

## Recommended Owner
Codex

