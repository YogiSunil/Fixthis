# Fixthis - SuiteCRM Track

This workspace is separate from firstbuild and is dedicated to the SuiteCRM option.

## Chosen Project

- Project: SuiteCRM 7
- Goal: Add a custom dashboard widget (dashlet)
- Upstream cloned at: `Fixthis/SuiteCRM`

## Assignment Structure

fixthis/
- README.md
- CLAUDE.md
- AGENTS.md
- writeup.md
- src/AGENTS.md
- SuiteCRM/

## Setup Used

1. Clone SuiteCRM into this workspace.
2. Explore architecture and conventions before coding.
3. Define scoped rules and feature acceptance criteria.

Command used:

- `git clone https://github.com/salesagility/SuiteCRM.git`

## Progress Checklist

### V1.0 - Exploration and Understanding

- [x] Map architecture with AI exploration and save notes in writeup.md
- [x] Create project-specific CLAUDE.md with real stack and paths
- [x] Add scoped AGENTS.md in a key subdirectory (`SuiteCRM/modules/`)
- [x] Commit and push

### V1.1 - Rules and Context Tuning

- [x] Add at least 3 scoped rules based on SuiteCRM conventions
- [x] Run a small implementation prompt to validate agent behavior
- [x] Refine rules and document before/after in writeup.md
- [x] Commit and push

### V1.2 - Feature Addition

- [x] Draft feature specification with acceptance criteria in writeup.md
- [x] Add failing tests first
- [x] Implement to green
- [x] Verify no regressions in existing test suites
- [x] Commit and push

## Current Feature Target

Build a new custom dashlet using existing SuiteCRM dashlet conventions:

- Dashlet class pattern from `modules/*/Dashlets/*/*.php`
- Dashlet metadata in `*.meta.php`
- Dashlet configuration/data in `*.data.php`
- Prefer customization-safe location under `custom/modules/.../Dashlets/...`

## Definition of Done

- Required docs are project-specific and accurate to SuiteCRM.
- Rules are path-scoped and tested against a small coding task.
- New feature has failing-then-passing tests/evidence.
- Existing tests (or selected baseline suite) still pass.
- writeup.md documents exploration, tuning, and results.
