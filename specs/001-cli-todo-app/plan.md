# Implementation Plan: CLI 기반 ToDo 관리 앱

**Branch**: `001-cli-todo-app` | **Date**: 2026-05-03 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-cli-todo-app/spec.md`

**Note**: 이 계획서는 명령행 기반 ToDo 관리 앱의 명확한 구현 경로를 제공합니다.

## Summary

터미널에서 실행하는 Python 기반 CLI ToDo 앱을 구현합니다. 이 앱은 제목을 필수로 받고, 선택적으로 마감일과 우선순위를 지정할 수 있습니다. 사용자는 항목 추가, 전체/필터 조회, 완료 처리, 삭제를 명령행으로 수행할 수 있으며, 모든 데이터는 로컬 파일에 영구 저장됩니다.

## Technical Context

**Language/Version**: Python 3.8+  
**Primary Dependencies**: 표준 라이브러리만 사용 (외부 패키지 불필요)  
**Storage**: 로컬 파일 기반 영구 저장, JSON 또는 간단한 구조화된 파일  
**Testing**: `unittest` 표준 라이브러리  
**Target Platform**: 로컬 터미널 환경 (POSIX 쉘 또는 Windows PowerShell/CMD)  
**Project Type**: CLI 애플리케이션  
**Performance Goals**: 소규모 로컬 리스트에서 즉각적인 응답  
**Constraints**: CLI 전용, REST/GUI/웹 제외, 비즈니스 로직과 CLI 분리, 최소 의존성  
**Scale/Scope**: 단일 사용자 로컬 ToDo 관리, 수백~천 개 수준의 항목 지원

## Constitution Check

- `CA-001` 레이어 분리: 비즈니스 로직은 CLI 파싱/출력과 분리된 모듈에서 처리됩니다.  
- `CA-002` 테스트 우선: 단위 테스트와 CLI 통합 테스트를 먼저 작성합니다.  
- `CA-003` 최소 의존성: 표준 라이브러리 기반으로 구현하며 외부 패키지를 도입하지 않습니다.  
- `CA-004` 단순함 우선: 필요한 핵심 기능만 구현하고 불필요한 추상화는 도입하지 않습니다.  
- `CA-005` CLI 범위: 사용자 상호작용은 명령행과 표준 입출력으로만 이루어집니다.

## Project Structure

### Documentation (this feature)

```text
specs/001-cli-todo-app/
├── plan.md
├── spec.md
└── checklists/
```

### Source Code (repository root)

```text
src/
└── todo/
    ├── __init__.py
    ├── cli.py
    ├── models.py
    ├── persistence.py
    └── service.py

todo.py

tests/
└── unit/
    ├── test_models.py
    ├── test_persistence.py
    ├── test_service.py
    └── test_cli.py
```

**Structure Decision**: 단일 Python CLI 프로젝트로 구현합니다. `src/todo/`에는 도메인 모델과 비즈니스 로직, 저장소가 위치하며, CLI 어댑터는 `src/todo/cli.py`에 둡니다. 테스트는 `tests/unit/`에 모아 작성합니다.

## Implementation Phases

### Phase 1: Setup
- 프로젝트 디렉토리 구조 생성
- 기본 모듈 및 테스트 파일 생성

### Phase 2: Foundation
- `ToDo` 모델 정의: ID, 제목, 마감일, 우선순위, 완료 여부, 생성 일시
- 로컬 파일 저장소 구현: 데이터 로드/저장, 파일 생성, 손상 복구
- 서비스 레이어 구현: 추가, 목록 조회, 필터, 완료, 삭제
- CLI 명령 파서 구현: `add`, `list`, `complete`, `delete`, `help`

### Phase 3: MVP
- `add` 기능 구현 및 테스트
- `list` 기능 구현 및 테스트
- `complete` 기능 구현 및 테스트
- `delete` 기능 구현 및 테스트

### Phase 4: Polish
- 입력 검증 및 오류 메시지 개선
- 날짜 형식 유효성 검사 및 우선순위 검증
- 파일 손상/동시 접근 시나리오 처리
- 문서화 및 `quickstart` 업데이트

## Complexity Tracking

별도 기술 또는 추가 아키텍처를 도입하지 않고, 명령행 기반 단일 기능 구현으로 단순한 구조를 유지합니다.
