# Tasks: CLI 기반 ToDo 관리 앱

**Input**: Design documents from `/specs/001-cli-todo-app/`
**Prerequisites**: `spec.md`, `plan.md`

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Create the base Python CLI project structure and initialize core files.

- [ ] T001 [P] Create source directory `src/todo/`
- [ ] T002 [P] Create tests directory `tests/unit/`
- [ ] T003 [P] Create entrypoint file `todo.py`
- [ ] T004 [P] Create CLI adapter skeleton in `src/todo/cli.py`
- [ ] T005 [P] Create model module skeleton in `src/todo/models.py`
- [ ] T006 [P] Create persistence module skeleton in `src/todo/persistence.py`
- [ ] T007 [P] Create service module skeleton in `src/todo/service.py`
- [ ] T008 [P] Create test initializer file `tests/unit/__init__.py`
- [ ] T009 [P] Create unit test file skeleton `tests/unit/test_models.py`
- [ ] T010 [P] Create unit test file skeleton `tests/unit/test_persistence.py`
- [ ] T011 [P] Create unit test file skeleton `tests/unit/test_service.py`
- [ ] T012 [P] Create CLI test file skeleton `tests/unit/test_cli.py`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Implement the core domain model, persistence, and CLI dispatch that all user stories depend on.

- [ ] T013 [P] Define `ToDo` model in `src/todo/models.py` with fields `id`, `title`, `due_date`, `priority`, `completed`, and `created_at`
- [ ] T014 [P] Implement `TaskStore` persistence in `src/todo/persistence.py` with JSON load/save and file creation
- [ ] T015 [P] Implement persistence recovery behavior in `src/todo/persistence.py` for missing or corrupted save files
- [ ] T016 [P] Implement `TaskService` interface in `src/todo/service.py` with `add_task`, `list_tasks`, `list_tasks(filter)`, `complete_task`, and `delete_task`
- [ ] T017 [P] Add validation helper methods for title, date format, priority, and ID in `src/todo/service.py`
- [ ] T018 [P] Implement basic CLI command dispatcher in `src/todo/cli.py` for `add`, `list`, `complete`, `delete`, and `help`
- [ ] T019 [P] Implement `todo.py` entrypoint to call `src/todo/cli.py` with command-line arguments
- [ ] T020 [P] Add persistence unit tests for load/save and recovery in `tests/unit/test_persistence.py`
- [ ] T021 [P] Add model unit tests for `ToDo` field mapping and serialization in `tests/unit/test_models.py`
- [ ] T022 [P] Add service scaffolding tests in `tests/unit/test_service.py` for method signatures and initial validation behavior
- [ ] T023 [P] Add CLI command dispatch tests in `tests/unit/test_cli.py` for command parsing and unknown command handling

---

## Phase 3: User Story 1 - ToDo 항목 추가 (Priority: P1)

**Goal**: Enable CLI-based ToDo 항목 추가 with title, optional due date, and optional priority, and persist it locally.

**Independent Test**: Run `python todo.py add "할 일 제목"` and verify the task is saved in the persistence file with correct fields.

- [ ] T024 [US1] Write unit tests for `TaskService.add_task()` in `tests/unit/test_service.py`
- [ ] T025 [US1] Write CLI tests for `add` command success and missing-title error in `tests/unit/test_cli.py`
- [ ] T026 [US1] Implement `TaskService.add_task(title, due_date=None, priority=None)` in `src/todo/service.py`
- [ ] T027 [US1] Implement title-required validation and empty-title rejection in `src/todo/service.py`
- [ ] T028 [US1] Implement due date format validation and priority normalization in `src/todo/service.py`
- [ ] T029 [US1] Implement `add` command handling in `src/todo/cli.py` and success message output
- [ ] T030 [US1] Persist new task to local file after add command in `src/todo/persistence.py`

---

## Phase 4: User Story 2 - 전체 목록 조회 및 필터링 (Priority: P2)

**Goal**: Enable users to list all ToDo 항목 and filter by completion or priority.

**Independent Test**: Run `python todo.py list` and `python todo.py list --status incomplete` / `python todo.py list --priority high` and verify output matches stored tasks.

