# Implementation Plan: Work-Skills Phase 1 Architecture Foundation

**Branch**: `[001-work-skills-foundation]` | **Date**: 2026-04-01 | **Spec**: `specs/001-work-skills-foundation/spec.md`
**Input**: Feature specification from `/specs/001-work-skills-foundation/spec.md`

## Summary

Define a local-first operating system for future executive automation projects:
one central control-plane web application inside `work-skills`, one blessed
delivery contract for managed sibling repositories, one required skill bundle,
one first-class task and worktree model, and one audit, integrity, and
provenance scheme that keeps delivery state reliable in a locked-down
same-user environment.

## Technical Context

**Language/Version**: Python 3.11+ for target implementation; Markdown, YAML, JSON, and SQL contracts for phase-1 artifacts  
**Primary Dependencies**: Django control plane, SQLite, Git worktrees, Spec Kit artifact workflow, Codex and Claude skill files, local LLM audit endpoint on port 3737  
**Storage**: Central control-plane SQLite store, per-project local SQLite issue store, and project-local reference files for specs, provenance, integrity baselines, QA evidence, and exceptions  
**Testing**: pytest, Django test runner, contract fixtures, deterministic audit checks, and repeatable QA evidence logs  
**Target Platform**: Locked-down Windows 11 userland with VS Code, browser access, local git, and limited install rights  
**Project Type**: Local-first control-plane web application plus reusable agent skill bundle and contract standard  
**Performance Goals**: Select the next ready task in under 5 seconds for a normal project; refresh portfolio state for 10 to 30 managed repos in under 30 seconds; complete deterministic task audit checks in under 30 seconds excluding optional LLM latency  
**Constraints**: No Docker, no routine GitHub issue dependency, minimal installation surface, single local cockpit preferred, all operational state local, approval gates required, same-user environment cannot rely on hard isolation  
**Scale/Scope**: Dozens of managed projects, hundreds of tasks and worktrees, one central operator cockpit, and one standardized delivery process

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- **Local-First Contract Authority**: PASS. The design keeps project artifacts
  local and uses the control plane as an index and sanctioned API path rather
  than the only readable store.
- **Blessed Delivery Pattern**: PASS. The plan defines one standard hierarchy,
  one required skill chain, and one default downstream application profile.
- **Task-Scoped Isolation and Approval Gates**: PASS. Every coding task is
  modeled as a first-class task with a dedicated worktree and approval gates.
- **Deterministic Verification Before LLM Judgment**: PASS. Deterministic audit,
  integrity, provenance, and QA checks run before the LLM auditor can influence
  closure.
- **Provenance and Attribution by Default**: PASS. The plan requires a local
  provenance ledger and cloned base repos before incorporation.

Post-design re-check: PASS. The selected contracts, models, and workflow docs
preserve the same rules without introducing architectural exceptions.

## Project Structure

### Documentation (this feature)

```text
specs/001-work-skills-foundation/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── checklists/
│   └── requirements.md
├── contracts/
│   ├── cicd-auditor-contract.md
│   ├── control-plane-api.md
│   ├── integrity-contract.md
│   ├── local-issue-store-contract.md
│   ├── managed-project-contract.md
│   ├── provenance-ledger-contract.md
│   └── skill-bundle-contract.md
└── tasks.md
```

### Source Code (repository root)

```text
control_plane/
├── manage.py
├── config/
├── apps/
│   ├── portfolio/
│   ├── registry/
│   ├── orchestration/
│   ├── audit/
│   ├── provenance/
│   └── contracts/
├── templates/
└── static/

skills/
├── plan-the-plan/
├── project-lite/
├── project-next/
├── flow-auto/
├── qa/
└── cicd-auditor/

docs/
├── contracts/
├── process/
└── examples/

tests/
├── contract/
├── integration/
├── fixtures/
│   └── managed_projects/
└── unit/
```

**Structure Decision**: Keep one central Django-based control plane and the
skill specifications in the `work-skills` repo. Managed application repos
remain outside this repository as sibling projects under the broader
`Projects/` workspace and are consumed through the managed-project contract.

## Complexity Tracking

No constitutional violations are currently justified. The design intentionally
avoids hard-isolation claims because the environment is same-user local access,
and instead treats drift detection and blocking audit gates as the reliability
mechanism.
