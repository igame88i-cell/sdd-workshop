# Tasks: CLI Todo Management App

**Input**: Design documents from `/specs/001-cli-todo/`
**Prerequisites**: `plan.md`, `spec.md`, `data-model.md`, `contracts/`

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Initialize the Python CLI project structure and create the base source/test files.

- [ ] T001 [P] Create source directory `src/todo/`
- [ ] T002 [P] Create tests directory `tests/unit/`
- [ ] T003 [P] Create entrypoint file `todo.py`
- [ ] T004 [P] Create CLI module skeleton in `src/todo/cli.py`
- [ ] T005 [P] Create model module skeleton in `src/todo/models.py`
- [ ] T006 [P] Create persistence module skeleton in `src/todo/persistence.py`
- [ ] T007 [P] Create service module skeleton in `src/todo/service.py`
- [ ] T008 [P] Create test initializer file `tests/unit/__init__.py`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Implement core business entities, persistence, and service layer behavior that all user stories depend on.

- [ ] T009 [P] Define `Task` model in `src/todo/models.py` with `id`, `description`, `completed`, and optional `created_at`
- [ ] T010 [P] Implement `TaskStore` persistence in `src/todo/persistence.py` with load/save, missing file creation, and JSON file handling
- [ ] T011 [P] Implement `TaskService` behavior in `src/todo/service.py` with method signatures for `add_task`, `list_tasks`, `complete_task`, and `delete_task`
- [ ] T012 [P] Create model unit tests in `tests/unit/test_models.py`
- [ ] T013 [P] Create persistence unit tests in `tests/unit/test_persistence.py`
- [ ] T014 [P] Create service unit tests scaffold in `tests/unit/test_service.py`
- [ ] T015 [P] Implement basic CLI command dispatch in `src/todo/cli.py` using the command contract in `specs/001-cli-todo/contracts/cli-commands.md`

---

## Phase 3: User Story 1 - Add a Task (Priority: P1) 🎯 MVP

**Goal**: Enable users to add a new task with a description through the CLI and persist it locally.

**Independent Test**: Run `python todo.py add "Buy groceries"` and verify the task appears in `tasks.json` and the command returns a success confirmation.

### Tests for User Story 1

- [ ] T016 [US1] Write unit tests for `TaskService.add_task()` in `tests/unit/test_service.py`
- [ ] T017 [US1] Write a CLI test for the `add` command behavior in `tests/unit/test_cli.py`

### Implementation for User Story 1

- [ ] T018 [US1] Implement `TaskService.add_task(description)` in `src/todo/service.py`
- [ ] T019 [US1] Implement CLI handling for `add` in `src/todo/cli.py`
- [ ] T020 [US1] Wire `todo.py` to call `src/todo/cli.py` and print the add confirmation message
- [ ] T021 [US1] Ensure `add` persists the new task to `tasks.json` and returns the created task ID

---

## Phase 4: User Story 2 - List Tasks (Priority: P1)

**Goal**: Allow users to list all saved tasks with ID, description, and status from the terminal.

**Independent Test**: Run `python todo.py list` after adding tasks and verify the displayed output matches persisted tasks.

### Tests for User Story 2

- [ ] T022 [US2] Write unit tests for `TaskService.list_tasks()` in `tests/unit/test_service.py`
- [ ] T023 [US2] Write a CLI test for `list` output in `tests/unit/test_cli.py`

### Implementation for User Story 2

- [ ] T024 [US2] Implement `TaskService.list_tasks()` in `src/todo/service.py`
- [ ] T025 [US2] Implement CLI handling for `list` in `src/todo/cli.py`
- [ ] T026 [US2] Add friendly empty-list behavior to `list` output in `src/todo/cli.py`

---

## Phase 5: User Story 3 - Complete a Task (Priority: P2)

**Goal**: Enable users to mark a task as completed by its ID.

**Independent Test**: Add a task, run `python todo.py complete 1`, and verify the task status updates to completed in `tasks.json`.

### Tests for User Story 3

- [ ] T027 [US3] Write unit tests for `TaskService.complete_task(task_id)` in `tests/unit/test_service.py`
- [ ] T028 [US3] Write a CLI test for the `complete` command in `tests/unit/test_cli.py`

