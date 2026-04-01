---
name: project-next
description: Select the next dependency-safe highest-value ready task for a managed project. Use when the user asks what should be worked next or when orchestration needs a deterministic next-task recommendation.
---

# Project Next

Use this skill to recommend one task to work next. This skill is read-only.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/contracts/local-issue-store-contract.md`
- `../../specs/001-work-skills-foundation/contracts/integrity-contract.md`
- `../../specs/001-work-skills-foundation/contracts/cicd-auditor-contract.md`

Then read the target project's:

- contract manifest
- normalized issue export
- open exceptions
- current wave/task artifacts

## Ranking Policy

Rank ready work by:

1. dependency satisfaction
2. blocked vs ready state
3. wave priority
4. strategic value
5. risk reduction
6. effort and size
7. staleness penalty for abandoned worktrees

## Output

Return:

- one recommended `task_id`
- why it was chosen
- the next two candidates, if useful
- blockers for higher-priority tasks that were skipped

## Rules

- Never recommend a coding task that lacks the required worktree binding plan.
- Never hide blocking drift, missing provenance, or expired exceptions.
- Do not mutate task state from this skill.
