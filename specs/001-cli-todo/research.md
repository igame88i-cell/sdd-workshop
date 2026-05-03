# Research: CLI Todo Management App

## Decision: Use Python standard library only

- Chosen because the feature must minimize external dependencies and run in a terminal-only environment.
- Python 3.8+ provides built-in `argparse`, `json`, and `unittest`, which are sufficient for CLI parsing, persistence, and tests.
- Alternatives considered:
  - `click` or `typer`: simpler CLI code but adds external dependencies that violate the minimal-dependency requirement.
  - YAML or SQLite persistence: more complex than needed for a small local todo list.

## Decision: Local JSON file persistence

- Chosen because it is easy to implement, human-readable, and avoids database dependencies.
- The persistence layer will store tasks in a local `tasks.json` file in the working directory.
- Alternatives considered:
  - plain text or CSV: less structured and harder to validate reliably.
  - SQLite: more robust but unnecessarily complex for the first version.

## Decision: `unittest` for tests

- Chosen to avoid test framework dependencies while still enabling automated verification.
- This supports the constitution principle of test-first development without external packages.
- Alternatives considered:
  - `pytest`: more ergonomic, but adds a dependency.
  - manual script-based assertions: not as maintainable or standard.

## Decision: Monotonic task IDs

- Task IDs will increase monotonically and never be reused after deletion.
- This avoids ambiguous IDs and simplifies persistence and history reasoning.
- Alternatives considered:
  - reuse deleted IDs: saves ID space but can confuse users and complicate the task store.
  - UUIDs: overkill for a simple CLI todo list.

## Decision: Separate business logic from CLI

- Business logic will live in service and persistence modules.
- The CLI module will only parse input, validate arguments, and delegate operations.
- This supports easier unit testing and keeps the app aligned with the constitution.
