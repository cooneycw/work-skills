---
name: cicd-auditor
description: Perform blocking audit checks for tasks, waves, or projects. Use when deciding whether work may advance or close based on deterministic evidence, integrity status, provenance, and optional LLM review.
---

# CI/CD Auditor

This skill is the gatekeeper. Run deterministic checks first and only then use
optional LLM judgment.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/contracts/cicd-auditor-contract.md`
- `../../specs/001-work-skills-foundation/contracts/integrity-contract.md`
- `../../specs/001-work-skills-foundation/contracts/provenance-ledger-contract.md`
- `../../specs/001-work-skills-foundation/contracts/control-plane-api.md`

Then read for the target scope:

- task or wave record
- normalized issue export
- integrity baseline and current diff
- provenance ledger
- QA evidence
- worktree and git state

## Deterministic Checks

Verify:

- the requested transition is valid
- required artifacts exist and are current
- coding tasks have worktree and commit evidence
- QA evidence exists
- integrity drift is resolved or explicitly excepted
- provenance is complete
- exceptions are active, in scope, and not expired

## Optional LLM Review

If a local audit model is configured, evaluate:

- whether the implementation matches the tracked task
- whether claimed completion exceeds the evidence
- whether there is likely spec or plan drift

LLM review cannot override failed deterministic checks.

## Output

Return:

- `pass`, `warn`, `fail`, or `excepted`
- exact blocking findings
- evidence reviewed
- recommended next action

## Rules

- Do not waive blocking findings silently.
- Do not update closure state unless the caller explicitly requests it and all
  blocking conditions are satisfied.
