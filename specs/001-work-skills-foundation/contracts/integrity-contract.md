# Integrity Contract

## Purpose

Define how project integrity baselines are computed and compared.

## Hash Inputs

The integrity system hashes normalized content for:

- `.workskills/project.yml`
- `.workskills/reference/issues.snapshot.json`
- `.workskills/reference/provenance.yml`
- `.workskills/reference/integrity-baseline.json`
- open exception records
- required Spec Kit planning artifacts
- worktree metadata export
- selected rendered outputs when they are part of the delivery record

## Explicit Non-Goal

The raw SQLite issue database file MUST NOT be the primary integrity input.
Instead, the normalized logical export of issue state is hashed.

## Baseline Rules

- A baseline is established only after approved task or wave closure
- A baseline update MUST be linked to an `operation_id`
- An unexpected hash difference without a matching sanctioned operation is
  treated as drift

## Drift Classes

| Drift Class | Meaning |
|------------|---------|
| `content-drift` | Required artifacts changed without sanctioned tracking |
| `sync-drift` | Local mirror and central index disagree |
| `provenance-drift` | Referenced external source lacks recorded provenance |
| `closure-drift` | Task claims completion but supporting artifacts are stale |

## Required Output

The integrity comparison result MUST include:

- baseline hash set
- current hash set
- changed artifacts
- matched `operation_id`, if any
- recommended blocking status
