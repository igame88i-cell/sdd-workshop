# Data Model: CLI Todo Management App

## Entities

### Task
- `id` (integer): unique, monotonic identifier assigned when the task is created.
- `description` (string): the text description of the todo item.
- `completed` (boolean): true when the task has been marked complete.
- `created_at` (string, optional): ISO-8601 timestamp for when the task was created.

### TaskStore
- Responsible for loading and saving the task collection.
- File-based persistence using a local JSON file, e.g. `tasks.json`.
- Validation rules:
  - Task IDs must remain unique within the file.
  - The file may be recreated if missing or corrupted.

### TaskService
- Encapsulates business operations on `Task` objects.
- Core operations:
  - `add_task(description)`
  - `list_tasks()`
  - `complete_task(task_id)`
  - `delete_task(task_id)`
- Validation:
  - reject empty or whitespace-only descriptions
  - reject invalid task IDs that do not exist
  - preserve existing tasks when completion or deletion fails

## Relationships

- `TaskService` depends on `TaskStore` for persistence.
- `TaskStore` manages a collection of `Task` objects and exposes load/save operations.
- `cli.py` depends on `TaskService` to execute user commands.

## Behavior rules

- Adding a task assigns the next available monotonic ID.
- Listing tasks returns the full current collection with status labels.
- Completing a task updates its `completed` flag.
- Deleting a task removes it from the collection but does not reuse its ID.
- An empty task list produces a friendly message, not an error.
