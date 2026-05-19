# Local Agent Fork Roadmap

This roadmap describes the planned conversion of Kanban into a personal Ubuntu-first local-agent IDE/orchestrator. It is intentionally implementation-oriented and references the current codebase so work can be assigned as small, low-risk tasks.

Some foundation tasks have now been implemented. The current task status index lives in `tasks/README.md`.

## Goals

- Use the web UI as the visual control layer.
- Let the backend orchestrate planning, task generation, worker assignment, proposed diffs, review, test runs, and fix loops.
- Prioritize Ubuntu 22.04+.
- Keep existing Kanban project, board, worktree, diff, and terminal behavior usable while new systems are added.
- Optimize local LLM workflows by sending narrow task-specific context to Ollama workers.
- Require user approval before mutating files.

## Current Codebase Map

### Frontend

- App entry: `web-ui/src/App.tsx`.
- Board UI: `web-ui/src/components/kanban-board.tsx`, `web-ui/src/components/board-card.tsx`.
- Detail view: `web-ui/src/components/card-detail-view.tsx`.
- Task create/edit state: `web-ui/src/hooks/use-task-editor.ts`.
- Runtime task actions: `web-ui/src/hooks/use-task-sessions.ts`.
- Cline task chat panel: `web-ui/src/components/detail-panels/cline-agent-chat-panel.tsx`.
- PTY terminal panel: `web-ui/src/components/detail-panels/agent-terminal-panel.tsx`.
- Diff panel: `web-ui/src/components/detail-panels/diff-viewer-panel.tsx`.
- Shared diff renderer: `web-ui/src/components/shared/diff-renderer.tsx`.
- Project navigation: `web-ui/src/components/project-navigation-panel.tsx`.
- Runtime state stream hook: `web-ui/src/runtime/use-runtime-state-stream.ts`.
- Task agent/model picker: `web-ui/src/components/task-agent-model-picker.tsx`.

### Backend

- Runtime HTTP/tRPC/websocket server: `src/server/runtime-server.ts`.
- Live runtime state fanout: `src/server/runtime-state-hub.ts`.
- Workspace/project registry: `src/server/workspace-registry.ts`.
- tRPC router and context: `src/trpc/app-router.ts`.
- Runtime coordinator: `src/trpc/runtime-api.ts`.
- Project API: `src/trpc/projects-api.ts`.
- Workspace/git API: `src/trpc/workspace-api.ts`.
- Shared API/data schemas: `src/core/api-contract.ts`.

### Tasks And Cards

- Runtime card schema: `runtimeBoardCardSchema` in `src/core/api-contract.ts`.
- Frontend card type: `BoardCard` in `web-ui/src/types/board.ts`.
- Board state helpers: `web-ui/src/state/board-state.ts`.
- Task cards currently store prompt, title, base ref, task agent override, Cline settings, review options, images, and timestamps.

### Agents

- Agent IDs: `runtimeAgentIdSchema` in `src/core/api-contract.ts`.
- Agent catalog: `src/core/agent-catalog.ts`.
- Agent detection/command resolution: `src/terminal/agent-registry.ts`.
- Launch routing: `createRuntimeApi().startTaskSession` in `src/trpc/runtime-api.ts`.
- PTY-backed agents: `TerminalSessionManager.startTaskSession` in `src/terminal/session-manager.ts`.
- Native Cline sessions: `InMemoryClineTaskSessionService` in `src/cline-sdk/cline-task-session-service.ts`.
- CLI launch adapters: `prepareAgentLaunch` in `src/terminal/agent-session-adapters.ts`.

### Terminals

- PTY wrapper: `src/terminal/pty-session.ts`.
- PTY session lifecycle: `src/terminal/session-manager.ts`.
- Terminal websocket bridge: `src/terminal/ws-server.ts`.
- Frontend terminal persistence: `web-ui/src/terminal/persistent-terminal-manager.ts`.

### Git Worktrees

- Worktree lifecycle: `src/workspace/task-worktree.ts`.
- Main functions: `ensureTaskWorktreeIfDoesntExist`, `deleteTaskWorktree`, `resolveTaskCwd`, `getTaskWorkspaceInfo`.
- Path helpers: `src/workspace/task-worktree-path.ts`.
- Current task worktrees live under `~/.cline/worktrees/<taskId>/<workspace-folder>`.

### Diffs And Reviews

- Working-copy and last-turn diffs: `src/workspace/get-workspace-changes.ts`.
- Workspace diff API: `loadChanges` in `src/trpc/workspace-api.ts`.
- Commit diffs: `getCommitDiff` in `src/workspace/git-history.ts`.
- Diff query hook: `web-ui/src/runtime/use-runtime-workspace-changes.ts`.
- Diff review UI: `web-ui/src/components/detail-panels/diff-viewer-panel.tsx`.

### Project State