- [ ] T031 [US2] Write unit tests for `TaskService.list_tasks()` and filtered list behaviors in `tests/unit/test_service.py`
- [ ] T032 [US2] Write CLI tests for `list`, `list --status`, and `list --priority` output in `tests/unit/test_cli.py`
- [ ] T033 [US2] Implement `TaskService.list_tasks(status=None, priority=None)` in `src/todo/service.py`
- [ ] T034 [US2] Implement `list` command options in `src/todo/cli.py` and formatted output display
- [ ] T035 [US2] Implement empty-list friendly message in `src/todo/cli.py`

---

## Phase 5: User Story 3 - 항목 완료 처리 (Priority: P3)

**Goal**: Enable marking a task as completed by ID with clear feedback.

**Independent Test**: Add an incomplete task, run `python todo.py complete 1`, and verify the task status updates to completed.

- [ ] T036 [US3] Write unit tests for `TaskService.complete_task(task_id)` in `tests/unit/test_service.py`
- [ ] T037 [US3] Write CLI tests for `complete` success, already completed, and invalid ID cases in `tests/unit/test_cli.py`
- [ ] T038 [US3] Implement `TaskService.complete_task(task_id)` in `src/todo/service.py`
- [ ] T039 [US3] Implement `complete` command handling in `src/todo/cli.py`
- [ ] T040 [US3] Add completed-already and invalid-ID user-facing messages in `src/todo/cli.py`

---

## Phase 6: User Story 4 - 항목 삭제 (Priority: P4)

**Goal**: Enable permanent deletion of a task by ID with error handling.

**Independent Test**: Add a task, run `python todo.py delete 1`, and verify it no longer appears in `todo list`.

- [ ] T041 [US4] Write unit tests for `TaskService.delete_task(task_id)` in `tests/unit/test_service.py`
- [ ] T042 [US4] Write CLI tests for `delete` success and invalid ID cases in `tests/unit/test_cli.py`
- [ ] T043 [US4] Implement `TaskService.delete_task(task_id)` in `src/todo/service.py`
- [ ] T044 [US4] Implement `delete` command handling in `src/todo/cli.py`
- [ ] T045 [US4] Add deletion confirmation and invalid ID error output in `src/todo/cli.py`

---

## Phase 7: User Story 5 - 도움말 표시 (Priority: P5)

**Goal**: Provide a help command describing available CLI usage and commands.

**Independent Test**: Run `python todo.py help` and verify help text lists `add`, `list`, `complete`, `delete`, and `help`.

- [ ] T046 [US5] Write CLI tests for `help` output and unknown command guidance in `tests/unit/test_cli.py`
- [ ] T047 [US5] Implement `help` output in `src/todo/cli.py`
- [ ] T048 [US5] Implement unknown command fallback to display help guidance in `src/todo/cli.py`

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Improve validation, error recovery, and documentation across the entire app.

- [ ] T049 [P] Add whitespace-only title rejection in `src/todo/service.py`
- [ ] T050 [P] Enforce `YYYY-MM-DD` due date format validation in `src/todo/service.py`
- [ ] T051 [P] Restrict priority values to `high`, `medium`, `low` in `src/todo/service.py`
- [ ] T052 [P] Add persistence file corruption handling in `src/todo/persistence.py`
- [ ] T053 [P] Add tests for invalid date, invalid priority, and invalid ID handling in `tests/unit/test_service.py`
- [ ] T054 [P] Add CLI tests for invalid input error messages in `tests/unit/test_cli.py`
- [ ] T055 [P] Update `specs/001-cli-todo-app/plan.md` and `specs/001-cli-todo-app/spec.md` with confirmed command syntax and behavior
- [ ] T056 [P] Review and refactor `src/todo/` modules for readability and separation of concerns
- [ ] T057 [P] Review and refactor `tests/unit/` for coverage and maintainability

---

## Dependencies & Execution Order

- **Phase 1**: Setup tasks can begin immediately and are parallelizable.
- **Phase 2**: Foundational tasks must complete before implementing user stories.
- **Phase 3+**: User story tasks depend on the foundational layer and can be implemented independently afterward.
- **Phase 8**: Polish depends on completion of the user story phases.

### Parallel Opportunities
- `T001` through `T012` can run in parallel because they create separate files and scaffolding.
- `T013` through `T023` can mostly run in parallel across model, persistence, service, and CLI modules.
- User story phases can proceed in parallel after foundational work is complete.
