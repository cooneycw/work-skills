# Feature Specification: Work-Skills Phase 1 Architecture Foundation

**Feature Branch**: `[001-work-skills-foundation]`  
**Created**: 2026-04-01  
**Status**: Draft  
**Input**: User description: "Define the phase 1 architecture, contracts, and workflow for the work-skills control plane, managed-project standard, and core skill bundle."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Standardize Initiative Planning (Priority: P1)

An executive operator can start a new initiative with a fixed planning process
that produces consistent local artifacts, a required skill chain, wave
boundaries, and success criteria before implementation begins.

**Why this priority**: Without a reliable initiative-framing process, every
future project will drift into one-off planning and inconsistent delivery.

**Independent Test**: From an empty managed project, an operator can produce an
initiative brief, required skills, wave outline, and initial spec/plan/task
artifacts that follow the same contract as every other project.

**Acceptance Scenarios**:

1. **Given** an operator wants to start a new internal initiative, **When**
   they run the required planning sequence, **Then** the initiative is framed
   using the standard hierarchy, required skills, and local planning artifacts.
2. **Given** two different initiatives are started by the same system, **When**
   their initial planning outputs are compared, **Then** both follow the same
   artifact layout and governance rules.

---

### User Story 2 - Standardize Managed Project Contracts (Priority: P1)

A project owner can onboard a sibling repository to a blessed local contract so
that tasks, provenance, audit evidence, and integrity baselines are visible and
repeatable without relying on hosted services.

**Why this priority**: The control plane cannot manage projects consistently
unless each project exposes the same contract and local tracking surfaces.

**Independent Test**: A sample managed project can publish the required
contract, local issue mirror, provenance ledger, and integrity baseline, and
the control plane can read them without custom per-project logic.

**Acceptance Scenarios**:

1. **Given** a sibling repository is registered as a managed project, **When**
   it exposes the standard contract, **Then** its planning, issue, provenance,
   and audit surfaces can be discovered deterministically.
2. **Given** a project is missing a required artifact, **When** the project is
   audited, **Then** the missing contract element is flagged as blocking or
   excepted instead of being silently ignored.

---

### User Story 3 - See Cross-Project Delivery State (Priority: P2)

An operator can use one local control cockpit to understand what projects are
active, which tasks are ready next, where drift exists, and what work is
blocked across the entire portfolio.

**Why this priority**: Portfolio visibility is essential for directing work
without opening every repository manually.

**Independent Test**: Given two or more managed projects with different states,
the operator can open one local view and identify current health, next logical
work, and unresolved drift for each project.

**Acceptance Scenarios**:

1. **Given** several managed projects are registered, **When** the operator
   opens the control cockpit, **Then** they can see project health, active
   waves, ready tasks, and audit results across the portfolio.
2. **Given** one project is healthy and another has unresolved drift, **When**
   the portfolio is refreshed, **Then** the difference is obvious and traceable
   to specific artifacts or task states.

---

### User Story 4 - Control Task Execution Through Gates (Priority: P3)

A delivery operator can move a coding task through a controlled lifecycle that
uses dedicated worktree isolation, approval gates, QA evidence, and blocking
audit checks before closure.

**Why this priority**: Reliable delivery depends on disciplined task execution,
not just good planning.

**Independent Test**: A coding task can be selected, assigned a worktree,
advanced through planning, implementation, QA, and audit gates, and either
closed or blocked based on recorded evidence.

**Acceptance Scenarios**:

1. **Given** a coding task is ready to start, **When** the delivery operator
   advances it into execution, **Then** it is bound to a dedicated worktree and
   cannot skip required approval or audit stages.
2. **Given** a task has unrecorded drift, missing evidence, or missing
   provenance, **When** closure is attempted, **Then** the task is blocked or
   routed through an explicit exception path.

### Edge Cases

- A managed project contains planning artifacts but no project contract.
- A task record exists in a local database mirror but not in the normalized
  export or task plan.
- A direct local edit changes issue state outside the sanctioned API path.
- A worktree remains open after its task is marked done.
- A provenance ledger omits the source revision or license for a borrowed repo.
- An exception expires while a task or wave is still in progress.
- The control cockpit is unavailable temporarily and projects must continue to
  retain local delivery truth.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The system MUST define a required baseline skill bundle for all
  managed initiatives and projects.
- **FR-002**: The system MUST include a pre-spec planning pattern that frames
  initiative scope, waves, success criteria, and the required skill bundle
  before project-specific specification begins.
