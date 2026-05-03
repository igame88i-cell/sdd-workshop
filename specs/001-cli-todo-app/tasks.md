# Tasks: CLI 기반 ToDo 관리 앱

**Input**: Design documents from `/specs/001-cli-todo-app/`
**Prerequisites**: `spec.md`, `plan.md`

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Create the base project structure and initialize required test and CLI entrypoint files.

- [ ] T001 [P] Create source directories `src/cli/`, `src/todo_lib/`, and `src/infrastructure/`
- [ ] T002 [P] Create test directories `tests/unit/` and `tests/integration/`
- [ ] T003 [P] Create `src/cli/__init__.py`
- [ ] T004 [P] Create `src/cli/main.py`
- [ ] T005 [P] Create `src/todo_lib/__init__.py`
- [ ] T006 [P] Create `src/todo_lib/models.py`
- [ ] T007 [P] Create `src/todo_lib/persistence.py`
- [ ] T008 [P] Create `src/todo_lib/service.py`
- [ ] T009 [P] Create `src/todo_lib/validation.py`
- [ ] T010 [P] Create `src/infrastructure/config.py`
- [ ] T011 [P] Create `tests/unit/__init__.py`
- [ ] T012 [P] Create `tests/unit/test_service.py`
- [ ] T013 [P] Create `tests/unit/test_cli.py`
- [ ] T014 [P] Create `tests/unit/test_validation.py`
- [ ] T015 [P] Create `tests/integration/test_cli_end_to_end.py`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Implement the core persistence, domain model, service layer, and CLI dispatch that all stories depend on.

- [ ] T016 [P] Define `ToDoItem` model in `src/todo_lib/models.py` with fields `id`, `title`, `due_date`, `priority`, `is_done`, and `created_at`
- [ ] T017 [P] Implement SQLite engine and session setup in `src/todo_lib/persistence.py`
- [ ] T018 [P] Implement database table creation in `src/todo_lib/persistence.py`
- [ ] T019 [P] Implement `add_todo`, `list_todos`, `mark_done`, and `delete_todo` methods in `src/todo_lib/service.py`
- [ ] T020 [P] Implement validation utilities in `src/todo_lib/validation.py` for title, due date format, priority, and ID inputs
- [ ] T021 [P] Implement the Typer app skeleton and command registration in `src/cli/main.py`
- [ ] T022 [P] Implement configuration loading for the SQLite file path in `src/infrastructure/config.py`
- [ ] T023 [P] Add persistence unit tests for database initialization and recovery in `tests/unit/test_service.py`
- [ ] T024 [P] Add model unit tests for field defaults and type constraints in `tests/unit/test_validation.py`
- [ ] T025 [P] Add CLI dispatch tests for command registration and invalid command handling in `tests/unit/test_cli.py`

---

## Phase 3: User Story 1 - ToDo 항목 추가 (Priority: P1)

**Goal**: Add new ToDo 항목 via CLI with title, optional due date, and optional priority, then persist it.

**Independent Test**: Run `uv run python -m cli add "할 일 제목" --due 2026-05-10 --priority high` and verify the new item is stored in SQLite with correct fields.

- [ ] T026 [US1] Write unit tests for `todo_lib.service.add_todo()` in `tests/unit/test_service.py`
- [ ] T027 [US1] Write CLI tests for successful `add` and missing-title error in `tests/unit/test_cli.py`
- [ ] T028 [US1] Implement `todo_lib.service.add_todo(title, due_date=None, priority='medium')` in `src/todo_lib/service.py`
- [ ] T029 [US1] Enforce non-empty title validation in `src/todo_lib/validation.py`
- [ ] T030 [US1] Enforce due date format validation in `src/todo_lib/validation.py`
- [ ] T031 [US1] Enforce priority normalization to `high`, `medium`, `low` in `src/todo_lib/validation.py`
- [ ] T032 [US1] Implement `add` command in `src/cli/main.py` and show `항목이 추가되었습니다 (ID: {id})`
- [ ] T033 [US1] Persist new task to SQLite using `src/todo_lib/persistence.py`

---

## Phase 4: User Story 2 - 전체 목록 조회 및 필터링 (Priority: P2)

**Goal**: List saved ToDo 항목 and filter them by completion 상태 or priority.

**Independent Test**: Run `uv run python -m cli list`, `uv run python -m cli list --filter pending`, and `uv run python -m cli list --priority high`, verifying output reflects the stored records.

