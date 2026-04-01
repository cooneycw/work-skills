# Managed Project Contract

## Purpose

Define the minimum local structure that every managed sibling repository must
publish so the `work-skills` control cockpit and skill bundle can operate
without custom repo-specific logic.

## Contract Root

Each managed project MUST expose a contract root at:

```text
.workskills/
```

## Required Files And Directories

```text
.workskills/
├── project.yml
├── reference/
│   ├── issues.snapshot.json
│   ├── integrity-baseline.json
│   ├── provenance.yml
│   ├── exceptions/
│   └── qa/
└── runtime/
    ├── issues.db
    └── rendered/
```

## Versioning Rules

- `project.yml` MUST contain `contract_version`
- Contract-breaking changes MUST increment the major version
- The control cockpit MUST refuse silent upgrades across incompatible contract
  versions

## `project.yml` Required Fields

| Field | Required | Notes |
|------|----------|-------|
| `project_id` | yes | Stable project identifier |
| `display_name` | yes | Human-readable name |
| `contract_version` | yes | Managed-project contract version |
| `initiative_id` | yes | Parent initiative identifier |
| `default_profile` | yes | Blessed application profile name |
| `specs_root` | yes | Relative path to spec-kit artifacts |
| `issue_db_path` | yes | Relative path to runtime SQLite issue store |
| `issue_snapshot_path` | yes | Relative path to normalized issue export |
| `provenance_ledger_path` | yes | Relative path to provenance ledger |
| `integrity_baseline_path` | yes | Relative path to baseline hash table |
| `qa_log_dir` | yes | Relative path to QA evidence directory |
| `rendered_output_dir` | yes | Relative path to generated HTML output |

## Git Rules

- `reference/` content SHOULD be version-controlled unless explicitly justified
- `runtime/` content SHOULD be excluded from version control
- The project MUST keep `.workskills/runtime/issues.db` out of git
- Generated rendered HTML MAY be kept in `runtime/rendered/` unless the project
  explicitly treats it as a review artifact

## Discovery Rules

- The control cockpit discovers projects through an explicit allowlist registry
- Projects not in the allowlist MUST NOT be auto-enrolled
- The cockpit reads sibling repos in read-only mode unless an explicit action
  targets one project

## Failure Modes

The project is considered contract-degraded when:

- `.workskills/project.yml` is missing
- required paths do not resolve
- `contract_version` is unsupported
- the normalized issue export is stale relative to sanctioned operations
- required provenance or integrity reference files are missing
