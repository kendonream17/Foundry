# F1-01 Audit Add Project UI

## Goal
Map the current project add/import UI flow before changing it.

## Files To Read
- `web-ui/src/components/project-navigation-panel.tsx`
- `web-ui/src/components/add-project-dialog.tsx`
- `src/trpc/projects-api.ts`
- `src/core/api-contract.ts`

## Files To Modify
- `docs/project-import-ui-audit.md`

## Exact Instructions
1. Create `docs/project-import-ui-audit.md`.
2. Document how local path selection, directory listing, GitHub/Git clone, and git initialization currently work.
3. Identify which UI text should later be rebranded from Cline/Kanban to the local-agent fork.

## Forbidden Changes
- Do not modify UI or API behavior.

## Acceptance Criteria
- The audit identifies exact files and flows for project import.

## Tests / Checks
- `git diff -- docs/project-import-ui-audit.md`

## Difficulty
Low

## Dependencies
- None

## Recommended Owner
Smaller local model

