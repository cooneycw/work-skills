# Research: Work-Skills Phase 1 Architecture Foundation

## Decision 1: Keep the control cockpit inside `work-skills`

- **Decision**: Implement the central control cockpit as a bounded Django
  subproject inside the `work-skills` repository.
- **Rationale**: One repo keeps the planning standards, contracts, skill specs,
  and control-plane code aligned. It also matches the requirement for one local
  HTML-serving cockpit rather than multiple per-project services.
- **Alternatives considered**:
  - Separate cockpit repo: rejected for phase 1 because it would split the core
    workflow standard from the tool that enforces it.
  - No cockpit yet: rejected because cross-project visibility is a primary
    planning objective, not a later convenience.

## Decision 2: Keep managed applications as sibling repositories

- **Decision**: Downstream applications remain separate sibling repositories
  under the broader `Projects/` workspace.
- **Rationale**: This preserves portability, lets projects be split out later,
  and keeps the control plane from becoming a monorepo manager.
- **Alternatives considered**:
  - Monorepo: rejected because it couples unrelated applications and makes later
    extraction harder.
  - Nested apps inside `work-skills`: rejected because the repo's job is to
    standardize and orchestrate work, not contain every application.

## Decision 3: Use one blessed downstream application profile

- **Decision**: Standardize future application planning on a browser-based
  localhost application profile using one blessed stack.
- **Rationale**: The target environment is locked down, and one default stack
  lowers architectural variance across projects.
- **Alternatives considered**:
  - Stack-agnostic project starts: rejected because they would weaken the value
    of shared skills and make tasking less predictable.
  - Desktop-native defaults first: rejected because the browser debugging and
    localhost model are more compatible with the stated environment.

## Decision 4: Use dual-write mirrored state with reconciliation

- **Decision**: Mirror task and project state between project-local artifacts
  and the control-plane store, with the sanctioned SQL write path going through
  the control-plane API.
- **Rationale**: The operator wants both local durability and central portfolio
  visibility. In a same-user environment, reconciliation is more realistic than
  pretending direct bypass is impossible.
- **Alternatives considered**:
  - Files only: rejected because deterministic orchestration and ranking are
    harder without a structured local issue store.
  - Central DB only: rejected because projects must remain portable and locally
    intelligible.

## Decision 5: Store project issue state in local SQLite plus normalized exports

- **Decision**: Each managed project uses a local SQLite issue store for
  working state and a normalized export for integrity comparison and durable
  mirroring.
- **Rationale**: SQLite is practical in the locked-down environment, while the
  normalized export avoids treating the raw SQLite file as the audit baseline.
- **Alternatives considered**:
  - Commit raw SQLite files: rejected because diffs, merges, and worktrees would
    be noisy and brittle.
  - File-per-issue only: rejected because the operator explicitly prefers a
    project-local SQL-backed issue model.

## Decision 6: Give each coding task its own worktree

- **Decision**: Every coding task gets a first-class task record and a
  dedicated git worktree by default.
- **Rationale**: Worktrees make task isolation, commit evidence, and
  gatekeeping more reliable. They also give `flow-auto <task_id>` a clean
  execution scope.
- **Alternatives considered**:
  - Shared branch for multiple tasks: rejected because it weakens auditability.
  - Optional worktrees: rejected because the operator wants this pattern at all
    times for coding tasks.

## Decision 7: Make deterministic audit precede LLM review

- **Decision**: `cicd-auditor` runs deterministic checks first and uses the LLM
  only as a second-stage semantic reviewer.
- **Rationale**: Reliability depends on repeatable mechanical checks before
  probabilistic judgment is trusted.
- **Alternatives considered**:
  - LLM-only gatekeeper: rejected because it is too easy to make
    non-repeatable decisions.
  - No LLM audit: rejected because semantic drift between code and tracked task
    intent is still important to catch.

## Decision 8: Make provenance and cloned base repos mandatory

- **Decision**: Any external repo or template must be cloned locally first and
  recorded in a provenance ledger before related work closes.
- **Rationale**: Attribution is a hard requirement, and cloned local references
  make later audit and adaptation work practical.
- **Alternatives considered**:
  - Informal notes in tasks: rejected because provenance would drift or be lost.
  - URLs without local clones: rejected because the operator wants a locally
    inspectable source base before adoption.

## Decision 9: Put Django in charge of the cockpit, not the editor

- **Decision**: Treat Django as the primary workflow cockpit and VS Code as the
  execution client for coding and agent runs.
- **Rationale**: This matches the desired process shift without requiring phase
  1 to replace or embed the editor chat surface directly.
- **Alternatives considered**:
  - VS Code remains primary: rejected because the planning and governance
    surface would stay fragmented.
  - Deep editor embedding in phase 1: rejected because it adds unnecessary
    integration complexity before the operating model is proven.
