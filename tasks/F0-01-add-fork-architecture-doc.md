# F0-01 Add Fork Architecture Doc

## Goal
Create a durable architecture note for the local-agent fork goals without changing source code.

## Files To Read
- `docs/architecture.md`
- `AGENTS.md`
- `docs/LOCAL_AGENT_FORK_ROADMAP.md`

## Files To Modify
- `docs/local-agent-fork-architecture.md`

## Exact Instructions
1. Create `docs/local-agent-fork-architecture.md`.
2. Summarize the target fork architecture: Plan Mode, Architect Mode, Ollama workers, context bundles, patch proposals, approval, tests, and fix-loop generation.
3. Reference existing runtime areas: `src/trpc/runtime-api.ts`, `src/server/runtime-state-hub.ts`, `src/workspace/task-worktree.ts`, `web-ui/src/components/card-detail-view.tsx`.
4. Keep the document descriptive only.

## Forbidden Changes
- Do not modify TypeScript or UI files.
- Do not rename existing docs.

## Acceptance Criteria
- The new doc exists and references current code paths accurately.
- No source code files are modified.

## Tests / Checks
- `git diff -- docs/local-agent-fork-architecture.md`

## Difficulty
Low

## Dependencies
- None

## Recommended Owner
Smaller local model

