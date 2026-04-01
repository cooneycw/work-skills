# Tasks: Work-Skills Phase 1 Architecture Foundation

**Input**: Design documents from `/specs/001-work-skills-foundation/`  
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/

**Tests**: Tests are required for all behavior that affects task flow, audit
gates, project contract parsing, or portfolio state selection.

## Phase 1: Setup (Shared Infrastructure)

- [ ] T001 Create the initial `control_plane/` Django project structure and base
  settings for local-only operation
- [ ] T002 Create the `skills/` directory structure for the required baseline
  skill bundle
- [ ] T003 [P] Add `tests/fixtures/managed_projects/` with sample contract
  layouts, issue exports, provenance ledgers, and integrity baselines

## Phase 2: Foundational (Blocking Prerequisites)

- [ ] T004 Implement registry models and services for an explicit allowlist of
  managed sibling project roots
- [ ] T005 [P] Implement managed-project contract parsing for
  `.workskills/project.yml`
- [ ] T006 [P] Implement the project-local SQLite issue adapter and normalized
  issue export reader
- [ ] T007 Implement portfolio synchronization that reconciles contract,
  snapshot, provenance, integrity, and exception surfaces
- [ ] T008 Implement worktree binding models and validation rules for coding
  tasks
- [ ] T009 Implement provenance and integrity models, storage, and comparison
  services
- [ ] T010 Implement `cicd-auditor` deterministic checks and result persistence

## Phase 3: User Story 1 - Standardize Initiative Planning (Priority: P1)

**Goal**: Produce a repeatable initiative-planning chain before project-specific
specification begins

**Independent Test**: A new initiative can be framed into standard artifacts
and required skills from the control cockpit

### Tests For User Story 1

- [ ] T011 [P] [US1] Add contract tests for initiative creation and required
  skill-chain emission in `tests/contract/test_initiative_planning.py`
- [ ] T012 [P] [US1] Add integration tests for initiative framing through the
  cockpit in `tests/integration/test_initiative_flow.py`

### Implementation For User Story 1

- [ ] T013 [US1] Implement `plan-the-plan` skill specification and artifact
  outputs in `skills/plan-the-plan/SKILL.md`
- [ ] T014 [US1] Implement `project-init` skill specification and managed
  project bootstrap outputs in `skills/project-init/SKILL.md`
- [ ] T015 [US1] Implement `project-lite` skill specification and brief format
  in `skills/project-lite/SKILL.md`
- [ ] T016 [US1] Implement initiative and wave views plus supporting services in
  `control_plane/apps/portfolio/`

## Phase 4: User Story 2 - Standardize Managed Project Contracts (Priority: P1)

**Goal**: Onboard sibling repositories to a blessed contract with first-class
task and worktree state

**Independent Test**: A sample managed repo can be registered and parsed
without custom project logic

### Tests For User Story 2

- [ ] T017 [P] [US2] Add contract tests for `.workskills/project.yml`,
  normalized issue exports, and provenance ledgers in
  `tests/contract/test_managed_project_contract.py`
- [ ] T018 [P] [US2] Add integration tests for project sync and drift detection
  in `tests/integration/test_project_sync.py`

### Implementation For User Story 2

- [ ] T019 [US2] Implement `project-next` selection service and API route in
  `control_plane/apps/orchestration/`
- [ ] T020 [US2] Implement `flow-auto <task_id>` state machine and approval gate
  handling in `control_plane/apps/orchestration/`
- [ ] T021 [US2] Implement sample managed-project templates and reference
  outputs in `docs/examples/`

## Phase 5: User Story 3 - See Cross-Project Delivery State (Priority: P2)

**Goal**: Provide one local cockpit for project health, ready tasks, and drift

**Independent Test**: Two or more managed projects render correctly in one
portfolio view with clear health differences

### Tests For User Story 3

- [ ] T022 [P] [US3] Add contract tests for portfolio summary serialization in
  `tests/contract/test_portfolio_summary.py`
- [ ] T023 [P] [US3] Add integration tests for portfolio rendering and
  filtering in `tests/integration/test_portfolio_views.py`

### Implementation For User Story 3

- [ ] T024 [US3] Implement project registry, portfolio overview, and project
  detail views in `control_plane/apps/portfolio/`
- [ ] T025 [US3] Implement local rendered HTML outputs and refresh hooks in
  `control_plane/apps/portfolio/`

## Phase 6: User Story 4 - Control Task Execution Through Gates (Priority: P3)

**Goal**: Advance tasks through worktree-backed delivery with QA and blocking
audit checks

**Independent Test**: A coding task can be advanced from ready to done only
when all required evidence is present

### Tests For User Story 4

- [ ] T026 [P] [US4] Add contract tests for task state transitions and gate
  enforcement in `tests/contract/test_task_flow.py`
- [ ] T027 [P] [US4] Add integration tests for audit-blocked and
  exception-allowed closure in `tests/integration/test_audit_flow.py`

### Implementation For User Story 4

- [ ] T028 [US4] Implement `qa` skill specification and evidence logging model
  in `skills/qa/SKILL.md`
- [ ] T029 [US4] Implement `cicd-auditor` skill specification and deterministic
  audit engine integration in `skills/cicd-auditor/SKILL.md`
- [ ] T030 [US4] Implement exception management and expiry handling in
  `control_plane/apps/audit/`

## Phase 7: Polish & Cross-Cutting Concerns

- [ ] T031 [P] Document operator workflows, onboarding steps, and provenance
  rules in `docs/process/`
- [ ] T032 Validate quickstart flows against the implemented control cockpit
- [ ] T033 Add regression coverage for next-task ranking, sync drift, and
  provenance blocking behavior
