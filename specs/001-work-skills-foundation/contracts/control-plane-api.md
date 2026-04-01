# Control-Plane API Contract

## Purpose

Define the sanctioned API surface that reads and writes central and
project-local SQL-backed state.

## Authority Rules

- The control-plane API is the only sanctioned writer to SQL-backed project and
  control-plane stores.
- Direct SQL writes are unsupported and MUST be treated as drift when detected.
- The API is responsible for dual-writing central state and refreshing the
  project-local normalized export.

## Core Resources

### `GET /api/portfolio/overview`

Returns:

- registered projects
- active initiatives and waves
- next ready task per project
- unresolved drift counts
- active exceptions

### `POST /api/projects/register`

Registers a managed project path into the allowlist registry.

Request fields:

- `project_id`
- `repo_root`
- `manifest_path`

### `POST /api/projects/{project_id}/sync`

Reconciles:

- project contract
- normalized issue export
- provenance ledger
- integrity baseline
- open exceptions

Response includes:

- sync status
- drift findings
- updated hashes
- blocking conditions

### `GET /api/projects/{project_id}/next-task`

Runs the `project-next` selection policy and returns:

- recommended `task_id`
- dependency rationale
- blockers for skipped tasks

### `POST /api/tasks/{task_id}/flow/start`

Starts `flow-auto <task_id>` for a task.

Preconditions:

- task exists
- dependencies satisfied
- worktree exists for coding tasks

### `POST /api/tasks/{task_id}/flow/advance`

Advances a task to the next gate when evidence requirements are satisfied.

Required request fields:

- `target_state`
- `approval_note`
- `operation_context`

### `POST /api/tasks/{task_id}/qa`

Records:

- newly added tests
- repeatable validation steps
- evidence paths

### `POST /api/tasks/{task_id}/audit`

Runs `cicd-auditor` and records:

- deterministic audit findings
- optional LLM review result
- blocking status

### `POST /api/tasks/{task_id}/exceptions`

Creates a time-boxed exception record with:

- reason
- owner
- scope
- expiry

## Response Guarantees

Every sanctioned write response MUST include:

- `operation_id`
- affected project and task identifiers
- whether the normalized export was refreshed
- whether blocking drift remains
