# Data Model: ToDo 엔티티

## ToDoItem

**Entity**: ToDoItem

- `id`: 정수, 자동 증가, 기본 키
- `title`: 문자열, 필수, 공백만 허용하지 않음
- `due_date`: 날짜, 선택적, `YYYY-MM-DD` 형식
- `priority`: 문자열, 선택적, `high`, `medium`, `low` 중 하나, 기본값 `medium`
- `is_done`: 불린, 기본값 `False`
- `created_at`: 타임스탬프, 항목 생성 시 자동 설정

## Validation Rules

- `title`은 빈 문자열 또는 공백만인 경우 추가를 거부합니다.
- `due_date`는 `YYYY-MM-DD` 형식이어야 하며, 유효하지 않으면 오류가 발생합니다.
- `priority`는 `high`, `medium`, `low` 세 단계만 허용합니다.
- `done` 및 `delete` 명령의 `id` 값은 정수여야 하며, 존재하지 않을 경우 명확한 오류 메시지를 반환합니다.

## Storage Schema

SQLite 테이블 구조 예시:

- `todos`
  - `id INTEGER PRIMARY KEY AUTOINCREMENT`
  - `title TEXT NOT NULL`
  - `due_date DATE NULL`
  - `priority TEXT NOT NULL DEFAULT 'medium'`
  - `is_done BOOLEAN NOT NULL DEFAULT 0`
  - `created_at DATETIME NOT NULL`

## Layer Separation

- `todo_lib/models.py`: SQLAlchemy 모델과 도메인 엔티티 정의
- `todo_lib/persistence.py`: SQLite 세션 생성, DB 연결, 테이블 생성
- `todo_lib/service.py`: `add_todo`, `list_todos`, `mark_todo_done`, `delete_todo` 등 비즈니스 로직
- `todo_lib/validation.py`: 제목, 날짜, 우선순위 입력 검증

## State Transitions

- 생성: `is_done=False`로 초기화되어 pending 상태
- 완료: `mark_todo_done(id)` 호출 시 `is_done=True`로 변경
- 삭제: `delete_todo(id)` 호출 시 DB에서 항목 제거
- 조회: `list_todos(filter, priority)`는 완료/미완료 및 우선순위 필터를 적용하여 결과를 반환
