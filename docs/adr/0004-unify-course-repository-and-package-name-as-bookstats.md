---
status: accepted
date: 2026-09-14
authors:
  - Igors Dubanevics
  - Antigravity
supersedes: "Repository naming in ADR 0001"
---

# Unify course repository and package name as bookstats

The course project repository and its reusable Python package are both named
`bookstats`. This supersedes the earlier naming decision in ADR 0001, which
named the repository `gutenberg-analysis` while naming the internal package
`bookstats`.

## Context

In ADR 0001, the repository was named `gutenberg-analysis` to reflect the raw
Project Gutenberg input data, while the Python package under `src/` was named
`bookstats`.

In practice, this split introduced unnecessary friction across the cumulative
curriculum:
1. When running `uv init --bare` inside an existing repository, `uv` adopts the
   enclosing directory name as the default project distribution name in
   `pyproject.toml` (`name = "gutenberg-analysis"`), causing a mismatch with the
   internal import package `src/bookstats/`.
2. Downstream sessions (Code Quality and Automation) naturally referred to the
   project as `bookstats` (e.g., in the `Makefile`, test suites, and GitHub Actions
   workflows).
3. The canonical reference repository and its milestone tags are published under
   the repository name `bookstats`.

## Decision

1. **Unify under `bookstats`**:
   - The learner's course repository created in Session 1 is named `bookstats`.
   - The GitHub remote repository is `<user>/bookstats`.
   - The collaborator's fork is `bookstats-<collaborator-a>`.
   - The Python distribution package and manifest in `pyproject.toml` is `name = "bookstats"`.
   - The source layout module is `src/bookstats/`.
2. **Pedagogical continuity**:
   - Learners begin in Session 1 with an empty folder named `bookstats`.
   - Session 2 initializes the environment directly within `bookstats`, producing
     a matching and consistent `pyproject.toml` without manual renaming steps.
   - The term `gutenberg-analysis` is retired and listed under `_Avoid_` in the project glossary.

## Consequences

- Zero renaming or namespace friction when learners progress from Session 1 to Session 2.
- `uv init --bare` produces `name = "bookstats"` automatically.
- Perfect consistency with the canonical reference repository (`https://github.com/oist/bookstats`).
