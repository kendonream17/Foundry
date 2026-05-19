# F0-05 Document Desktop Build Path Limitation

## Goal
Document the desktop native rebuild warning caused by spaces in the repository path.

## Files To Read
- `packages/desktop/package.json`
- `packages/desktop/scripts/patch-node-pty.mjs`
- `AGENTS.md`
- `DEVELOPMENT.md`

## Files To Modify
- `docs/local-agent-dev-setup.md`
- Optional `AGENTS.md` addition only if this becomes a repeated source of failed installs

## Exact Instructions
1. Explain that `electron-builder install-app-deps` can warn about native modules when the repo path contains spaces.
2. Note that the observed install can still complete successfully.
3. Recommend using a no-space checkout path if desktop native rebuilds become unreliable.
4. Keep this as documentation only.

## Forbidden Changes
- Do not move the repository.
- Do not change desktop build scripts.
- Do not disable the desktop postinstall.

## Acceptance Criteria
- The setup doc explains the warning and recommended mitigation.
- No build/runtime code is changed.

## Tests / Checks
- `git diff -- docs/local-agent-dev-setup.md`

## Difficulty
Low

## Dependencies
- F0-03

## Recommended Owner
Smaller local model

## Local LLM Label
- Can be done by local LLM: Yes
- Recommended model: `qwen2.5-coder:7b`