- Workspace state persistence: `src/state/workspace-state.ts`.
- Runtime home: `~/.cline/kanban`.
- Workspace state root: `~/.cline/kanban/workspaces`.
- Per-workspace state files: `board.json`, `sessions.json`, `meta.json`.
- Runtime config: `src/config/runtime-config.ts`.
- Global config path: `~/.cline/kanban/config.json`.
- Project config path: `.cline/kanban/config.json` under project root.

## Feature Gap Analysis

### Already Exists Or Reusable

- Local project list/import/remove through `src/trpc/projects-api.ts`.
- Git clone/import support through `cloneGitRepository`.
- Git worktree isolation for task execution.
- Kanban board, card editing, and task movement.
- Per-task agent selection through `agentId`.
- Runtime state websocket updates.
- Terminal output and command execution infrastructure.
- Working-copy and last-turn diff rendering.
- Review comments routed into terminal or Cline chat.

### Partially Exists

- Plan mode exists as a Cline task-session mode, but not as project-level planning.
- Model/provider settings exist for Cline, but not generic model roles or Ollama.
- Task generation is manual, not Architect-driven.
- Diffs assume files are already changed in a worktree.
- Runtime summaries support task activity but not worker/node status.
- Project import exists, but UI still reflects upstream Cline product framing.

### Missing

- Project-level Plan Mode chat.
- Architect Mode task-card generation.
- Ollama client/provider.
- Local worker node service.
- Remote worker protocol.
- Worker assignment and heartbeat.
- Context bundle builder.
- Prompt preview and prompt/response logs.
- Patch proposal persistence and approval/application.
- Test run persistence and fix-loop generation.
- Project rules and off-limits files.
- Project index/database and long-term RAG support.

### Dangerous To Change Early

- `src/workspace/task-worktree.ts`: preserves existing worktrees and trashed patches.
- `src/cline-sdk/`: adapts SDK-managed provider, OAuth, session, and history behavior.
- `src/terminal/session-manager.ts`: handles PTY lifecycle, auto-restart, trust prompts, checkpoints.
- `src/terminal/ws-server.ts`: handles terminal websocket backpressure.
- `src/server/runtime-state-hub.ts`: controls live UI state synchronization.
- Existing `RuntimeTaskSessionSummary` state meanings because board auto-moves depend on them.

### Defer

- Remote workers.
- Embeddings/RAG.
- Drag-and-drop worker assignment.
- Autopilot.
- Multi-node scheduling.
- Full Git history intelligence.
- Multi-user/product-grade security.

## Recommended Architecture

Add new orchestration systems alongside existing Cline and PTY paths.

Recommended new backend areas:

- `src/agents/`: role/model abstractions such as `AgentRole` and `ModelProfile`.
- `src/ollama/`: Ollama HTTP client and model discovery.
- `src/workers/`: worker registry, local Ollama worker, future remote worker protocol.
- `src/context/`: project scanner, context bundle builder, framework detection.
- `src/prompt-runs/`: prompt preview and prompt/response persistence.
- `src/patches/`: patch proposal storage, validation, and application.
- `src/test-runs/`: test execution and result capture.

Recommended new frontend areas:

- `web-ui/src/components/workers/`
- `web-ui/src/components/prompt-preview/`
- `web-ui/src/components/project-rules/`
- `web-ui/src/components/project-chat/`

Plan Mode should be project-scoped. Architect Mode should share the same chat surface, compile Plan context, and generate structured card drafts. Ollama workers should be treated as worker nodes, not as PTY agents. Patch application should be backend-owned and user-approved.

Completed task handling should be explicit. When a task is finished and any approved patch/test flow is done, the user must be able to either mark the card as complete for history/audit purposes or delete/archive it if they do not want it retained on the board.

## Data Model Additions

- `AgentRole`: `plan`, `architect`, `worker`, `reviewer`, `tester`.
- `ModelProfile`: provider/model/context role settings.
- `WorkerNode`: local or remote worker, heartbeat, Ollama URL, models, current task.
- `ContextBundle`: task-scoped file/context bundle with token estimate.
- `PromptRun`: exact prompt/context/response log.
- `PatchProposal`: worker-proposed patch and explanation.
- `ReviewResult`: Architect/Reviewer verdict and comments.
- `TestRun`: command, output, status, exit code.
- `ProjectRule`: off-limits globs, preferred test commands, context include/exclude globs.
- `FileIndexEntry`: file path, language, framework hints, summary, mtime, off-limits flag.

Extend `RuntimeBoardCard` later with additive optional fields:

- `assignedWorkerId`
- `workerModelProfileId`
- `taskStatus`, including at least active, completed, and deleted/archived-style terminal states
- `parentTaskId`
- `sourcePromptRunId`
- `contextBundleId`

## API Boundary Plan

Project and rules:

- `project.scan.start`
- `project.scan.status`
- `project.rules.get`
- `project.rules.save`

