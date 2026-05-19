# F6-05 Render Patch Proposal Diff

## Goal
Show a stored patch proposal in the existing diff/review UI.

## Files To Read
- `web-ui/src/components/detail-panels/diff-viewer-panel.tsx`
- `web-ui/src/components/shared/diff-renderer.tsx`
- `web-ui/src/components/git-history/git-commit-diff-panel.tsx`
- `src/workspace/get-workspace-changes.ts`

## Files To Modify
- New proposal diff adapter/component under `web-ui/src/components/detail-panels/` or `web-ui/src/components/patches/`
- Minimal integration file selected after reading current detail panel flow

## Exact Instructions
1. Add an adapter that converts a patch proposal into file diff display data.
2. Reuse the existing diff renderer.
3. Show proposal status and summary.
4. Do not add approval/apply actions in this task.

## Forbidden Changes
- Do not modify backend patch application.
- Do not remove current working-copy diff.

## Acceptance Criteria
- A patch proposal can be displayed as a read-only diff source.

## Tests / Checks
- `npm --prefix web-ui run typecheck`
- Focused web test if practical

## Difficulty
High

## Dependencies
- F6-04

## Recommended Owner
Codex

