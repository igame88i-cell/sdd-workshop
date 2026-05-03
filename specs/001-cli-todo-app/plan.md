# Implementation Plan: CLI 기반 ToDo 앱

**Branch**: `001-cli-todo-app` | **Date**: 2026-05-03 | **Spec**: `specs/001-cli-todo-app/spec.md`
**Input**: Feature specification from `specs/001-cli-todo-app/spec.md`

## Summary

Python 3.12 기반 로컬 SQLite ToDo CLI 애플리케이션을 구현합니다. 명령행에서 `add`, `list`, `done`, `delete` 서브커맨드를 제공하며, 비즈니스 로직은 `todo_lib/` 내부에 분리하고 CLI는 입력/출력과 명령 매핑에 집중합니다.

## Technical Context

**Language/Version**: Python 3.12  
**Primary Dependencies**: `typer`, `sqlalchemy`  
**Storage**: SQLite 파일 기반 저장소 (`todo.db`) via SQLAlchemy  
**Testing**: `pytest`, `pytest-cov`  
**Target Platform**: Windows PowerShell/CMD, macOS/Linux shell  
**Project Type**: CLI application with independent business logic library  
**Performance Goals**: 1,000개 이상의 항목을 저장했을 때도 목록 조회 및 상태 변경 명령이 체감상 즉각적으로 실행되어야 함  
**Constraints**: GUI/REST API는 범위 밖, 로컬 단일 사용자 CLI 도구, 필요 없는 의존성은 도입하지 않음  

## Why SQLAlchemy?

`SQLAlchemy`는 SQLite와의 안전한 데이터 매핑, 스키마 정의, 트랜잭션 관리, 확장성을 제공합니다. 로컬 DB를 직접 조작하는 대신 명확한 모델과 ORM 계층을 두어 코드 품질과 테스트 용이성을 높이기 위해 선택했습니다. 또한 향후 저장소 구조가 변경되더라도 비즈니스 로직 레이어의 수정 범위를 줄일 수 있습니다.

## Constitution Check

- [x] 레이어 분리: `cli/`는 입력/출력과 명령 라인 처리에 집중하고, `todo_lib/`는 도메인 로직과 영속성을 관리합니다.
- [x] 테스트 우선: `tests/` 폴더에 단위 테스트와 통합 테스트를 포함하며 구현 전에 테스트를 작성하도록 계획합니다.
- [x] 최소 의존성: `typer`, `sqlalchemy`, `pytest`만 도입하며 불필요한 패키지는 추가하지 않습니다.
- [x] 단순함 우선: 추가/조회/완료/삭제 기능에 집중하며 과도한 추상화는 피합니다.
- [x] CLI 범위: 전체 워크플로우는 명령행과 표준 입출력으로 제한됩니다.

## Project Structure

### Documentation (feature artifacts)

```text
specs/001-cli-todo-app/
  plan.md
  research.md
  data-model.md
  quickstart.md
  contracts/
    cli-commands.md
  tasks.md
```

### Source Code Layout

```text
src/
  cli/
    __init__.py
    main.py
  todo_lib/
    __init__.py
    models.py
    persistence.py
    service.py
    validation.py
  infrastructure/
    config.py

tests/
  unit/
    test_service.py
    test_cli.py
    test_validation.py
  integration/
    test_cli_end_to_end.py
```

## Key Design Decisions

- `cli/`는 `typer` 기반 서브커맨드 등록과 사용자 메시지 출력에 전념합니다.
- `todo_lib/`는 도메인 모델, 영속성, 서비스, 입력 검증을 분리해 책임을 격리합니다.
- `infrastructure/config.py`는 SQLite 파일 경로와 환경 구성을 중앙 관리합니다.
- CLI 계약은 `specs/001-cli-todo-app/contracts/cli-commands.md`에 명세하고 구현과 문서를 동기화합니다.

## Phase Summary

- Phase 1: 베이스 디렉터리/파일 구조 생성
- Phase 2: 모델/영속성/서비스/CLI 뼈대 구현
- Phase 3: `add` 기능 구현 및 테스트
- Phase 4: `list` 기능과 필터링 구현 및 테스트
- Phase 5: `done` 기능 구현 및 테스트
- Phase 6: `delete` 기능 구현 및 테스트
- Phase 7: 도움말/오류 안내 및 CLI 완성도 강화
- Phase 8: 검증, 성능, 문서, 유지 보수 개선

## Notes

- `SQLAlchemy`는 현재 로컬 SQLite와 함께 쓰이며, 필요 시 동일 서비스/모델 코드로 다른 DB로 확장할 수 있도록 합니다.
- `todo add ...`, `todo list ...`, `todo done ...`, `todo delete ...` 형식의 CLI 계약을 명세와 구현 양쪽에서 일치시키는 것이 중요합니다.
