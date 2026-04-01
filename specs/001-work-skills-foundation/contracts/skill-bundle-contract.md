# Skill Bundle Contract

## Purpose

Define the required skill set for all managed initiatives and projects.

## Required Skills

| Skill | Purpose | Required Inputs | Expected Outputs | Allowed Writes |
|------|---------|-----------------|------------------|----------------|
| `plan-the-plan` | Frame an initiative before any project-specific specification | objective, constraints, portfolio context | initiative brief, wave outline, required skill bundle | planning docs only |
| `project-init` | Initialize a new managed project or onboard a repo to the blessed contract | initiative brief, project identity, contract standard | contract root, contract files, onboarding notes | contract files only |
| `project-lite` | Brief an agent on the current state of one project | project contract, active specs, open tasks, worktree map, audit history | concise operational brief | none |
| `grill-me` | Stress-test assumptions and close planning gaps | active plan or design question | clarified decisions and follow-up questions | planning docs only |
| `speckit-constitution` | Define project governance | repo context, approved principles | constitution update | constitution and aligned templates |
| `speckit-specify` | Write the feature spec | initiative or feature description | `spec.md`, checklist | spec docs |
| `speckit-plan` | Produce technical design artifacts | approved spec and constraints | `plan.md`, research, contracts, data model, quickstart | planning docs |
| `speckit-tasks` | Produce actionable task breakdown | approved plan | `tasks.md` | task docs |
| `project-next` | Select the best ready task | project state, dependencies, priorities, exceptions | ranked next-task recommendation | none |
| `flow-auto <task_id>` | Drive one task through controlled stages | task record, worktree, approvals | updated task state and evidence requests | sanctioned task-flow writes only |
| `qa` | Add or update tests or record repeatable validations | active task, code state, acceptance criteria | tests and QA evidence | task QA records and tests |
| `cicd-auditor` | Block or approve progression based on deterministic and semantic checks | task state, evidence, provenance, integrity, git state | audit result and findings | audit records only |

## Sequencing Rules

The minimum required sequence for new work is:

1. `plan-the-plan`
2. `project-init`
3. `project-lite`
4. `grill-me`
5. `speckit-constitution`
6. `speckit-specify`
7. `speckit-plan`
8. `speckit-tasks`

Task execution then uses:

9. `project-next`
10. `flow-auto <task_id>`
11. `qa`
12. `cicd-auditor`

## Gate Rules

- `flow-auto <task_id>` MUST stop at approval gates
- `qa` MUST run before `cicd-auditor` can approve closure
- `cicd-auditor` MUST run before a task or wave closes
- Optional supporting skills MAY exist, but they MUST NOT replace the required
  bundle or bypass its gates
