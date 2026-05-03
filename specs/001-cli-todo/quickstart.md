# Quickstart: CLI Todo Management App

## Prerequisites

- Python 3.8 or newer installed on the local machine.
- Terminal access on Windows, macOS, or Linux.
- The repository checked out locally.

## Run the App

From the repository root:

```powershell
python todo.py add "Buy groceries"
python todo.py list
python todo.py complete 1
python todo.py delete 1
python todo.py help
```

If the application is implemented as a package entrypoint, the equivalent commands may be:

```powershell
python -m todo add "Buy groceries"
python -m todo list
```

## Expected Behavior

- `add`: creates a new task and prints a confirmation with the task ID.
- `list`: displays the list of tasks with ID, description, and status.
- `complete`: marks the referenced task as completed.
- `delete`: removes the referenced task from persistent storage.
- `help`: shows available commands and usage examples.

## Persistence

- Tasks are stored in a local `tasks.json` file in the working directory.
- The file is loaded every time the app starts, and changes are written back after each command.

## Error Handling

- Empty descriptions are rejected with a clear error.
- Invalid task IDs produce a user-friendly error and do not change existing data.
- Unknown commands show help guidance rather than failing silently.
