# Provenance Ledger Contract

## Purpose

Define the required local ledger for any external repository, template, or
pattern used by a managed project.

## File Location

```text
.workskills/reference/provenance.yml
```

## Required Entry Fields

| Field | Required | Notes |
|------|----------|-------|
| `provenance_id` | yes | Stable local identifier |
| `source_repo_url` | yes | Canonical upstream URL |
| `local_clone_path` | yes | Local clone path used for inspection |
| `revision` | yes | Commit SHA or tag |
| `license` | yes | License captured at adoption time |
| `usage_mode` | yes | `reference`, `adapted`, `copied`, or `wrapped` |
| `artifacts_touched` | yes | Which local files or features were affected |
| `attribution_text` | yes | Required attribution summary |
| `linked_task_ids` | yes | Related tasks |
| `recorded_at` | yes | ISO timestamp |

## Workflow Rules

- The base repository MUST be cloned locally before adoption is approved
- Provenance entries MUST exist before related task or wave closure
- Missing revision or license data is blocking
- `cicd-auditor` MUST check provenance completeness before closure
