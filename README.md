# work-skills

`work-skills` is the control repo for a local-first executive automation
workflow. It is intended to hold:

- Spec Kit based planning artifacts
- reusable Codex and Claude skills
- the future central Django control cockpit
- the contract that managed sibling repos must follow

The target environment is a locked-down Windows 11 corporate machine where
local development must avoid heavy infrastructure, hosted issue systems, and
non-essential install steps.

## Current State

This repository is currently a scaffold:

- Spec Kit has been initialized locally
- agent skills were generated into `.agents/skills/`
- a first feature branch scaffold exists under `specs/001-work-skills-foundation/`
- canonical repo-local skill specs live under `skills/`
- the actual Django implementation and Windows-specific LLM wiring are still to
  be built

## Corporate Environment Assumptions

The structure is being designed for an environment with these constraints:

- Windows 11 userland
- very limited ability to install software
- Python available from a corporate package source
- VS Code with Codex and Claude access
- browser access for localhost tools
- optional local LLM endpoint on port `3737`
- git available locally
- no dependence on GitHub issues or hosted CI/CD during normal delivery

## How To Initiate Development In The Corporate Environment

### 1. Clone the repo locally

Clone this repo into your normal projects workspace on the corporate machine.

Recommended location:

```text
<Projects>/work-skills
```

### 2. Verify the minimum toolchain

Before writing code, confirm you have:

- `git`
- a corporate-approved Python interpreter
- VS Code
- Codex and/or Claude access inside VS Code
- browser access to `localhost`

Optional but useful:

- a local LLM audit endpoint on port `3737`

### 3. Create a local Python environment if allowed

If `.venv` is allowed in the corporate environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

If `.venv` is not allowed, use the approved local Python interpreter directly
and keep the dependency footprint minimal.

### 4. Start from the planning scaffold, not from code

The first implementation work should be planning-first:

1. fill the project constitution in `.specify/memory/constitution.md`
2. complete the phase-1 feature spec in
   `specs/001-work-skills-foundation/spec.md`
3. complete the implementation plan in
   `specs/001-work-skills-foundation/plan.md`
4. generate or maintain `tasks.md` before building the control plane

The repo should not jump directly into Django code until the operating contract
is written down.

### 4.1 Immediate build order

If you are starting fresh on the corporate machine, use this order:

1. review the constitution in `.specify/memory/constitution.md`
2. review the phase-1 spec package in `specs/001-work-skills-foundation/`
3. review the canonical skill specs in `skills/`
4. finalize any contract changes before scaffolding Django
5. scaffold `control_plane/` and `tests/`
6. implement the managed-project contract parser and sync flow
7. implement `project-next`, `flow-auto`, `qa`, and `cicd-auditor`
8. only then start onboarding sibling application repos

This is the intended answer to “how do I start building this project?”

### 5. Build the central control plane inside this repo

The recommended target structure is:

```text
work-skills/
├── control_plane/   # future Django project
├── skills/          # reusable local skill definitions
├── docs/            # process and contract docs
├── specs/           # spec-kit feature artifacts
├── tests/           # contract, integration, and unit tests
├── .agents/skills/  # generated spec-kit skills
└── .specify/        # spec-kit templates and scripts
```

The control plane should become the primary planning and audit cockpit, while
VS Code remains the execution surface for coding tasks.

### 6. Keep managed applications outside this repo

Future applications should live as sibling repositories, not inside
`work-skills`.

Recommended workspace shape:

```text
Projects/
├── work-skills
├── project-a
├── project-b
└── project-c
```

Each managed project should later expose a standard local contract so the
control plane can scan it without custom project logic.

### 7. Use local-only operational rules

When implementation begins on the corporate machine, keep these rules:

- use one local Django control plane
- use SQLite where structured local state is required
- use git worktrees for coding tasks
- keep hosted dependencies out of the delivery loop
- keep provenance and attribution records locally
- make tests and audit evidence part of the normal task flow

### 8. Implement in thin, reviewable waves

Recommended order:

1. finalize the architecture and contracts
2. scaffold the Django control plane
3. add project registry and portfolio views
4. add task/worktree orchestration
5. add QA and audit flows
6. add skill implementations

### 9. Use the skill specs as the operating guide

The top-level `skills/` directory is the canonical specification for the
non-Spec-Kit skills in this repo:

- `skills/plan-the-plan/`
- `skills/project-lite/`
- `skills/project-next/`
- `skills/flow-auto/`
- `skills/qa/`
- `skills/cicd-auditor/`

These specs define how the future Django control plane and agent workflow are
expected to behave. Implement the platform to satisfy these skills, rather than
inventing the process during coding.

## What This Repo Is For

This repo is for:

- standardizing project planning
- defining reusable skills
- enforcing local tracking and audit rules
- serving as the dogfood control cockpit for all managed projects

This repo is not for:

- hosting every downstream application
- relying on GitHub issues for day-to-day delivery
- assuming Docker, Redis, Postgres, or hosted CI are available

## Suggested First Development Milestone

The first milestone on the corporate machine should be:

- complete the phase-1 spec and plan
- define the managed-project contract
- define the task/worktree model
- define the `cicd-auditor` contract
- scaffold the Django control plane without deep integrations yet

## Notes

- The public repository can safely hold the scaffold and generic planning
  assets.
- Corporate-specific configuration, credentials, and machine-local settings
  should remain out of version control.
