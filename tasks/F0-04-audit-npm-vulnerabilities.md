# F0-04 Audit NPM Vulnerabilities

## Goal
Review dependency audit findings without blindly applying upgrades that could break the app.

## Files To Read
- `package.json`
- `package-lock.json`
- `web-ui/package.json`
- `web-ui/package-lock.json`
- `packages/desktop/package.json`
- `packages/desktop/package-lock.json`

## Files To Modify
- `docs/local-agent-dependency-audit.md`
- Package files only if a targeted, low-risk upgrade is clearly justified

## Exact Instructions
1. Run `npm audit --json` at the repo root.
2. Run `npm --prefix web-ui audit --json`.
3. Run `npm --prefix packages/desktop audit --json`.
4. Summarize each vulnerability, affected package path, severity, and whether it matters for the local personal MVP.
5. Recommend targeted upgrades only when they do not downgrade or remove existing functionality.

## Forbidden Changes
- Do not run `npm audit fix --force`.
- Do not downgrade packages.
- Do not remove Cline SDK dependencies to silence audit findings.

## Acceptance Criteria
- Audit findings are documented.
- Any proposed package changes are justified individually.
- No package files are changed unless the task explicitly decides and verifies a safe upgrade.

## Tests / Checks
- `npm run typecheck`
- `npm run web:typecheck`
- Focused tests for any package area touched

## Difficulty
Medium

## Dependencies
- F0-03

## Recommended Owner
Codex

## Local LLM Label
- Can be done by local LLM: Partially
- Recommended model: `qwen3-coder:30b` for analysis; use Codex for any actual dependency edits

