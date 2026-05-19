# F2-01 Add AgentRole And ModelProfile Schemas

## Goal
Add generic model/role types without affecting existing Cline or PTY agent behavior.

## Files To Read
- `src/core/api-contract.ts`
- `src/core/agent-catalog.ts`
- `src/config/runtime-config.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add `runtimeAgentRoleSchema` with roles: `plan`, `architect`, `worker`, `reviewer`, `tester`.
2. Add `runtimeModelProfileSchema` with provider, model, label, context limit, temperature, and supported roles.
3. Export inferred types.

## Forbidden Changes
- Do not change `runtimeAgentIdSchema`.
- Do not change existing runtime config.

## Acceptance Criteria
- New types are exported.
- Existing agent launch behavior is untouched.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- None

## Recommended Owner
Smaller local model

