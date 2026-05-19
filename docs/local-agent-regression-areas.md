# Local Agent Regression Areas

This document lists current behavior that should be protected while building the local-agent fork. These areas are central to existing Kanban behavior and should not be refactored casually.

## Worktree Lifecycle

Primary file: `src/workspace/task-worktree.ts`.

Important invariants:

- `ensureTaskWorktreeIfDoesntExist` treats an existing valid task worktree as authoritative.
- Existing worktrees are not recreated just because the base branch advanced.
- Worktree setup is guarded by a lock through `withTaskWorktreeSetupLock`.
- `deleteTaskWorktree` captures pending changes as a patch before removal when possible.
- Trashed task patches are restored when a worktree is recreated.
- Ignored paths are mirrored/symlinked into worktrees carefully and `.git`-like paths are skipped.
- Task IDs are normalized through `normalizeTaskIdForWorktreePath`.

Regression tests to add before changing this area:

- Existing worktree is reused and not reset.
- Missing worktree is created from base ref.
- Deleting a dirty worktree stores a patch.
- Recreating a deleted dirty task reapplies the patch when possible.
- Invalid task IDs cannot escape the worktree root.

## Runtime Session Routing

Primary file: `src/trpc/runtime-api.ts`.

Important invariants:

- `startTaskSession` resolves task cwd before launch using `resolveExistingTaskCwdOrEnsure`.
- Effective agent precedence is previous session agent on trash restore, task-level `agentId`, then workspace selected agent.
- Cline launches use `ClineTaskSessionService`.
- Non-Cline launches use `TerminalSessionManager`.
- Cline persisted-session probing is intentionally skipped when a concrete previous non-Cline agent is known.
- Turn checkpoints are best effort and should not break session start.

Regression tests to add:

- Cline task routes to Cline service.
- Non-Cline task routes to terminal manager.
- Resume-from-trash uses previous agent ID when present.
- Failed worktree resolution returns a failed start response without crashing.

## Runtime State Streaming

Primary file: `src/server/runtime-state-hub.ts`.

Important invariants:

- Terminal and Cline summaries are batched through `queueTaskSessionSummaryBroadcast`.
- Initial websocket snapshot is sent before the socket is registered for incremental workspace metadata messages.
- Workspace metadata monitor connect/disconnect is paired with websocket lifecycle.
- Cline summary transitions to `awaiting_review` can broadcast task-ready notifications.
- Checkpoint changes trigger workspace state refresh broadcasts.

Regression tests to add:

- Initial stream sends snapshot before incremental metadata updates.
- Batched task session summaries are delivered once per task per flush.
- Disposing a workspace unregisters terminal/Cline listeners.
- Cline transition to awaiting review emits ready-for-review notification.

## Terminal Session Manager

Primary file: `src/terminal/session-manager.ts`.

Important invariants:

- PTY sessions preserve summary state and emit updates through `onSummary`.
- `writeInput` routes bytes to the active PTY only.
- Terminal restore snapshots are managed by `TerminalStateMirror`.
- Auto-restart has rate limiting.
- Codex and Claude trust prompt handling is special-cased and timing-sensitive.
- `recoverStaleSession` preserves `agentId` so restore routing can choose the correct agent type.

Regression tests to add:

- Starting a task emits a running summary.
- Process exit emits idle/awaiting-review/interrupted according to state machine behavior.
- Stale active summary can recover to idle without losing agent ID.
- Stop marks interrupted where expected.

## Native Cline Integration

Primary directory: `src/cline-sdk/`.

Important invariants:

- Cline provider settings and secrets are SDK-owned, not runtime-config-owned.
- `InMemoryClineTaskSessionService` maps SDK sessions to Kanban task summaries and chat messages.
- Cline messages are streamed through `runtime-state-hub.ts`.
- Persisted Cline sessions can be rebound for task history/resume.

Regression tests to add:

- Loading persisted Cline messages still works.
- Sending Cline task chat message emits summary and latest message.
- Cline provider settings save path does not write secrets into Kanban runtime config.

## Project Import And Registry

Primary files:

- `src/trpc/projects-api.ts`
- `src/server/workspace-registry.ts`
- `src/state/workspace-state.ts`

Important invariants:

- `projects.addProject` supports local path and Git URL.
- Non-Git paths require explicit initialization.
- Existing Git repositories are ensured to have an initial commit.
- Project removal disposes sessions, removes workspace state, and cleans task worktrees best effort.
- Workspace registry hydrates terminal managers from persisted sessions.

Regression tests to add:

- Adding an existing Git repo creates/loads a workspace context.
- Adding a non-Git repo without initialization returns `requiresGitInitialization`.
- Removing a project disposes managed workspace state.

## Diff And Review

Primary files:

- `src/workspace/get-workspace-changes.ts`
- `src/workspace/git-history.ts`
- `web-ui/src/components/detail-panels/diff-viewer-panel.tsx`

Important invariants:

- Working-copy diff includes tracked and untracked files.
- Last-turn mode uses turn checkpoints when available.
- Missing task worktree returns an empty diff rather than breaking the UI.
- Commit diff parsing supports name/status, numstat, and patch display.

Regression tests to add:

- Modified, added, deleted, renamed, and untracked files render as expected.
- Last-turn diff falls back correctly when there is no previous checkpoint.
- Missing task worktree returns an empty changes response.

## Rules For Early Fork Work

- Add new systems alongside existing ones.
- Prefer additive schemas and optional fields.
- Preserve old persisted state compatibility.
- Do not remove `trash` column behavior until completion/delete disposition is separately implemented and tested.
- Do not auto-apply model output.
- Do not bypass worktree cleanup helpers.

