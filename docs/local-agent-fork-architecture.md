# Local Agent Fork Architecture

This document records the intended architecture for the Ubuntu-first local-agent fork. It is descriptive only; no implementation is implied by this file.

## Product Direction

The fork keeps Kanban's browser UI plus local runtime split, but changes the main workflow from "launch a coding agent in a task worktree" to "orchestrate local model work through explicit planning, task generation, worker assignment, proposed diffs, review, approval, and tests."

The target loop is:

1. User opens a local Git project.
2. Plan Mode discusses the desired change with broad project context.
3. Architect Mode converts the plan into precise task cards.
4. User assigns a task to a local or remote worker.
5. Worker receives a narrow context bundle and returns structured output.
6. Worker output becomes a patch proposal.
7. User reviews and approves the proposal.
8. Backend applies the patch and runs tests.
9. Failed tests generate follow-up fix task drafts.
10. Completed tasks can be marked complete for history or deleted/archived by user choice.

## Current Architecture To Preserve

Kanban already has the right high-level split:

- Browser UI in `web-ui/src`.
- Local runtime in `src`.
- Runtime API in `src/trpc/app-router.ts` and `src/trpc/runtime-api.ts`.
- Live state streaming in `src/server/runtime-state-hub.ts`.
- Git/worktree support in `src/workspace`.
- PTY process sessions in `src/terminal`.
- Native Cline SDK integration in `src/cline-sdk`.

The fork should keep the browser as a control surface. The local runtime should remain the source of truth for project state, sessions, worker status, patch proposals, and tests.

## New Runtime Areas

The fork should add new backend areas alongside existing Cline and PTY systems:

- `src/agents/`: shared role and model abstractions such as `AgentRole` and `ModelProfile`.
- `src/ollama/`: Ollama HTTP client, model discovery, request/response parsing.
- `src/workers/`: worker registry, local Ollama worker, future remote worker protocol.
- `src/context/`: project scanner, framework detection, context bundle builder.
- `src/prompt-runs/`: prompt preview and prompt/response persistence.
- `src/patches/`: patch proposal storage, validation, and application.
- `src/test-runs/`: test command execution and persisted output.

These areas should be additive. They should not move Cline SDK behavior into generic worker code and should not force local workers through the PTY terminal path.

## Plan And Architect Modes

Plan Mode should be project-scoped rather than task-scoped. It can scan or summarize broad project context and ask clarifying questions. It should store prompt runs and visible chat history in Kanban-owned state, not in Cline SDK state.

Architect Mode should share the project chat surface but use a different role prompt and output contract. Its primary output is structured task drafts that the user approves before creating cards.

The existing task chat path in `src/cline-sdk/cline-task-session-service.ts` should remain available for Cline-backed task sessions. New Plan/Architect state should not depend on Cline persisted sessions.

## Worker Model

Workers are execution nodes, not UI agents. MVP has one local Ollama worker:

- Backend probes the configured Ollama URL.
- Worker advertises available models.
- Worker runs one task at a time.
- Worker receives task instructions and a context bundle.
- Worker returns structured JSON plus a proposed patch.

Future remote workers should register with a token, heartbeat to the main runtime, report capabilities, and accept task execution requests. Main runtime remains the authority for patch validation and application.

## Context Bundles

The central performance goal is to avoid huge prompts. Context building should be explicit:

- Plan Mode may use broad project summaries.
- Workers receive narrow task-specific bundles.
- Bundles must respect project off-limits rules.
- Bundles should show file list, token/character estimate, and exclusions before model execution.
- RAG/embeddings are future enhancements, not MVP requirements.

## Patch Proposal Flow

Workers should not directly mutate the main repo in the long-term design. The safe path is:

1. Worker returns a proposed patch and explanation.
2. Backend stores a `PatchProposal`.
3. UI renders the proposal through the existing diff/review surface.
4. User explicitly approves.
5. Backend validates paths and runs `git apply --check`.
6. Backend applies the patch in the intended safe target.
7. Backend records the result and optionally runs tests.

This keeps mutation inside the local runtime, where path guards, off-limits rules, logs, and rollback strategy can be enforced.

## UI Surfaces

The fork should add these surfaces incrementally:

- Project selector and import screen.
- Project-level Plan/Architect chat.
- Prompt/context preview panel.
- Worker status panel.
- Task assignment dropdown.
- Patch proposal diff/review panel.
- Test output panel.
- Project rules/settings screen.

Existing components should be reused where practical:

- `web-ui/src/components/project-navigation-panel.tsx` for project selection.
- `web-ui/src/components/card-detail-view.tsx` for task detail composition.
- `web-ui/src/components/detail-panels/diff-viewer-panel.tsx` for diffs.
- `web-ui/src/components/detail-panels/agent-terminal-panel.tsx` for terminal-adjacent status and actions.

## Storage Direction

MVP can use workspace-scoped JSON files next to existing board/session state under `~/.cline/kanban/workspaces/<workspaceId>`.

Likely new stores:

- `project-rules.json`
- `project-chat.json`
- `prompt-runs.json`
- `patch-proposals.json`
- `test-runs.json`
- `file-index.json`

SQLite may be useful later for indexing and prompt logs, but JSON is enough for the first proof loop.

## Boundaries To Respect

- `src/workspace/task-worktree.ts` owns task worktree lifecycle.
- `src/cline-sdk/` owns Cline SDK integration and should not be generalized prematurely.
- `src/terminal/session-manager.ts` owns PTY-backed process sessions.
- `src/server/runtime-state-hub.ts` owns state fanout and should remain the streaming boundary.
- `src/trpc/runtime-api.ts` should coordinate but not accumulate deep worker, context, or patch logic.