- [ ] T034 [US2] Write unit tests for `todo_lib.service.list_todos()` and filter logic in `tests/unit/test_service.py`
- [ ] T035 [US2] Write CLI tests for `list`, `list --filter pending`, `list --filter done`, and `list --priority high` in `tests/unit/test_cli.py`
- [ ] T036 [US2] Implement `todo_lib.service.list_todos(status=None, priority=None)` in `src/todo_lib/service.py`
- [ ] T037 [US2] Implement `list` command options in `src/cli/main.py`
- [ ] T038 [US2] Implement formatted task output with `ID | 제목 | 마감일 | 우선순위 | 완료 여부` in `src/cli/main.py`
- [ ] T039 [US2] Implement empty list handling with `등록된 항목이 없습니다` output in `src/cli/main.py`

---

## Phase 5: User Story 3 - 항목 완료 처리 (Priority: P3)

**Goal**: Mark a task as completed by ID and provide a clear confirmation message.

**Independent Test**: Add a pending task, run `uv run python -m cli complete 1`, and verify the task becomes completed in the database.

- [ ] T040 [US3] Write unit tests for `todo_lib.service.mark_done(task_id)` in `tests/unit/test_service.py`
- [ ] T041 [US3] Write CLI tests for `complete` success, already completed, and invalid ID cases in `tests/unit/test_cli.py`
- [ ] T042 [US3] Implement `todo_lib.service.mark_done(task_id)` in `src/todo_lib/service.py`
- [ ] T043 [US3] Implement `complete` command in `src/cli/main.py`
- [ ] T044 [US3] Implement user-facing messages for success, already completed, and missing ID in `src/cli/main.py`

---

## Phase 6: User Story 4 - 항목 삭제 (Priority: P4)

**Goal**: Delete a task by ID permanently with error handling for missing tasks.

**Independent Test**: Add a task, run `uv run python -m cli delete 1`, and confirm it no longer appears in `uv run python -m cli list`.

- [ ] T045 [US4] Write unit tests for `todo_lib.service.delete_todo(task_id)` in `tests/unit/test_service.py`
- [ ] T046 [US4] Write CLI tests for `delete` success and invalid ID error in `tests/unit/test_cli.py`
- [ ] T047 [US4] Implement `todo_lib.service.delete_todo(task_id)` in `src/todo_lib/service.py`
- [ ] T048 [US4] Implement `delete` command in `src/cli/main.py`
- [ ] T049 [US4] Implement confirmation and invalid ID error output in `src/cli/main.py`

---

## Phase 7: Help and Error Guidance (Priority: P5)

**Goal**: Provide help text and graceful guidance for unknown commands.

**Independent Test**: Run `uv run python -m cli --help` and `uv run python -m cli help` and verify command usage is shown.

- [ ] T050 [US5] Write CLI tests for `--help`, `help`, and unknown command fallback in `tests/unit/test_cli.py`
- [ ] T051 [US5] Implement `help` and fallback guidance in `src/cli/main.py`
- [ ] T052 [US5] Ensure `typer` help text includes `add`, `list`, `complete`, and `delete` commands

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Strengthen validation, error recovery, documentation, and maintainability across all stories.

- [ ] T053 [P] Add whitespace-only title rejection in `src/todo_lib/validation.py`
- [ ] T054 [P] Enforce `YYYY-MM-DD` due date validation in `src/todo_lib/validation.py`
- [ ] T055 [P] Enforce priority values only `high`, `medium`, `low` in `src/todo_lib/validation.py`
- [ ] T056 [P] Add persistence corruption recovery and database migration readiness in `src/todo_lib/persistence.py`
- [ ] T057 [P] Add invalid input and error scenario tests in `tests/unit/test_validation.py`
- [ ] T058 [P] Add CLI error handling tests for invalid date, invalid priority, and invalid ID in `tests/unit/test_cli.py`
- [ ] T059 [P] Review `specs/001-cli-todo-app/plan.md`, `specs/001-cli-todo-app/spec.md`, and `specs/001-cli-todo-app/contracts/cli-commands.md` for confirmed command syntax, then update if needed
- [ ] T062 [P] Add performance validation tasks for SC-005, including `list` and `done` operation behavior with 1,000+ stored items
- [ ] T063 [P] Add concurrency/storage edge case guidance tasks for file corruption or simultaneous access scenarios in `src/todo_lib/persistence.py`
- [ ] T060 [P] Refactor `src/todo_lib/` modules to improve separation of concerns while preserving tests
- [ ] T061 [P] Refactor test suites for readability and coverage in `tests/unit/` and `tests/integration/`

---

## Dependencies & Execution Order

- **Phase 1**: Setup tasks can begin immediately and are parallelizable.
- **Phase 2**: Foundational tasks must complete before implementing user stories.
- **Phase 3+**: User story tasks depend on the foundational layer and can be implemented independently afterward.
- **Phase 8**: Polish depends on completion of the user story phases.

### Parallel Opportunities
- `T001` through `T015` can run in parallel because they create separate scaffolding files.
- `T016` through `T025` can mostly run in parallel across model, persistence, service, validation, and CLI setup.
- User story phases can proceed in parallel after foundational work is complete.
