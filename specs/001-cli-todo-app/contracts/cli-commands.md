# CLI Contracts: todo 명령어 정의

## 명령어 인터페이스

### `todo add "<제목>" [--due YYYY-MM-DD] [--priority high|medium|low]`
- 기능: 새 ToDo 항목을 추가합니다.
- `title`: 필수, 공백만 허용되지 않음
- `--due`: 선택적 마감일
- `--priority`: 선택적 우선순위, 기본값 `medium`
- 성공 메시지: `항목이 추가되었습니다 (ID: {id})`
- 실패 메시지:
  - `제목은 필수 입력 항목입니다`
  - `유효한 날짜 형식이 아닙니다: YYYY-MM-DD`
  - `우선순위는 high, medium, low 중 하나여야 합니다`

### `todo list [--filter done|pending] [--priority high|medium|low]`
- 기능: 저장된 항목 목록을 조회합니다.
- `--filter`: `done` 또는 `pending`으로 상태 필터링
- `--priority`: 특정 우선순위만 표시
- 출력 형식: `ID | 제목 | 마감일 | 우선순위 | 완료 여부`
- 예: `1 | Buy milk | 2026-05-10 | high | pending`
- 빈 목록 출력: `등록된 항목이 없습니다`

### `todo done <id>`
- 기능: 지정한 ID 항목을 완료 상태로 변경합니다.
- 성공 메시지: `항목 {id}가 완료 처리되었습니다`
- 오류 메시지:
  - `항목 {id}를 찾을 수 없습니다`
  - `항목 {id}는 이미 완료된 항목입니다`

### `todo delete <id>`
- 기능: 지정한 ID 항목을 삭제합니다.
- 성공 메시지: `항목 {id}가 삭제되었습니다`
- 오류 메시지: `항목 {id}를 찾을 수 없습니다`

## 공통 제약
- 모든 명령이 정상 종료 시 `exit code 0`을 반환합니다.
- 검증 실패 또는 존재하지 않는 ID 처리 시 `exit code 1`을 반환합니다.
- `todo --help` 또는 `todo <command> --help`는 Typer의 자동 도움말을 출력합니다.
