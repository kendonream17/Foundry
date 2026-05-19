# Local Agent Fork Task Index

This index is the working task tracker for the local-agent fork. Completed tasks can stay here for audit/history or be deleted/archived if the user does not want them retained.

Recommended local model tiers:

- Small/local-docs: `qwen2.5-coder:7b`
- Medium/local-code: `qwen2.5-coder:14b`
- Strong/local-agentic: `qwen3-coder:30b`
- Alternative coding model: `deepseek-coder-v2:16b`
- Codex: use for high-risk orchestration, patch application, dependency changes, and cross-cutting architecture edits.

## Completed

| Task | Title | Local LLM | Recommended Model |
| --- | --- | --- | --- |
| F0-01 | Add Fork Architecture Doc | Yes | `qwen2.5-coder:7b` |
| F0-02 | Add Regression Areas Doc | Yes | `qwen2.5-coder:7b` |
| F1-01 | Audit Add Project UI | Yes | `qwen2.5-coder:7b` |
| F1-02 | Add ProjectRule Schema | Yes | `qwen2.5-coder:7b` |
| F2-01 | Add AgentRole And ModelProfile Schemas | Yes | `qwen2.5-coder:7b` |
| F2-02 | Add Ollama Config Shape | Yes | `qwen2.5-coder:14b` |
| F3-01 | Add PromptRun Schema | Yes | `qwen2.5-coder:7b` |
| F4-01 | Add Project Chat Data Model | Yes | `qwen2.5-coder:7b` |
| F4-04 | Add Architect Task Draft Schema | Yes | `qwen2.5-coder:7b` |
| F5-02 | Add Local Worker Schemas | Yes | `qwen2.5-coder:7b` |
| F6-01 | Add PatchProposal Schema | Yes | `qwen2.5-coder:7b` |
| F6-02 | Add Worker Output Schema | Yes | `qwen2.5-coder:7b` |
| F9-01 | Add FileIndexEntry Schema | Yes | `qwen2.5-coder:7b` |
| F10-01 | Add Remote Worker Protocol Doc | Yes | `qwen2.5-coder:7b` |
| F12-01 | Add Autopilot Policy Schema | Yes | `qwen2.5-coder:7b` |

## Remaining Tasks

| Task | Title | Local LLM | Recommended Model | Notes |
| --- | --- | --- | --- | --- |
| F0-03 | Add Dev Setup Verification Doc | Yes | `qwen2.5-coder:7b` | New setup-hardening task |
| F0-04 | Audit NPM Vulnerabilities | Partially | `qwen3-coder:30b` | Codex should make any dependency edits |
| F0-05 | Document Desktop Build Path Limitation | Yes | `qwen2.5-coder:7b` | New setup-hardening task |
| F1-03 | Persist Project Rules JSON | Yes | `qwen2.5-coder:14b` | Add storage only |
| F1-04 | Add Project Rules API | Yes | `qwen2.5-coder:14b` | Backend API boundary |
| F2-03 | Add Model Profile Defaults | Yes | `qwen2.5-coder:14b` | Depends on F2-02 |
| F3-02 | Add Prompt Preview Builder Skeleton | Yes | `qwen2.5-coder:14b` | Keep pure builder |
| F3-03 | Add Prompt Preview tRPC Endpoint | Yes | `qwen2.5-coder:14b` | Small API wiring |
| F3-04 | Add Prompt Preview Modal | Yes | `qwen2.5-coder:14b` | UI task |
| F4-02 | Persist Project Chat | Yes | `qwen2.5-coder:14b` | State file/store |
| F4-03 | Add Plan/Architect Chat API Skeleton | Yes | `qwen2.5-coder:14b` | Skeleton only |
| F4-05 | Create Cards From Architect Drafts | Partially | `qwen3-coder:30b` | Board mutation risk |
| F5-01 | Add Ollama HTTP Client | Yes | `qwen2.5-coder:14b` | Mock fetch tests |
| F5-03 | Add Worker Registry Service | Partially | `qwen3-coder:30b` | Runtime state lifecycle |
| F5-04 | Add Workers tRPC Router | Partially | `qwen3-coder:30b` | Router/state integration |
| F5-05 | Add Local Ollama Worker Discovery | Yes | `qwen2.5-coder:14b` | Uses Ollama client |
| F6-03 | Execute Task With Ollama | No | Codex | First real worker execution path |
| F6-04 | Store Patch Proposals | Yes | `qwen2.5-coder:14b` | Additive persistence |
| F6-05 | Render Patch Proposal Diff | Yes | `qwen2.5-coder:14b` | Reuse diff renderer |
| F7-01 | Add Patch Validation Service | No | Codex | Safety-critical |
| F7-02 | Add Apply Patch API | No | Codex | File mutation boundary |
| F7-03 | Add TestRun Schema And Store | Yes | `qwen2.5-coder:14b` | Additive persistence |
| F7-04 | Add Test Execution API | No | Codex | Command execution policy |
| F7-05 | Create Fix Task From Failed Test | Yes | `qwen2.5-coder:14b` | Board mutation, focused |
| F8-01 | Add Worker Status Panel Shell | Yes | `qwen2.5-coder:14b` | UI shell |
| F8-02 | Add Worker Card Details | Yes | `qwen2.5-coder:14b` | UI detail rendering |
| F8-03 | Add Task Assignment Dropdown | Yes | `qwen2.5-coder:14b` | UI + mutation |
| F9-02 | Add Project Scanner MVP | Yes | `qwen2.5-coder:14b` | Respect off-limits rules |
| F9-03 | Add Framework Detector | Yes | `qwen2.5-coder:14b` | Pure utility |
| F9-04 | Add Context Bundle Builder | Partially | `qwen3-coder:30b` | Core prompt-size control |
| F9-05 | Add Context Preview UI | Yes | `qwen2.5-coder:14b` | UI task |
| F10-02 | Add Registration Token Store | No | Codex | Future security boundary |
| F10-03 | Add Remote Heartbeat Endpoint | No | Codex | Remote protocol surface |
| F11-01 | Add Split Task Card Action | Yes | `qwen2.5-coder:14b` | Board mutation |
| F11-02 | Add Merge Task Cards Action | Yes | `qwen2.5-coder:14b` | Board mutation |
| F11-03 | Add Task Completion Disposition | Partially | `qwen3-coder:30b` | Preserve Done/Trash compatibility |

## Suggested Next Order

1. F0-03, F0-05
2. F2-03
3. F5-01
4. F5-03, F5-04, F5-05
5. F3-02, F3-03, F3-04
6. F9-02, F9-03, F9-04
7. F6-03, F6-04, F6-05
8. F7-01, F7-02, F7-03, F7-04, F7-05
9. F8-01, F8-02, F8-03
10. F4-02, F4-03, F4-05
11. F11-01, F11-02, F11-03
12. F10-02, F10-03
