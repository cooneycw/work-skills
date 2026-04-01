# Data Model: Work-Skills Phase 1 Architecture Foundation

## Core Entities

### Initiative

| Field | Type | Notes |
|------|------|-------|
| `initiative_id` | string | Stable identifier across the portfolio |
| `title` | string | Human-readable initiative name |
| `objective` | text | Executive goal being pursued |
| `success_criteria` | list | Portfolio-level measurable outcomes |
| `status` | enum | `draft`, `active`, `paused`, `complete`, `archived` |
| `owner` | string | Responsible human operator |

**Relationships**

- Owns one or more `ManagedProject` records
- Owns one or more `Wave` records

### ManagedProject

| Field | Type | Notes |
|------|------|-------|
| `project_id` | string | Stable project identifier |
| `display_name` | string | UI-facing project name |
| `repo_root` | path | Absolute local path registered in the cockpit |
| `contract_version` | string | Version of the blessed project contract |
| `default_profile` | string | Blessed downstream application profile |
| `registry_status` | enum | `candidate`, `registered`, `degraded`, `archived` |
| `last_sync_at` | timestamp | Last successful reconciliation time |

**Relationships**

- Belongs to one `Initiative`
- Owns many `Task` records
- Owns one local issue store and one normalized issue export
- Owns one provenance ledger and one integrity baseline

### Wave

| Field | Type | Notes |
|------|------|-------|
| `wave_id` | string | Stable identifier within an initiative |
| `initiative_id` | string | Parent initiative |
| `project_id` | string | Target project |
| `title` | string | Deliverable slice title |
| `priority` | integer | Ordering signal |
| `entry_criteria` | list | Preconditions for work to begin |
| `exit_criteria` | list | Conditions to mark wave complete |
| `status` | enum | `planned`, `active`, `blocked`, `done` |

### Task

| Field | Type | Notes |
|------|------|-------|
| `task_id` | string | First-class stable identifier |
| `project_id` | string | Owning project |
| `wave_id` | string | Owning wave |
| `title` | string | Human-readable task summary |
| `task_type` | enum | `planning`, `coding`, `qa`, `audit`, `ops`, `docs` |
| `priority` | integer | Relative ordering |
| `dependency_ids` | list | Other tasks that must be satisfied first |
| `lifecycle_state` | enum | See task state machine below |
| `health_state` | enum | `normal`, `blocked`, `drift`, `excepted` |
| `worktree_required` | boolean | True for coding tasks |
| `active_worktree_id` | string | Current bound worktree, if any |
| `operation_id` | string | Last sanctioned write operation |
| `commit_refs` | list | Commits linked to this task |

### WorktreeBinding

| Field | Type | Notes |
|------|------|-------|
| `worktree_id` | string | Stable binding ID |
| `task_id` | string | Owning task |
| `branch_name` | string | Expected git branch |
| `worktree_path` | path | Local filesystem path |
| `state` | enum | `planned`, `active`, `stale`, `merge_ready`, `closed` |
| `created_at` | timestamp | Creation time |
| `closed_at` | timestamp | Close time |

### ProvenanceEntry

| Field | Type | Notes |
|------|------|-------|
| `provenance_id` | string | Stable entry ID |
| `source_repo_url` | string | Canonical upstream URL |
| `local_clone_path` | path | Local clone used for reference |
| `revision` | string | Commit SHA or tag |
| `license` | string | License captured at adoption time |
| `usage_mode` | enum | `reference`, `adapted`, `copied`, `wrapped` |
| `attribution_text` | text | Required attribution summary |
| `related_task_ids` | list | Tasks affected by this source |

### IntegrityBaseline

| Field | Type | Notes |
|------|------|-------|
| `baseline_id` | string | Stable baseline record |
| `project_id` | string | Owning project |
| `artifact_scope` | list | Which artifacts are hashed |
| `baseline_hashes` | map | Hashes from the approved baseline |
| `current_hashes` | map | Most recent measured hashes |
| `drift_status` | enum | `clean`, `changed`, `unapproved` |
| `measured_at` | timestamp | Last measurement time |

### AuditRun

| Field | Type | Notes |
|------|------|-------|
| `audit_id` | string | Stable audit result ID |
| `scope_type` | enum | `project`, `wave`, `task` |
| `scope_id` | string | Target record identifier |
| `audit_kind` | enum | `deterministic`, `llm`, `qa` |
| `result` | enum | `pass`, `fail`, `warn`, `excepted` |
| `blocking` | boolean | Whether the result blocks progression |
| `findings_path` | path | Local file for detailed findings |
| `created_at` | timestamp | Audit time |

### ExceptionRecord

| Field | Type | Notes |
|------|------|-------|
| `exception_id` | string | Stable exception identifier |
| `scope_type` | enum | `project`, `wave`, `task`, `audit_rule` |
| `scope_id` | string | Target record identifier |
| `reason` | text | Human-accepted risk statement |
| `owner` | string | Responsible person |
| `opened_at` | timestamp | When the exception was granted |
| `expires_at` | timestamp | Expiry time |
| `status` | enum | `active`, `expired`, `resolved`, `revoked` |

## Task State Machine

`Task.lifecycle_state` uses the following primary progression:

1. `draft`
2. `planned`
3. `ready`
4. `in_progress`
5. `review`
6. `qa`
7. `audit`
8. `done`

Allowed side paths:

- Any non-terminal state may move to `blocked`
- `blocked` may return to `ready` or `in_progress` when evidence is supplied
- Any non-terminal state may move to `cancelled`

`Task.health_state` is orthogonal to lifecycle state:

- `normal`: no current delivery concerns
- `blocked`: a dependency or gate is unsatisfied
- `drift`: mirrored state or integrity baseline does not match
- `excepted`: a valid time-boxed exception is active

## Derived Models

### Normalized Issue Export

A deterministic, sorted serialization of task state used for:

- integrity hashing
- control-plane synchronization
- reproducible audit input

The export MUST exclude volatile database internals and MUST include:

- stable task fields
- dependency lists
- worktree bindings
- active lifecycle and health state
- last sanctioned `operation_id`
- related audit result identifiers

### Portfolio Summary

A read model derived by the control cockpit that aggregates:

- project registration and health
- active initiative and wave
- next ready task
- unresolved drift
- open exceptions
- provenance debt
