# F8-02 Add Worker Card Details

## Goal
Show useful worker details in the worker status panel.

## Files To Read
- `web-ui/src/components/workers/worker-status-panel.tsx`
- `src/core/api-contract.ts`

## Files To Modify
- `web-ui/src/components/workers/worker-status-panel.tsx`

## Exact Instructions
1. Show machine name, online/offline status, Ollama URL, model names, current task, and last heartbeat age.
2. Keep cards compact and consistent with existing dark UI tokens.
3. Use Lucide icons where helpful.

## Forbidden Changes
- Do not add remote worker controls yet.
- Do not add drag/drop.

## Acceptance Criteria
- Worker cards display all required MVP fields.

## Tests / Checks
- `npm --prefix web-ui run typecheck`

## Difficulty
Low

## Dependencies
- F8-01

## Recommended Owner
Smaller local model

