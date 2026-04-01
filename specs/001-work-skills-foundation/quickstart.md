# Quickstart: Work-Skills Phase 1 Operating Model

This quickstart describes the intended operator workflow after the architecture
in this feature is implemented on the Windows target environment.

## 1. Start the control cockpit

Launch the local control-plane application from `work-skills` and open the
cockpit in a browser on `localhost`.

Expected outcome:

- Portfolio overview is reachable locally
- Registered project list is visible
- No hosted issue system is required

## 2. Register or onboard a managed project

Add a sibling repository to the cockpit's allowlist and ensure it exposes the
managed-project contract under the standard local path.

Expected outcome:

- The project appears in the registry
- Contract health is visible
- Missing artifacts are flagged before work begins

## 3. Plan the initiative before project-specific implementation

Run the required planning chain:

1. `plan-the-plan`
2. `project-lite`
3. `grill-me`
4. `speckit-constitution`
5. `speckit-specify`
6. `speckit-plan`
7. `speckit-tasks`

Expected outcome:

- Initiative, wave, and task boundaries are clear
- Required skills and gates are recorded
- Project-local planning artifacts exist

## 4. Select the next task

Use `project-next` to choose the next dependency-safe highest-value ready task.

Expected outcome:

- One task is recommended with reasoning
- Blocking dependencies and health state are visible
- The task is ready for worktree creation if it is a coding task

## 5. Bind the task to a worktree

For a coding task, create or confirm the dedicated task worktree before any
code changes begin.

Expected outcome:

- The task references a worktree and branch
- The task can now enter the controlled execution flow

## 6. Run controlled task flow

Advance one task with `flow-auto <task_id>`, stopping at approval gates for:

1. task-context confirmation
2. implementation or patch review
3. QA evidence review
4. final audit and closure

Expected outcome:

- The flow never skips required gates
- Evidence is attached locally as the task advances

## 7. Execute QA and audit

Run `qa` to add or update tests or record repeatable validations. Then run
`cicd-auditor` to perform deterministic checks and optional LLM semantic review.

Expected outcome:

- Tests or validation logs are recorded locally
- Audit findings are linked to the task
- Drift, missing provenance, or missing commits block closure

## 8. Close the task and refresh the cockpit

Only after the required evidence, audit results, and commit linkage exist
should the task advance to `done`.

Expected outcome:

- The project-local reference files and the cockpit mirror are reconciled
- Portfolio health reflects the new state
- The next ready task becomes visible
