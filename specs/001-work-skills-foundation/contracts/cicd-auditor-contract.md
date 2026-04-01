# CI/CD Auditor Contract

## Purpose

Define the blocking gatekeeper behavior for `cicd-auditor`.

## Audit Phases

### Phase 1: Deterministic Checks

The auditor MUST verify:

- task exists and is linked to the current plan and task artifacts
- required task state transition is valid
- coding tasks have a bound worktree
- expected tests or QA evidence are present
- normalized issue export matches sanctioned task state
- integrity baseline comparison is current
- provenance entries exist for any adopted external sources
- related commit references exist before closure
- worktree and git status are acceptable for the requested transition

### Phase 2: Optional LLM Semantic Review

If a local LLM audit endpoint is configured, the auditor MAY request a semantic
review of:

- whether the implementation aligns with the tracked task
- whether closure evidence matches the claimed scope
- whether missing updates suggest spec or plan drift

LLM review cannot override a failed deterministic check.

## Outcomes

| Result | Meaning | Blocking |
|--------|---------|----------|
| `pass` | All required checks satisfied | no |
| `warn` | Non-blocking concern recorded | no |
| `fail` | Blocking check failed | yes |
| `excepted` | Blocking issue covered by an active exception | conditional |

## Required Findings Output

Each audit run MUST record:

- `audit_id`
- `scope_type`
- `scope_id`
- deterministic findings
- optional LLM findings
- evidence paths
- blocking decision
- linked `operation_id`

## Blocking Rules

The auditor MUST block closure when:

- drift is unresolved
- commit evidence is missing for a completed coding task
- required QA evidence is missing
- provenance is missing for adopted external work
- integrity hashes differ without approval
- an exception is missing, expired, or out of scope
