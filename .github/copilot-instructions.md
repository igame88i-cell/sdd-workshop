<!-- SPECKIT START -->
For additional context about technologies to be used, project structure,
shell commands, and other important information, read the current plan
global context below. This context is meant to inform your execution of the implementation plan and should be considered alongside the feature specification.
globla instructions: 폴더임 
<!-- SPECKIT END -->
# 언어 규칙
- 모든 응답은 한국어로 작성되어야 합니다.
- 기술 용어는 영어로 유지하되, 필요한 경우 괄호 안에 한국어 설명을 추가할 수 있습니다.
- 코드 스니펫과 명령어는 영어로 작성되어야 합니다.
- 응답은 명확하고 간결해야 하며, 불필요한 장황한 설명은 피해야 합니다.
- 질문이 명확하지 않거나추가 정보가 필요한 경우, 명확한 질문을 통해 필요한 정보를 요청해야 합니다.
# 기술 스택
- 백엔드: Node.js, Express
- 프론트엔드: React
- 데이터베이스: MongoDB
- 버전 관리: Git
- 배포: Docker, AWS
# 프로젝트 구조
```
my-project/
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/           
│   └── app.js
├── frontend/
│   ├── components/
│   ├── pages/
│   └── App.js
├── database/
│   └── connection.js
├── .git/
├── Dockerfile
├── docker-compose.yml
├── README.md
└── .github/
    ├── copilot-instructions.md
    └── agents/
        ├── speckit.constitution.agent.md
        ├── speckit.git.commit.agent.md     
        ├── speckit.git.feature.agent.md
        └── speckit.plan.agent.md
```
# 주요 명령어
- 백엔드 서버 시작: `npm run start:backend`
- 프론트엔드 서버 시작: `npm run start:frontend`
- 데이터베이스 연결: `npm run start:database`
- 전체 프로젝트 시작 (Docker): `docker-compose up`      
- Git 커밋: `git commit -m "커밋 메시지"`
- Git 브랜치 생성: `git checkout -b feature/브랜치명`
- Git 브랜치 병합: `git checkout main` → `git merge feature/
브랜치명`
- Git 푸시: `git push origin 브랜치명`    
- Git 풀: `git pull origin main`
- Docker 이미지 빌드: `docker build -t 이미지명 .`
- Docker 컨테이너 실행: `docker run -p 호스트포트:컨테이너포트 이미지명`  
- Docker Compose 실행: `docker-compose up`
- Docker Compose 중지: `docker-compose down`
- AWS 배포: `aws deploy push --application-name 애플리케이션명 --s3-location s3://버킷명/배포패키지.zip`
