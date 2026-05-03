# Quickstart: CLI ToDo 앱 실행

## 사전 준비

1. Python 3.12 설치
2. `uv` 설치 또는 사용 가능한 상태 확인

## 의존성 설치

```powershell
uv install typer sqlalchemy pytest pytest-cov
```

## 개발 실행

```powershell
uv run python -m cli add "Buy milk" --due 2026-05-10 --priority high
uv run python -m cli list
uv run python -m cli list --filter pending --priority high
uv run python -m cli done 1
uv run python -m cli delete 1
```

## 테스트 실행

```powershell
uv run pytest --cov=todo_lib tests/
```

## 데이터 저장 위치

- 기본 SQLite 파일: `todo.db`
- `todo.db`는 프로젝트 루트 또는 환경 설정에서 지정한 경로에 생성됩니다.
