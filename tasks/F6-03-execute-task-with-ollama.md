# F6-03 Execute Task With Ollama

## Goal
Run one assigned task through the local Ollama worker and capture structured output without applying changes.

## Files To Read
- `src/workers/local-ollama-worker.ts`
- `src/ollama/ollama-client.ts`
- `src/prompt-runs/prompt-preview.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `src/workers/local-ollama-worker.ts`
- Supporting worker service files as needed

## Exact Instructions
1. Add a function that accepts task instructions, model name, and context text.
2. Send a structured-output prompt to Ollama.
3. Parse the result into the worker output schema from F6-02.
4. Return failure state when JSON parsing fails.
5. Do not mutate files.

## Forbidden Changes
- Do not wire into UI yet.
- Do not apply patches.
- Do not change PTY/Cline session execution.

## Acceptance Criteria
- Worker execution returns structured success/failure.
- Invalid model output is handled safely.

## Tests / Checks
- `npm run typecheck`
- Mocked Ollama response test if practical

## Difficulty
High

## Dependencies
- F5-05
- F6-02

## Recommended Owner
Codex