### Implementation for User Story 3

- [ ] T029 [US3] Implement `TaskService.complete_task(task_id)` in `src/todo/service.py`
- [ ] T030 [US3] Implement CLI handling for `complete` in `src/todo/cli.py`
- [ ] T031 [US3] Add a confirmation message when a task is successfully completed

---

## Phase 6: User Story 4 - Delete a Task (Priority: P2)

**Goal**: Enable users to delete a task by its ID.

**Independent Test**: Add a task, run `python todo.py delete 1`, and verify the task is removed from `tasks.json`.

### Tests for User Story 4

- [ ] T032 [US4] Write unit tests for `TaskService.delete_task(task_id)` in `tests/unit/test_service.py`
- [ ] T033 [US4] Write a CLI test for the `delete` command in `tests/unit/test_cli.py`

### Implementation for User Story 4

- [ ] T034 [US4] Implement `TaskService.delete_task(task_id)` in `src/todo/service.py`
- [ ] T035 [US4] Implement CLI handling for `delete` in `src/todo/cli.py`
- [ ] T036 [US4] Add a confirmation message when a task is successfully deleted

---

## Phase 7: User Story 5 - Display Help (Priority: P3)

**Goal**: Provide a help command that lists available CLI commands and usage examples.

**Independent Test**: Run `python todo.py help` and verify that add, list, complete, delete, and help usage is shown.

### Tests for User Story 5

- [ ] T037 [US5] Write unit tests for help output in `tests/unit/test_cli.py`
- [ ] T038 [US5] Write a CLI test for unknown command guidance in `tests/unit/test_cli.py`

### Implementation for User Story 5

- [ ] T039 [US5] Implement `help` command output in `src/todo/cli.py`
- [ ] T040 [US5] Implement unknown command handling in `src/todo/cli.py` to display help guidance

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Add validation, error handling, persistence recovery, and polish across all stories.

- [ ] T041 [P] Add empty or whitespace-only description validation in `src/todo/service.py`
- [ ] T042 [P] Add invalid task ID error handling in `src/todo/service.py`
- [ ] T043 [P] Add persistence file corruption recovery and missing file handling in `src/todo/persistence.py`
- [ ] T044 [P] Add unit tests for persistence recovery scenarios in `tests/unit/test_persistence.py`
- [ ] T045 [P] Add CLI error message tests for invalid input in `tests/unit/test_cli.py`
- [ ] T046 [P] Update `specs/001-cli-todo/quickstart.md` with confirmed implementation command examples
- [ ] T047 [P] Review and refactor `src/todo/` and `tests/unit/` for clarity and maintainability

---

## Dependencies & Execution Order

### Phase Dependencies
- **Phase 1**: Setup tasks can begin immediately and are parallelizable.
- **Phase 2**: Foundational work must complete before user story implementation begins.
- **Phase 3+**: User stories depend on the foundational phase but can be implemented independently afterward.
- **Phase 8**: Polish depends on user story completion and production readiness.

### User Story Dependencies
- **US1**: independent after foundational phase.
- **US2**: independent after foundational phase.
- **US3**: independent after foundational phase.
- **US4**: independent after foundational phase.
- **US5**: independent after foundational phase.

### Parallel Opportunities
- Setup tasks `T001` through `T008` can run in parallel.
- Foundational tasks `T009` through `T015` can run in parallel as long as files are separate.
- Test creation tasks can run in parallel with implementation work in separate modules where dependencies allow.
- Different user stories can be worked on in parallel after the foundational layer is complete.

---

## Implementation Strategy

### MVP Scope
- Complete Phase 1 and Phase 2.
- Deliver User Story 1 (`add`) as the first functional increment.
- Validate `add` independently with unit and CLI tests before continuing.

### Incremental Delivery
1. Finish setup and foundational layers.
2. Implement and verify `add` command.
3. Implement `list` command.
4. Implement `complete` command.
5. Implement `delete` command.
6. Add `help` support and polish validation.

### Testing Strategy
- Write unit tests for each service method before implementing it.
- Add CLI tests for each user story command.
- Ensure persistence and error behaviors are covered as part of polish.
