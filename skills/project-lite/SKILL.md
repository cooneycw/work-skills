---
name: project-lite
description: Build a lightweight operational brief for one managed project. Use when an agent needs fast familiarity with the current repo, active work, ready tasks, blockers, and audit state.
---

# Project Lite

Use this skill to familiarize an agent with one project without doing a broad
or expensive repo dive.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/contracts/managed-project-contract.md`
- `../../specs/001-work-skills-foundation/contracts/local-issue-store-contract.md`
- `../../specs/001-work-skills-foundation/contracts/integrity-contract.md`
- `../../specs/001-work-skills-foundation/contracts/provenance-ledger-contract.md`

Then read the target project's local contract and current planning artifacts.

## Output

Produce a short operational brief with:

- project purpose
- active initiative and wave
- open coding tasks
- ready next-task candidates
- blocked tasks and why
- open worktrees
- drift or provenance debt
- active exceptions

## Rules

- Prefer the project's contract, issue snapshot, and current spec artifacts over
  ad hoc repository scraping.
- Keep the brief concise and operational.
- Call out missing contract artifacts immediately.
- If the project is degraded, say so before recommending work.