Plan and Architect:

- `chat.start`
- `chat.send`
- `architect.generateTasks`
- `architect.createCards`

Workers:

- `workers.list`
- `workers.local.ensureStarted`
- `workers.heartbeat`
- `workers.assignTask`
- `workers.startTask`
- `workers.pauseTask`
- `workers.resumeTask`
- `workers.cancelTask`

Context and prompts:

- `context.previewForTask`
- `context.buildBundle`
- `promptRuns.get`
- `promptRuns.list`

Patch and tests:

- `patches.submit`
- `patches.validate`
- `patches.apply`
- `tests.run`
- `tests.createFixTask`
- `tasks.complete`
- `tasks.delete`

## UI Roadmap

- Project dropdown/import: reuse existing project APIs and add Ubuntu-first local path/GitHub import flow.
- Mode-switching chat: project-level Plan/Architect panel.
- Prompt/context preview: modal or panel before model calls and worker starts.
- Task board: add worker assignment/status/proposal/test state, plus a clear completion choice: mark complete or delete/archive task.
- Worker status panel: show machine, online/offline, Ollama URL, models, current task, basic timing/status.
- Diff/review panel: add patch-proposal diff source alongside existing worktree diff.
- Terminal/test output panel: read-only `TestRun` output plus existing terminal.
- Project rules/settings: off-limits globs, context limits, test commands, Ollama URL.

## Worker Design

MVP:

- One local Ollama worker.
- One task at a time.
- Backend calls Ollama directly.
- Worker receives task instructions plus a narrow context bundle.
- Worker returns structured JSON plus proposed patch.
- Worker reports status through runtime state.

Future:

- Remote worker service.
- Worker registration token.
- Heartbeat with machine name, models, and basic capabilities.
- Multiple model profiles per node.
- Routing recommendations, but user assignment remains primary.

## Context Management

- Scan project files and summarize language/framework structure.
- Apply off-limits rules before indexing or prompt construction.
- Use task prompt, current diffs, filename matching, imports, and user-selected files for MVP relevance.
- Add token/character estimates.
- Always preview exact prompt and file list.
- Keep Plan mode broader and Worker mode narrow.
- Defer embeddings until file summaries and basic relevance are stable.

## Safety Design

- Worker output is a proposal, not an automatic mutation.
- Validate patches with path guards and `git apply --check`.
- Require explicit user approval before apply.
- Store prompt, response, context bundle, patch, approval, and test logs.
- Prevent edits outside repo root.
- Enforce project off-limits globs.
- Capture pre-apply Git status and base commit.
- Prefer applying to a task worktree first.

## Phases

### Phase 0: Baseline Audit And Setup

Document fork goals and preserve current fragile behavior with audit notes and regression tests before source edits.

### Phase 1: Project Selection And Import Foundation

Reuse and refine project import/list/remove. Add project rules persistence.

### Phase 2: Model And Role Abstraction

Add generic role/model data types and Ollama config without changing Cline behavior.

### Phase 3: Prompt And Context Preview

Add prompt preview storage/API/UI for current task runs before introducing worker execution.

### Phase 4: Architect Task Generation

Add project-level Plan/Architect chat and convert Architect output into approved task cards.

### Phase 5: Local Ollama Worker Provider

Add Ollama client, local worker registry, model discovery, and single-worker status.

### Phase 6: Structured Worker Result And Patch Proposal

Worker returns structured output and patch proposals. Store and render proposals.

### Phase 7: Approval, Apply, And Test Loop

Validate/apply approved patches, run tests, and create fix task drafts on failure.

### Phase 8: Worker Status Panel

Expose worker/node status in UI and task cards.

### Phase 9: Project Indexing And Context Optimizer

Add file index, framework detection, summaries, relevance builder, and project rules.

### Phase 10: Remote Workers

Add registration, heartbeat, remote execution protocol, and capability reporting.

### Phase 11: Advanced UI And Assignment

Add drag/drop assignment, split/merge task cards, and richer worker board UI.

### Phase 12: Optional Autopilot

Add disabled-by-default automation policies after manual flow is reliable.

## MVP Definition

The smallest proof loop:

1. Select/import an existing Git project.
2. Chat in project-level Plan/Architect mode.
3. Generate one task draft.
4. Create one task card.
5. Assign it to one local Ollama worker.
6. Preview exact prompt/context.
7. Worker returns structured result and proposed patch.
8. UI shows the patch diff.
9. User approves.
10. Backend validates and applies the patch.
11. Backend runs one configured test command.
12. If tests pass, user chooses whether to mark the task complete or delete/archive it.
13. If tests fail, app creates one follow-up fix task draft.

## Task Files

Atomic implementation tasks are stored in `tasks/`. Each file includes scope, exact read/modify paths, forbidden changes, acceptance criteria, checks, dependencies, difficulty, and recommended owner.
