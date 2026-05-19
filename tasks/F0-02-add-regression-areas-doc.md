# F0-02 Add Regression Areas Doc

## Goal
Document fragile existing behavior that should be protected before implementation begins.

## Files To Read
- `src/workspace/task-worktree.ts`
- `src/trpc/runtime-api.ts`
- `src/server/runtime-state-hub.ts`
- `src/terminal/session-manager.ts`
- `src/cline-sdk/cline-task-session-service.ts`

## Files To Modify
- `docs/local-agent-regression-areas.md`

## Exact Instructions
1. Create `docs/local-agent-regression-areas.md`.
2. List current invariants for worktree creation/deletion, task patch preservation, session summaries, Cline routing, PTY routing, and runtime state streaming.
3. Include suggested future regression tests but do not implement tests.

## Forbidden Changes
- Do not modify source code or tests.

## Acceptance Criteria
- The document identifies fragile areas and why they should not be touched early.

## Tests / Checks
- `git diff -- docs/local-agent-regression-areas.md`

## Difficulty
Low

## Dependencies
- None

## Recommended Owner
Smaller local model

