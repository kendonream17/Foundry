# F2-02 Add Ollama Config Shape

## Status
Complete. Implemented as an additive config field; verification commands are blocked until dependencies are installed because `tsc` and `vitest` are not currently available in `node_modules`.

## Goal
Add runtime config fields for a local Ollama endpoint.

## Files To Read
- `src/config/runtime-config.ts`
- `src/core/api-contract.ts`
- `src/terminal/agent-registry.ts`
- `web-ui/src/runtime/use-runtime-config.ts`

## Files To Modify
- `src/config/runtime-config.ts`
- `src/core/api-contract.ts`
- `web-ui/src/runtime/types.ts` if generated/manual runtime types require update

## Exact Instructions
1. Add an optional `ollamaBaseUrl` setting.
2. Default to `http://127.0.0.1:11434`.
3. Include the value in runtime config response and save request.
4. Keep config backward-compatible.

## Forbidden Changes
- Do not add UI yet.
- Do not call Ollama yet.
- Do not modify Cline provider settings.

## Acceptance Criteria
- Runtime config can load/save an Ollama URL.
- Missing config uses the default.

## Tests / Checks
- `npm run typecheck`
- Existing config tests if present

## Difficulty
Medium

## Dependencies
- None

## Recommended Owner
Codex
