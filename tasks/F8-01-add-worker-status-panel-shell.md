# F8-01 Add Worker Status Panel Shell

## Goal
Add a basic UI panel that lists worker nodes from the workers API.

## Files To Read
- `web-ui/src/App.tsx`
- `web-ui/src/components/project-navigation-panel.tsx`
- `web-ui/src/runtime/trpc-client.ts`
- `web-ui/src/runtime/use-trpc-query.ts`

## Files To Modify
- `web-ui/src/components/workers/worker-status-panel.tsx`
- Minimal layout integration file selected after reading `App.tsx`

## Exact Instructions
1. Create a worker status panel component.
2. Query `workers.list`.
3. Render loading, empty, and list states.
4. Keep layout minimal.

## Forbidden Changes
- Do not redesign the whole app layout.
- Do not add assignment behavior yet.

## Acceptance Criteria
- Worker panel shows local worker when API returns one.

## Tests / Checks
- `npm --prefix web-ui run typecheck`

## Difficulty
Medium

## Dependencies
- F5-04

## Recommended Owner
Smaller local model

