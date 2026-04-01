<!--
Sync Impact Report
Version change: 0.0.0 -> 1.0.0
Modified principles:
- Template placeholders -> I. Local-First Contract Authority
- Template placeholders -> II. Blessed Delivery Pattern
- Template placeholders -> III. Task-Scoped Isolation and Approval Gates
- Template placeholders -> IV. Deterministic Verification Before LLM Judgment
- Template placeholders -> V. Provenance and Attribution by Default
Added sections:
- Operating Constraints
- Workflow and Quality Gates
Removed sections:
- None
Templates requiring updates:
- ⚠ pending .specify/templates/spec-template.md
- ⚠ pending .specify/templates/plan-template.md
- ⚠ pending .specify/templates/tasks-template.md
Follow-up TODOs:
- Align spec-kit templates and local skill docs with the required contract,
  worktree, provenance, and audit vocabulary before broad rollout.
-->

# Work-Skills Constitution

## Core Principles

### I. Local-First Contract Authority
All managed project workflow state MUST remain locally resident. Each managed
project MUST expose a standard contract, local planning artifacts, and a local
issue-state mirror that can be rebuilt without any hosted service. The control
plane may index and mirror state, but no hosted system may become the only
readable source of delivery truth.

### II. Blessed Delivery Pattern
Work-skills exists to enforce one repeatable operating model across
initiatives. Every managed project MUST use the same required skill chain,
artifact layout, initiative hierarchy, and downstream default application
profile unless a documented exception is approved. Flexibility is allowed only
through explicit add-ons, not by inventing a new workflow per project.

### III. Task-Scoped Isolation and Approval Gates
Every coding task MUST be a first-class task record with a stable `task_id`,
mapped to a dedicated git worktree before implementation begins. Automated
flows MAY assist with planning, development, testing, and audit preparation,
but they MUST stop at named approval gates before a task advances to a higher
trust state or closes.

### IV. Deterministic Verification Before LLM Judgment
Deterministic checks MUST run before any LLM-based judgment is trusted. Tests,
artifact presence, task linkage, worktree state, integrity baselines,
provenance, and commit evidence MUST be verified mechanically. LLM review may
augment these checks, but it cannot replace them or bypass failed deterministic
gates.

### V. Provenance and Attribution by Default
Any external repository, template, pattern, or borrowed implementation idea
MUST be tracked in a project-local provenance ledger before related work
closes. The base repository MUST be cloned locally first, and the project MUST
record source URL, local clone path, revision, license, usage mode, and any
required attribution text.

## Operating Constraints

Work-skills is designed for a locked-down Windows 11 corporate environment with
minimal installation rights. The target operating assumptions are:

- A local-first control plane serves HTML over `localhost`.
- The default downstream application profile is a browser-based localhost
  application using one blessed stack.
- Docker, hosted CI/CD, and GitHub issue workflows are treated as unavailable
  for normal delivery operations.
- Claude Code, Codex, and VS Code are available execution clients.
- A local LLM endpoint may be available for audit or orchestration assistance.
- The execution environment is same-user local access, so the system MUST
  detect, reconcile, and block unauthorized drift rather than promise perfect
  isolation.

## Workflow and Quality Gates

The canonical hierarchy for all managed work is:

- `initiative -> project -> wave -> task -> worktree`

The required baseline skill chain is:

- `plan-the-plan`
- `project-init`
- `project-lite`
- `grill-me`
- `speckit-constitution`
- `speckit-specify`
- `speckit-plan`
- `speckit-tasks`
- `project-next`
- `flow-auto <task_id>`
- `qa`
- `cicd-auditor`

Workflow requirements:

- `plan-the-plan` MUST frame the initiative before project-specific
  specification begins.
- `project-init` MUST establish the managed-project contract before a new
  project enters normal delivery.
- `project-next` MUST choose dependency-safe highest-value ready work.
- `flow-auto <task_id>` MUST operate within the task's dedicated worktree.
- `qa` MUST add or update tests when needed for the active task and MUST log
  repeatable validation evidence.
- `cicd-auditor` MUST block task or wave closure when drift, missing evidence,
  failed integrity checks, missing provenance, or expired exceptions are
  present.
- Exceptions MUST be explicit, time-boxed, locally recorded, and visible to all
  orchestration skills.

## Governance

This constitution supersedes convenience-driven shortcuts. All future planning,
skill design, task orchestration, and project onboarding work MUST demonstrate
compliance with these principles or record an explicit exception.

Governance rules:

- Amendments require a documented rationale, impact analysis, and migration
  guidance for affected projects or skills.
- Versioning follows semantic versioning:
  `MAJOR` for incompatible workflow or governance changes,
  `MINOR` for new mandatory principles or sections,
  `PATCH` for clarifications without behavioral change.
- All plans MUST include a constitution check before design work is accepted.
- Complexity MUST be justified when a project cannot follow the blessed
  contract, task model, or control-plane rules.
- Template alignment listed in the Sync Impact Report MUST be completed before
  broad rollout of additional work-skills initiatives.

**Version**: 1.0.0 | **Ratified**: 2026-04-01 | **Last Amended**: 2026-04-01
