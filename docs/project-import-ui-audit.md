# Project Import UI Audit

This audit describes the current project selection and import flow before any Ubuntu-first local-agent changes are made.

## Current UI Entry Points

Project navigation is rendered by `web-ui/src/components/project-navigation-panel.tsx`.

Important behavior:

- Projects are sorted by path before rendering.
- Collapsed sidebar shows one button per project plus an add-project button.
- Expanded sidebar has a `Projects` section and a `Kanban Agent` section.
- `onAddProject` opens the add project dialog from the parent app composition.
- Project removal uses a confirmation flow and reports task counts.

Project import is rendered by `web-ui/src/components/add-project-dialog.tsx`.

The dialog has two tabs:

- `Server Path`
- `Git Clone`

The component is stateful and calls tRPC through `getRuntimeTrpcClient(currentProjectId)`.

## Local Path Flow

Relevant code:

- `AddProjectDialog`
- `PathTabContent`
- `DirectoryAutocomplete`
- `handleAddByPath`
- `handleInitializeGit`

Flow:

1. Dialog opens and resets path input to `/`.
2. It fetches root path through `projects.listDirectoryContents.query({})`.
3. User selects or types a server-relative directory path.
4. `resolveToAbsolutePath` combines the relative path with `serverRootPath`.
5. `handleAddByPath` calls `projects.add.mutate({ path, initializeGit })`.
6. If backend returns `requiresGitInitialization`, UI stores `pendingGitInitPath`.
7. User can confirm `Initialize Git Repository`.
8. On success, `onProjectAdded(added.project.id)` is called and dialog closes.

Current UX notes:

- UI text still says Kanban/Cline in some places.
- The browser is browsing server paths, not local browser filesystem paths.
- This is acceptable for the Ubuntu-first app because the runtime is local or SSH/tunnel-backed.

## Git Clone Flow

Relevant code:

- `CloneTabContent`
- `deriveRepoNameFromUrl`
- `handleClone`
- `cloneDestInput`
- `cloneFolderName`

Flow:

1. User enters a Git repository URL.
2. User optionally selects clone destination and folder name.
3. `handleClone` builds `{ gitUrl, path? }`.
4. It calls `projects.add.mutate(mutationInput)`.
5. Backend clones repository and adds it as a project.
6. UI shows success toast and switches to the new project.

Current UX notes:

- Label is generic `Git Clone`, not specifically GitHub.
- HTTPS and SSH-style repo names are display-derived in UI.
- Clone progress is only a spinner/status text.

## Backend Project API

Relevant file: `src/trpc/projects-api.ts`.

Procedures exposed by `app-router.ts` through `projectsApi`:

- `listProjects`
- `addProject`
- `removeProject`
- `pickProjectDirectory`
- `listDirectoryContents`

`addProject` behavior:

- Parses input with `parseProjectAddRequest`.
- If `gitUrl` is present, calls `cloneGitRepository`.
- If `path` is present, resolves relative to active/preferred workspace or process cwd.
- Verifies target is a directory.
- If not a Git repo and `initializeGit` is false, returns `requiresGitInitialization`.
- If initializing Git, calls `initializeGitRepository`.
- If already a Git repo, calls `ensureInitialCommit`.
- Loads workspace context and remembers workspace.
- Sets active workspace if there was no valid active workspace.
- Broadcasts project updates.

`removeProject` behavior:

- Reads project by ID from workspace index.
- Attempts to collect task IDs that need worktree cleanup.
- Stops terminal sessions for the removed project.
- Removes workspace index entry and workspace state files.
- Disposes workspace registry state.
- Picks a fallback active workspace if needed.
- Deletes task worktrees best effort in the background.

`listDirectoryContents` behavior:

- Uses server filesystem root as sandbox.
- Rejects paths outside the root.
- Lists only directories and skips hidden directories.
- Marks entries that contain a `.git` directory or file.

## Git Clone Helper

Relevant file: `src/workspace/git-clone.ts`.

Behavior:

- Derives repo name from HTTPS, SSH, or bare URL.
- Validates clone destination stays inside allowed root.
- If destination exists and is a directory, appends repo name.
- Rejects existing nested destination.
- Creates parent directory.
- Runs `git clone -- <url> <destination>`.

## Git Initialization Helper

Relevant file: `src/workspace/initialize-repo.ts`.

Behavior:

- `initializeGitRepository` runs `git init`.
- `ensureInitialCommit` checks `HEAD`.
- If missing, stages all files and creates an allow-empty initial commit.
- Commit message currently says `Initial commit through Cline Kanban`.

## Rebrand / Fork Notes

Later fork-specific UI cleanup should change:

- Product label in `ProjectNavigationPanel` from Cline/Kanban branding to local-agent fork name.
- Non-Git warning text in `AddProjectDialog` from "Cline requires git" to fork-specific wording.
- Initial commit message in `initialize-repo.ts` from Cline Kanban wording.
- Sidebar section label `Kanban Agent` if the new Plan/Architect/Worker model replaces it.

## Ubuntu-First Improvements To Add Later

- Make manual absolute path entry prominent.
- Treat missing native folder picker on remote/headless Linux as normal.
- Add clearer SSH/tunnel language for remote runtime paths.
- Add GitHub clone helper text but keep generic Git URLs.
- Add clone output/progress capture if clone operations become long-running.
- Let project rules be configured immediately after import.

## Current Safe Reuse

The existing project API is good enough for the MVP. It already supports:

- Local folder/path project import.
- Git clone/import.
- Git initialization prompt.
- Workspace index persistence.
- Active project selection.
- Project removal and worktree cleanup.

The first implementation phase should refine labels and add rules/settings rather than replacing this flow.

