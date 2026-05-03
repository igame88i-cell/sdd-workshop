# Research: CLI ToDo 앱 구현 기술 선택

## Decision: Python 3.12
- 요청된 언어가 Python 3.12이므로 본 계획은 Python 3.12 기반으로 작성합니다.
- Python 3.12은 최신 타입 지원과 안정적인 CLI/데이터 라이브러리를 제공합니다.

## Decision: Typer for CLI
- `typer`는 명령행 서브커맨드, 자동 `--help`, 입력 검증, 자연스러운 CLI 사용 경험을 제공합니다.
- `todo add`, `todo list`, `todo done`, `todo delete` 명령어를 명확히 표현하기에 적합합니다.
- 대안: `argparse` 또는 `click`이 있으나, 요구된 최소 의존성 목록에 `typer`가 포함되어 있으므로 우선 사용합니다.

## Decision: SQLAlchemy for SQLite persistence
- `sqlalchemy`는 로컬 SQLite 파일을 안정적으로 관리하며, 명확한 모델 정의와 쿼리 기능을 제공합니다.
- 단일 사용자 로컬 앱이라도 ORM 기반 구현은 데이터 무결성과 유지보수성 측면에서 유리합니다.
- 대안: 표준 `sqlite3`만 사용하면 의존성을 줄일 수 있으나, 요청 사항과 업데이트 유연성을 감안하여 SQLAlchemy를 선택했습니다.

## Decision: pytest + pytest-cov for testing
- `pytest`는 테스트 우선 개발에 적합하며 명확한 실패 메시지와 확장성을 제공합니다.
- `pytest-cov`는 코드 커버리지 측정으로 요구된 성공 기준과 테스트 품질을 검증하는 데 필요합니다.

## Decision: uv for package management
- `uv`는 요청된 패키지 관리 도구로, 개발용 종속성 설치와 실행 환경을 일관되게 유지합니다.
- 로컬 개발 시 `uv run`을 통해 테스트와 CLI 실행을 단순화할 수 있습니다.

## Alternatives Considered
- JSON 파일 기반 저장: 구현이 더 단순하지만 SQLAlchemy 요구를 충족하지 못합니다.
- REST/GU I: 범위를 벗어나므로 고려 대상에서 제외됩니다.
- 추상 저장소 인터페이스: 단순함 원칙과 실제 요구를 고려할 때 불필요한 과설계입니다.