- **FR-003**: The system MUST enforce one canonical hierarchy of
  `initiative -> project -> wave -> task -> worktree`.
- **FR-004**: The system MUST allow managed applications to remain separate
  sibling repositories rather than forcing them into a monorepo.
- **FR-005**: Every managed project MUST publish a standard local contract that
  allows the control cockpit and skills to operate without custom project logic.
- **FR-006**: Every coding task MUST have a stable `task_id` and a dedicated
  worktree before implementation begins.
- **FR-007**: The system MUST treat task issues as first-class local objects
  with dependencies, lifecycle state, health state, audit linkage, and commit
  linkage.
- **FR-008**: The system MUST provide a deterministic method for selecting the
  next dependency-safe highest-value ready task.
- **FR-009**: The system MUST provide a controlled delivery flow for one task at
  a time that stops at named approval gates.
- **FR-010**: The system MUST keep planning, tracking, audit, and provenance
  data locally resident within each project and the central control cockpit.
- **FR-011**: The system MUST mirror project delivery state between local
  project artifacts and a central control-plane store without allowing silent
  divergence.
- **FR-012**: The sanctioned write path to SQL-backed project and control-plane
  state MUST be the local control-plane API.
- **FR-013**: The system MUST detect unsupported direct state changes through
  reconciliation, operation provenance, and integrity comparison.
- **FR-014**: The system MUST run deterministic verification before any LLM
  semantic judgment is allowed to influence task or wave progression.
- **FR-015**: The system MUST support QA execution that either adds tests or
  records repeatable validations with locally stored evidence.
- **FR-016**: The system MUST provide blocking audit checks for task and wave
  closure, with explicit time-boxed exceptions when a human accepts risk.
- **FR-017**: The system MUST require a provenance ledger for any external repo,
  template, or pattern incorporated into a managed project.
- **FR-018**: The system MUST support locally derived HTML or similar visual
  views so operators can inspect project and task state without relying on
  hosted tools.
- **FR-019**: The system MUST define one blessed default application profile for
  downstream project scaffolding so planning and tasking remain consistent.
- **FR-020**: The system MUST remain operable in a locked-down local environment
  with limited install rights and no routine dependence on hosted issue systems.

### Key Entities *(include if feature involves data)*

- **Initiative**: The executive objective that sets portfolio intent, success
  criteria, and participating projects.
- **Managed Project**: A sibling repository that conforms to the work-skills
  project contract and exposes standard planning, issue, provenance, and audit
  surfaces.
- **Wave**: A deliverable slice within an initiative that groups tasks under a
  common objective and exit criteria.
- **Task**: A first-class executable unit with dependency data, lifecycle
  state, health state, audit evidence, and commit linkage.
- **Worktree Binding**: The isolated coding environment associated with a
  coding task.
- **Provenance Entry**: A local record of an external repository, template, or
  pattern that contributes to project work.
- **Integrity Snapshot**: A normalized set of hashes used to detect drift
  between expected and current project state.
- **Audit Run**: The recorded result of deterministic checks and any LLM-based
  semantic review for a task, wave, or project.
- **Exception Record**: A time-boxed allowance that explains why a blocking
  rule is temporarily overridden.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A new initiative can be framed into the standard planning
  hierarchy, required skill bundle, and local artifacts in under 30 minutes.
- **SC-002**: 100% of coding tasks accepted into execution receive a stable
  `task_id`, dependency record, and dedicated worktree before implementation
  begins.
- **SC-003**: 100% of tasks closed through the standard flow include linked
  planning references, QA evidence, audit results, and at least one associated
  commit reference.
- **SC-004**: Any drift between sanctioned local project state and mirrored
  control-plane state is detected before a task can move to a closed state.
- **SC-005**: An operator can identify the next ready task and current health
  state for any registered project from one local cockpit in under one minute.
- **SC-006**: 100% of incorporated external repositories or templates are
  recorded in a local provenance ledger before their related tasks or waves are
  closed.

## Assumptions

- Managed projects can expose local files and a local issue-state mirror even if
  the full control cockpit is temporarily unavailable.
- Agents, editor tooling, and the control cockpit run in a same-user local
  environment, so hard technical isolation is weaker than hosted boundaries.
- Hosted issue systems are not required for normal delivery, even if git
  remotes exist for backup or later publication.
- Downstream projects may eventually be split out of the portfolio, so each
  project must remain portable and self-describing.
- The actual control-plane implementation, Windows setup, and local LLM wiring
  will occur later; this feature defines the phase-1 operating model and
  contracts.
