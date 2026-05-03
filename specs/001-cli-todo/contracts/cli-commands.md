# CLI Command Contract: Todo Management App

## Command Overview

The app exposes a small and explicit CLI surface to keep the terminal workflow simple and discoverable.

### `todo add <description>`
- Purpose: create a new todo item.
- Input: non-empty text description enclosed in quotes if it contains spaces.
- Output: confirmation message with the newly assigned task ID.
- Error cases:
  - missing description
  - empty or whitespace-only description

### `todo list`
- Purpose: display all saved tasks.
- Input: no additional arguments.
- Output: list of tasks showing ID, description, and status.
- Behavior:
  - if no tasks exist, show a friendly empty-state message.

### `todo complete <task_id>`
- Purpose: mark an existing task as completed.
- Input: integer task ID.
- Output: confirmation message when the task is marked complete.
- Error cases:
  - invalid or missing task ID
  - task ID does not exist

### `todo delete <task_id>`
- Purpose: remove an existing task from the list.
- Input: integer task ID.
- Output: confirmation message when the task is deleted.
- Error cases:
  - invalid or missing task ID
  - task ID does not exist

### `todo help`
- Purpose: show available commands and usage examples.
- Input: no additional arguments.
- Output: help text describing `add`, `list`, `complete`, `delete`, and `help`.

## Execution Contract

- The CLI is responsible only for parsing arguments, validating user input, and displaying messages.
- No business logic should be implemented in the command parser itself.
- All core operations should delegate to the `TaskService` layer.

## Output Format

- Success messages should be short and explicit.
- Errors should be written clearly and indicate how to fix the input.
- The `list` command should present tasks in a readable table-like format or consistent bullet list.

## Persistence Contract

- Task state is persisted after modifying commands (`add`, `complete`, `delete`).
- Read-only commands (`list`, `help`) should not alter persistent state.
- The persistence layer must tolerate a missing `tasks.json` file by creating it on demand.
