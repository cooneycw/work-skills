---
name: project-init
description: Initialize a new managed project to the work-skills contract. Use when creating a new sibling repo or onboarding a repo to the blessed local contract before normal delivery begins.
---

# Project Init

Use this skill after `plan-the-plan` when a new managed project must be created
or when an existing repo must be brought into the standard contract.

## Read First

- `../../.specify/memory/constitution.md`
- `../../specs/001-work-skills-foundation/contracts/managed-project-contract.md`
- `../../specs/001-work-skills-foundation/contracts/local-issue-store-contract.md`
- `../../specs/001-work-skills-foundation/contracts/provenance-ledger-contract.md`
- `../../specs/001-work-skills-foundation/contracts/skill-bundle-contract.md`

## Responsibilities

- define the new project's `project_id`, purpose, and initiative linkage
- establish the `.workskills/` contract root
- create the minimum contract files and directories
- declare the default downstream profile
- prepare the repo for Spec Kit planning artifacts
- state what still must be filled manually before the project is delivery-ready

## Minimum Output

Produce or define:

- `.workskills/project.yml`
- `.workskills/reference/issues.snapshot.json`
- `.workskills/reference/integrity-baseline.json`
- `.workskills/reference/provenance.yml`
- `.workskills/reference/exceptions/`
- `.workskills/reference/qa/`
- `.workskills/runtime/`
- the intended specs root for Spec Kit artifacts

## Rules

- Do not treat the project as fully ready until the contract is complete.
- Keep the setup minimal and deterministic.
- If this is a brownfield repo, note which parts are adapted rather than native.
- If the project depends on external sources, create provenance placeholders
  immediately so later work cannot ignore attribution.

## Handoff

After `project-init`, the normal sequence is:

1. `project-lite`
2. `grill-me`
3. `speckit-constitution`
4. `speckit-specify`
5. `speckit-plan`
6. `speckit-tasks`
