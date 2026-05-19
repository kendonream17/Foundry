# F10-01 Add Remote Worker Protocol Doc

## Goal
Define future remote worker protocol before implementation.

## Files To Read
- `src/workers/worker-registry.ts`
- `docs/LOCAL_AGENT_FORK_ROADMAP.md`

## Files To Modify
- `docs/remote-worker-protocol.md`

## Exact Instructions
1. Document registration, heartbeat, task assignment, task result, cancellation, and security token flow.
2. Include JSON examples.
3. Keep it implementation-neutral.

## Forbidden Changes
- Do not implement remote workers.

## Acceptance Criteria
- Protocol doc is clear enough to implement later.

## Tests / Checks
- `git diff -- docs/remote-worker-protocol.md`

## Difficulty
Low

## Dependencies
- F5-03

## Recommended Owner
Smaller local model

