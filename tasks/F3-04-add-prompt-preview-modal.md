# F3-04 Add Prompt Preview Modal

## Goal
Add a UI modal that shows exact prompt preview before an existing task run starts.

## Files To Read
- `web-ui/src/hooks/use-task-sessions.ts`
- `web-ui/src/components/card-detail-view.tsx`
- `web-ui/src/components/ui/dialog.tsx`
- `web-ui/src/runtime/trpc-client.ts`

## Files To Modify
- New component under `web-ui/src/components/prompt-preview/`
- `web-ui/src/hooks/use-task-sessions.ts` or caller-level UI integration files as appropriate

## Exact Instructions
1. Add a reusable prompt preview dialog component.
2. Query the prompt preview endpoint from F3-03.
3. Add confirm/cancel behavior before starting a task.
4. Keep the default path non-invasive and easy to disable if needed.

## Forbidden Changes
- Do not change backend model calls.
- Do not auto-start after cancel.
- Do not alter Cline provider UI.

## Acceptance Criteria
- Starting a task can show the preview and requires confirmation.
- Cancel prevents the task from starting.

## Tests / Checks
- `npm --prefix web-ui run typecheck`
- Relevant web tests if added

## Difficulty
Medium

## Dependencies
- F3-03

## Recommended Owner
Codex

