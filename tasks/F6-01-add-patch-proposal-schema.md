# F6-01 Add PatchProposal Schema

## Goal
Define persisted worker patch proposals.

## Files To Read
- `src/core/api-contract.ts`
- `src/workspace/get-workspace-changes.ts`

## Files To Modify
- `src/core/api-contract.ts`

## Exact Instructions
1. Add `runtimePatchProposalSchema`.
2. Include id, taskId, workerNodeId, baseCommit, patchText, summary, files, status, createdAt, updatedAt.
3. Include statuses such as `draft`, `submitted`, `validated`, `rejected`, `approved`, `applied`, `failed`.

## Forbidden Changes
- Do not add patch application behavior.
- Do not change existing diff schemas.

## Acceptance Criteria
- Schema compiles and is exported.

## Tests / Checks
- `npm run typecheck`

## Difficulty
Low

## Dependencies
- F5-02

## Recommended Owner
Smaller local model

