# Local Issue Store Contract

## Purpose

Define the sanctioned project-local issue model used by `project-next`,
`flow-auto <task_id>`, `qa`, and `cicd-auditor`.

## Storage Model

- Working task state lives in `.workskills/runtime/issues.db`
- Durable mirrored issue state lives in
  `.workskills/reference/issues.snapshot.json`
- Agents are expected to interact with this state through the control-plane API,
  not through direct SQL

## SQLite Tables

### `issues`

| Column | Type | Notes |
|--------|------|-------|
| `task_id` | text | Primary task identifier |
| `project_id` | text | Owning project |
| `wave_id` | text | Owning wave |
| `title` | text | Task summary |
| `task_type` | text | `planning`, `coding`, `qa`, `audit`, `ops`, `docs` |
| `priority` | integer | Relative ordering |
| `lifecycle_state` | text | `draft`, `planned`, `ready`, `in_progress`, `review`, `qa`, `audit`, `done`, `blocked`, `cancelled` |
| `health_state` | text | `normal`, `blocked`, `drift`, `excepted` |
| `worktree_required` | integer | Boolean flag |
| `active_worktree_id` | text | Bound worktree |
| `operation_id` | text | Last sanctioned write operation |
| `updated_at` | text | ISO timestamp |

### `task_dependencies`

| Column | Type | Notes |
|--------|------|-------|
| `task_id` | text | Dependent task |
| `depends_on_task_id` | text | Required predecessor |

### `task_events`

| Column | Type | Notes |
|--------|------|-------|
| `event_id` | text | Stable event identifier |
| `task_id` | text | Related task |
| `event_type` | text | Transition, approval, sync, drift, closure |
| `payload_json` | text | Deterministic event payload |
| `operation_id` | text | Sanctioned write identifier |
| `created_at` | text | ISO timestamp |

### `worktrees`

| Column | Type | Notes |
|--------|------|-------|
| `worktree_id` | text | Stable binding identifier |
| `task_id` | text | Related coding task |
| `branch_name` | text | Expected branch |
| `worktree_path` | text | Filesystem path |
| `state` | text | `planned`, `active`, `stale`, `merge_ready`, `closed` |
| `updated_at` | text | ISO timestamp |

## Normalized Export Rules

The normalized issue export MUST:

- sort records deterministically
- exclude SQLite internals and row-order artifacts
- include task fields, dependencies, active worktree bindings, linked event
  IDs, and last sanctioned `operation_id`
- be suitable for hashing by the integrity system

## Sanctioned Write Rules

- Every API-mediated write MUST stamp a new `operation_id`
- The normalized export MUST be refreshed after sanctioned task transitions
- Rows or exports with missing `operation_id` are treated as drift candidates

## Unsupported States

The following conditions are invalid and MUST be flagged:

- coding task without a worktree once execution starts
- task marked `done` without commit linkage
- task marked `done` while `health_state` is `drift`
- task lifecycle state ahead of required approval gate evidence
