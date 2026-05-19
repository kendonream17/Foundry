# Remote Worker Protocol

This document defines the future remote worker protocol for the local-agent fork. It is a planning document only; no remote worker implementation exists yet.

## Goals

- Allow the main runtime to coordinate local and remote worker machines.
- Keep the main runtime authoritative for task state, prompt logs, patch validation, patch application, and test runs.
- Let remote workers execute model calls and produce structured results.
- Avoid giving remote workers direct permission to mutate the main project repo.

## Actors

### Main Runtime

The existing Node runtime started by the app. It owns:

- Project registry.
- Board/task state.
- Context bundle creation.
- Prompt preview/logging.
- Worker registry.
- Patch proposal storage.
- Patch validation/application.
- Test execution and fix task generation.

### Worker Node

A local or remote process that can:

- Report machine and Ollama status.
- Advertise model capabilities.
- Accept one or more task execution requests.
- Return structured worker output and proposed patches.
- Support cancellation.

MVP only needs a local worker embedded in the main runtime. Remote workers come later.

## Transport

Future remote workers can use HTTP JSON endpoints from worker to main runtime and main runtime to worker.

Recommended defaults:

- Main runtime listens on existing runtime host/port.
- Worker node exposes a small HTTP server for task execution and cancellation.
- Main runtime stores worker URL after registration.
- All remote endpoints require a registration token or derived worker token.

WebSockets can be added later for streaming logs, but polling heartbeats are enough for MVP remote design.

## Registration

Remote worker registration is explicit and token-based.

Main runtime creates a one-time or revocable token. User copies token to remote worker config.

Request:

```json
{
  "token": "worker_registration_token",
  "workerUrl": "http://192.168.1.50:43180",
  "machineName": "ubuntu-worker-1",
  "kind": "remote",
  "ollamaUrl": "http://127.0.0.1:11434"
}
```

Response:

```json
{
  "ok": true,
  "workerId": "worker_ubuntu_1",
  "workerToken": "scoped_worker_token",
  "heartbeatIntervalMs": 5000
}
```

Rules:

- Store only hashed registration tokens.
- Return a scoped worker token only once.
- Allow token revocation.
- Do not expose worker tokens in normal list responses.

## Heartbeat

Worker sends heartbeat periodically.

Request:

```json
{
  "workerId": "worker_ubuntu_1",
  "status": "online",
  "machineName": "ubuntu-worker-1",
  "ollama": {
    "url": "http://127.0.0.1:11434",
    "online": true,
    "models": [
      {
        "name": "qwen2.5-coder:7b",
        "modifiedAt": "2026-05-19T16:00:00.000Z",
        "size": 4680000000
      }
    ]
  },
  "currentTaskId": null,
  "metrics": {
    "activeRuns": 0,
    "completedRuns": 12,
    "lastRunDurationMs": 48750
  }
}
```

Response:

```json
{
  "ok": true,
  "serverTime": 1779216000000,
  "commands": []
}
```

Status values:

- `online`
- `offline`
- `busy`
- `error`

Main runtime should mark workers offline when heartbeats are stale.

## Task Assignment

User assignment remains primary. Scheduler recommendations can come later.

Main runtime records:

- `taskId`
- `workerId`
- `modelProfileId`
- assigned time
- assigned by user/manual policy

Remote worker should not pull arbitrary tasks. Main runtime sends an explicit run request.

## Run Task

Main runtime calls the worker's task execution endpoint.

Request:

```json
{
  "runId": "run_123",
  "taskId": "task_abc",
  "model": "qwen2.5-coder:7b",
  "role": "worker",
  "instructions": "Implement the scoped change described below...",
  "contextBundle": {
    "id": "ctx_123",
    "tokenEstimate": 7200,
    "files": [
      {
        "path": "src/example.ts",
        "content": "export function example() {}"
      }
    ],
    "summaries": [
      "This project is a TypeScript Node/React app."
    ]
  },
  "outputContract": {
    "format": "json",
    "requiresPatch": true
  }
}
```

Response:

```json
{
  "ok": true,
  "accepted": true,
  "runId": "run_123"
}
```

Worker then completes asynchronously or returns final result directly for simple MVP implementations.

## Task Result

Worker returns structured output to main runtime.

Request:

```json
{
  "workerId": "worker_ubuntu_1",
  "runId": "run_123",
  "taskId": "task_abc",
  "status": "completed",
  "model": "qwen2.5-coder:7b",
  "summary": "Added validation for project rules.",
  "explanation": "The change adds schema fields and keeps existing cards backward-compatible.",
  "patch": "diff --git a/src/example.ts b/src/example.ts\n...",
  "changedFiles": [
    "src/example.ts"
  ],
  "testSuggestions": [
    "npm run typecheck"
  ],
  "followUpQuestions": []
}
```

Response:

```json
{
  "ok": true,
  "patchProposalId": "patch_123"
}
```

Rules:

- Main runtime stores this as a patch proposal.
- Worker does not apply the patch.
- Main runtime validates patch before any user approval/apply action.

## Cancellation

Main runtime can cancel a run.

Request from main runtime to worker:

```json
{
  "runId": "run_123",
  "taskId": "task_abc",
  "reason": "user_cancelled"
}
```

Response:

```json
{
  "ok": true,
  "status": "cancelling"
}
```

Worker should attempt to abort the active Ollama request and report a final cancelled result.

## Error Reporting

Worker result can report failure.

```json
{
  "workerId": "worker_ubuntu_1",
  "runId": "run_123",
  "taskId": "task_abc",
  "status": "failed",
  "error": {
    "code": "MODEL_OUTPUT_INVALID",
    "message": "Model returned invalid JSON."
  },
  "rawOutputExcerpt": "{ not json"
}
```

Main runtime should store the failed prompt run and show it in UI.

## Security Rules

- Remote worker registration must be opt-in.
- Registration tokens must be revocable.
- Worker tokens must be scoped to worker actions.
- Workers must not receive files excluded by project rules.
- Workers must not receive broad project state unless the user approves the context bundle.
- Workers must not be allowed to apply patches directly.
- Main runtime must log every prompt and response.

## Capability Reporting

Workers should eventually report:

- Machine name.
- OS/platform.
- Ollama URL and status.
- Available models.
- Basic model metadata if available.
- CPU/RAM/GPU hints if easy to collect.
- Current task.
- Last run duration.
- Recent failure message.

## MVP Cut

The MVP should not implement this protocol over the network. It should implement the same concepts in-process for a local Ollama worker:

- Worker registry.
- Local heartbeat/discovery.
- One active task.
- Structured result.
- Patch proposal creation.

The remote protocol should be implemented only after the local worker flow is stable.

