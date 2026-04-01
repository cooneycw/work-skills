---
name: plan-the-plan
description: Frame a new initiative before project-specific specification begins. Use when converting an executive objective into projects, waves, success criteria, and the required skill chain.
---

# Plan The Plan

Use this skill before `speckit-specify` when the user is starting a new
initiative or redefining an existing one.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/spec.md`
- `../../specs/001-work-skills-foundation/plan.md`
- `../../specs/001-work-skills-foundation/contracts/skill-bundle-contract.md`
- `../../specs/001-work-skills-foundation/contracts/managed-project-contract.md`

## Output

Produce an initiative brief that includes:

- objective
- scope boundaries
- participating projects
- wave breakdown
- success criteria
- required skill chain
- major risks and open questions

## Rules

- Use the canonical hierarchy:
  `initiative -> project -> wave -> task -> worktree`
- Default to the blessed downstream profile unless an exception is explicit.
- Keep this stage technology-light. Focus on operating model, boundaries, and
  sequencing.
- If the initiative spans multiple repos, decide which repo is the control repo
  and which repos are managed projects.
- If a new project is needed, state that it must satisfy the managed-project
  contract before normal delivery begins.

## Handoff

After this brief is stable, the normal sequence is:

1. `project-init`
2. `project-lite`
3. `grill-me`
4. `speckit-constitution`
5. `speckit-specify`
6. `speckit-plan`
7. `speckit-tasks`
