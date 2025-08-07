# Useful MCP Servers for Claude Code

이 저장소는 Claude CLI와 함께 사용할 수 있는 유용한 MCP (Model Context Protocol) 서버들을 정리한 것입니다.

## MCP란?

MCP (Model Context Protocol)는 Claude가 외부 도구, API, 데이터베이스, 서비스와 실시간으로 상호작용할 수 있게 해주는 프로토콜입니다. MCP 서버들은 Claude Code를 동적이고 컨텍스트 인식이 가능한 어시스턴트로 변환시켜, 터미널을 떠나지 않고도 작업을 자동화하고 워크플로우를 간소화할 수 있게 해줍니다.

### MCP 서버 연결 범위 (Scope)

Claude Code는 3가지 범위에서 MCP 서버를 설정할 수 있습니다:

#### 1. **User Scope (추천)** - 모든 프로젝트에서 사용
```bash
# 모든 프로젝트에서 사용할 수 있는 글로벌 서버
claude mcp add <서버이름> --scope user <명령어> [인수...]
```
-  **장점**: 한 번 설정하면 모든 프로젝트에서 자동 사용
-  **적합한 용도**: 개인 개발 도구, 자주 사용하는 서비스
-  **저장 위치**: 사용자별 글로벌 설정

#### 2. **Local Scope** - 현재 프로젝트에서만 사용
```bash
# 현재 디렉토리에서만 사용
claude mcp add <서버이름> <명령어> [인수...]
```
-  **장점**: 프로젝트별 맞춤 설정
-  **적합한 용도**: 실험적 설정, 민감한 인증 정보
-  **저장 위치**: 현재 디렉토리의 `.claude.json`

#### 3. **Project Scope** - 팀과 공유
```bash
# 팀원들과 공유하는 설정 (프로젝트 루트에 .mcp.json 생성)
claude mcp add <서버이름> --scope project <명령어> [인수...]
```
-  **장점**: 팀원들과 설정 공유 가능
-  **주의**: 사용 전 승인 필요
-  **저장 위치**: 프로젝트 루트의 `.mcp.json` (버전 관리됨)

###  현재 테스트된 서버 구성 (User Scope)

다음 명령어들로 기본 MCP 서버를 User Scope으로 설정할 수 있습니다:

```bash
# 1. 파일시스템 서버 (파일 읽기/쓰기)
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem C:\

# 2. GitHub 서버 (리포지토리 관리)
claude mcp add github --scope user npx @modelcontextprotocol/server-github

# 3. 메모리 서버 (대화 기록 유지)
claude mcp add memory --scope user npx @modelcontextprotocol/server-memory

# 4. 웹 페치 서버 (웹 콘텐츠 가져오기)
claude mcp add fetch --scope user npx @modelcontextprotocol/server-fetch

# 5. 순차적 사고 서버 (복잡한 작업 분해)
claude mcp add sequential-thinking --scope user npx @modelcontextprotocol/server-sequential-thinking
```

###  환경 변수 설정

GitHub 서버 사용을 위한 토큰 설정:
```bash
# Windows에서 영구적으로 설정
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-github-token-here"
```

###  설정 확인
```bash
# 연결된 MCP 서버 목록 확인
claude mcp list

# 다른 디렉토리에서도 테스트
cd C:\temp
claude mcp list  # User Scope 서버들이 모든 곳에서 보여야 함
```

## 필수 MCP 서버들

###  개발 도구

#### 1. GitHub MCP Server
- **기능**: GitHub API 연결로 이슈 읽기, PR 관리, CI/CD 트리거, 커밋 분석
- **GitHub**: [Official GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)
- **사용법**: GitHub 토큰으로 인증 후 리포지토리와 상호작용

#### 2. File System Server
- **기능**: 파일 읽기/쓰기/편집, 프로젝트 관리, 로그 분석
- **GitHub**: [Filesystem MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- **사용법**: 안전한 파일 작업을 위한 구성 가능한 액세스 제어

#### 3. Browser Automation (Puppeteer)
- **기능**: 웹 자동화 기능
- **GitHub**: [Browser MCP](https://github.com/adhikasp/browser-mcp)
- **사용법**: 로컬 브라우저 자동화

###  데이터베이스 & API

#### 4. PostgreSQL/Database Server
- **기능**: PostgreSQL, MySQL, BigQuery 등 다중 데이터베이스 지원
- **GitHub**: [PostgreSQL MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres)
- **사용법**: 범용 데이터베이스 MCP 서버

#### 5. Apidog MCP Server
- **기능**: API 문서화, 테스팅, 코드 생성
- **설명**: API 개발 워크플로우 통합

###  AI 및 자동화

#### 6. Zen MCP Server
- **기능**: 여러 AI 모델을 개발팀으로 조직화, Claude가 각 작업에 최적의 모델 선택
- **GitHub**: [Zen MCP Server](https://github.com/BeehiveInnovations/zen-mcp-server)
- **특징**: Gemini, OpenAI, Grok, OpenRouter, Ollama, 커스텀 모델 지원

#### 7. Sequential Thinking Server
- **기능**: 복잡한 작업을 논리적 단계로 분해하여 아키텍처, 리팩토링, 계획 수립
- **설명**: 복잡한 프로젝트 관리에 유용

### 생산성 도구

#### 8. Memory Bank Server
- **기능**: 대규모 프로젝트 및 복잡한 로직 관리
- **설명**: 프로젝트 컨텍스트 유지


## 특수 목적 서버들

### 분석 & 모니터링

#### AgentOps
- **기능**: AI 에이전트 디버깅을 위한 관찰성 및 추적

## 클라우드 서비스 통합

### Alibaba Cloud
- AnalyticDB for MySQL
- AnalyticDB for PostgreSQL
- DataWorks
- OpenSearch
- Cloud OPS
- RDS


## 고급 설정 및 관리

### MCP 서버 관리 명령어
```bash
# 서버 목록 확인
claude mcp list

# 특정 서버 정보 보기
claude mcp get <서버이름>

# 서버 제거
claude mcp remove <서버이름>

# 서버 상태 확인
claude mcp list  # ✓ Connected 또는 ✗ Failed 표시
```

### 범위별 우선순위
1. **Local Scope** (최우선)
2. **Project Scope**
3. **User Scope** (최하위)

동일한 이름의 서버가 여러 범위에 있을 경우, 위 순서대로 적용됩니다.

### 🛠 문제 해결
- **서버가 연결되지 않을 때**: `npx` 패키지가 설치되어 있는지 확인
- **GitHub 서버 인증 실패**: 환경 변수 `GITHUB_PERSONAL_ACCESS_TOKEN` 확인
- **다른 프로젝트에서 서버가 보이지 않을 때**: `--scope user` 옵션으로 다시 설정

## 참고 자료

- [Awesome MCP Servers (wong2)](https://github.com/wong2/awesome-mcp-servers)
- [Awesome MCP Servers (punkpeye)](https://github.com/punkpeye/awesome-mcp-servers)
- [Official MCP Servers](https://github.com/modelcontextprotocol/servers)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)

## 기여하기

새로운 유용한 MCP 서버를 발견하시면 PR을 통해 추가해주세요!

---

*이 목록은 2025년 8월 기준으로 작성되었으며, 지속적으로 업데이트됩니다.*