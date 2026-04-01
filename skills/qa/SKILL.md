---
name: qa
description: Add or update tests and record repeatable validation evidence for an active task. Use when a task needs test coverage, deterministic validation, or auditable QA notes before closure.
---

# QA

Use this skill to strengthen task reliability and create repeatable evidence.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/contracts/local-issue-store-contract.md`
- `../../specs/001-work-skills-foundation/contracts/cicd-auditor-contract.md`

Then read for the active project and task:

- acceptance criteria from spec and plan
- task record
- current tests
- prior QA evidence

## Responsibilities

- add or update tests when the gap is directly tied to the active task
- record repeatable manual or scripted validations when tests are not the whole
  answer
- capture evidence paths, commands, expected outcomes, and observed outcomes

## Rules

- Prefer deterministic tests where possible.
- If a manual validation is required, make it repeatable and auditable.
- Never claim a pass without evidence.
- Keep QA changes scoped to the active task unless a broader fix is explicitly
  justified.

## Output

Report:

- tests added or updated
- validations performed
- evidence locations
- remaining quality risk
