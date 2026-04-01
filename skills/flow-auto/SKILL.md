---
name: flow-auto
description: Drive one task through the standard delivery flow with approval gates. Use when executing a specific task_id from planning through implementation, QA, and audit preparation.
---

# Flow Auto

Use this skill for one `task_id` at a time.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/contracts/skill-bundle-contract.md`
- `../../specs/001-work-skills-foundation/contracts/local-issue-store-contract.md`
- `../../specs/001-work-skills-foundation/contracts/control-plane-api.md`
- `../../specs/001-work-skills-foundation/contracts/cicd-auditor-contract.md`

Then read for the target project and task:

- current spec, plan, and tasks artifacts
- task record and dependencies
- worktree binding
- active exceptions
- relevant QA and audit history

## Required Flow

1. confirm the task context and acceptance intent
2. verify dependencies and worktree scope
3. implement only within the task's worktree
4. stop for review at the planned approval gate
5. run or prepare QA evidence
6. prepare for `cicd-auditor`
7. stop again before closure

## Rules

- Operate only inside the task's dedicated worktree for coding tasks.
- Use the sanctioned API path or sanctioned repo artifacts. Do not write SQL
  directly.
- Do not auto-close tasks.
- Stop at approval gates rather than running end to end.
- If dependencies, provenance, QA evidence, or drift status are not acceptable,
  stop and report the exact blocker.
