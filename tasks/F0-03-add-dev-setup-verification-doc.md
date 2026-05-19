# F0-03 Add Dev Setup Verification Doc

## Goal
Document the exact Ubuntu-first install and verification commands needed before local-agent work begins.

## Files To Read
- `package.json`
- `web-ui/package.json`
- `packages/desktop/package.json`
- `AGENTS.md`
- `DEVELOPMENT.md`

## Files To Modify
- `docs/local-agent-dev-setup.md`
- Optional link from `docs/LOCAL_AGENT_FORK_ROADMAP.md`

## Exact Instructions
1. Create a short Ubuntu 22.04+ setup doc.
2. Include `npm run install:all`.
3. Include verification commands: `npm run typecheck`, `npm run web:typecheck`, and focused test examples.
4. Mention that `packages/desktop` native rebuild can warn when the repo path contains spaces.
5. Mention that dependency vulnerabilities should be audited before public release but should not block personal MVP work unless they affect runtime execution.

## Forbidden Changes
- Do not change dependency versions.
- Do not modify package scripts.
- Do not add OS-specific setup for macOS or Windows.

## Acceptance Criteria
- A new setup doc exists.
- It gives exact commands that work from the repo root.
- It reflects Ubuntu-first personal-use priorities.

## Tests / Checks
- `git diff -- docs/local-agent-dev-setup.md`

## Difficulty
Low

## Dependencies
- None

## Recommended Owner
Smaller local model

## Local LLM Label
- Can be done by local LLM: Yes
- Recommended model: `qwen2.5-coder:7b`

