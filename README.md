# Useful MCP Servers for Claude Code

Claude CLI와 함께 사용할 수 있는 유용한 MCP (Model Context Protocol) 서버들을 정리

## MCP란?

MCP (Model Context Protocol)는 Claude가 외부 도구, API, 데이터베이스, 서비스와 실시간으로 상호작용할 수 있게 해주는 프로토콜이다. MCP 서버들은 Claude Code를 동적이고 컨텍스트 인식이 가능한 어시스턴트로 변환시켜, 터미널을 떠나지 않고도 작업을 자동화하고 워크플로우를 간소화할 수 있게 해준다.

### MCP 서버 연결 범위 (Scope)

Claude Code는 3가지 범위에서 MCP 서버를 설정할 수 있다:

#### 1. **User Scope (추천)** - 모든 프로젝트에서 사용
```bash
# 모든 프로젝트에서 사용할 수 있는 글로벌 서버
claude mcp add <서버이름> --scope user <명령어> [인수...]
```
- **장점**: 한 번 설정하면 모든 프로젝트에서 자동 사용
- **적합한 용도**: 개인 개발 도구, 자주 사용하는 서비스
- **저장 위치**: 사용자별 글로벌 설정

#### 2. **Local Scope** - 현재 프로젝트에서만 사용
```bash
# 현재 디렉토리에서만 사용
claude mcp add <서버이름> <명령어> [인수...]
```
- **장점**: 프로젝트별 맞춤 설정
- **적합한 용도**: 실험적 설정, 민감한 인증 정보
- **저장 위치**: 현재 디렉토리의 `.claude.json`

#### 3. **Project Scope** - 팀과 공유
```bash
# 팀원들과 공유하는 설정 (프로젝트 루트에 .mcp.json 생성)
claude mcp add <서버이름> --scope project <명령어> [인수...]
```
- **장점**: 팀원들과 설정 공유 가능
- **주의**: 사용 전 승인 필요
- **저장 위치**: 프로젝트 루트의 `.mcp.json` (버전 관리됨)

## 구현 및 테스트 완료된 MCP 서버들

### 빠른 설정 (원 클릭 설치)

다음 명령어들로 검증된 MCP 서버들을 User Scope으로 설정할 수 있다:

```bash
# 1. 파일시스템 서버 (파일 읽기/쓰기)
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem C:\

# 2. GitHub 서버 (리포지토리 관리
claude mcp add github --scope user npx @modelcontextprotocol/server-github

# 3. 메모리 서버 (대화 기록 유지)
claude mcp add memory --scope user npx @modelcontextprotocol/server-memory

# 4. 순차적 사고 서버 (복잡한 작업 분해)
claude mcp add sequential-thinking --scope user npx @modelcontextprotocol/server-sequential-thinking

# 5. Figma 서버 (디자인-투-코드 변환 
# Figma 개인 액세스 토큰으로 YOUR_FIGMA_TOKEN을 교체
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=YOUR_FIGMA_TOKEN --stdio"
```

### 환경 변수 설정

#### GitHub 토큰 설정
```bash
# Windows에서 영구적으로 설정
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-github-token-here"
```

#### Figma 토큰 설정

**1단계: Figma 개인 액세스 토큰 생성**
1. [Figma](https://www.figma.com) 로그인
2. **Settings** → **Personal Access Tokens** 이동
3. **Generate new token** 클릭
4. 토큰 이름 입력 (예: "Claude MCP")
5. 생성된 토큰 복사 (⚠️ 한 번만 표시됨!)

**2단계: 토큰으로 서버 설정**
```bash
# 위에서 복사한 토큰으로 교체
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=figd_YOUR_ACTUAL_TOKEN_HERE --stdio"

# 연결 상태 확인
claude mcp list
```

### 설정 확인
```bash
# 연결된 MCP 서버 목록 확인
claude mcp list

# 다른 디렉토리에서도 테스트
cd C:\temp
claude mcp list  # User Scope 서버들이 모든 곳에서 보여야 함
```

## 구현된 MCP 서버 상세 가이드

### 🐙 GitHub MCP Server
- **상태**: **연결됨**
- **기능**: GitHub API 연결로 이슈 읽기, PR 관리, CI/CD 트리거, 커밋 분석
- **GitHub**: [Official GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)
- **사용법**: GitHub 토큰으로 인증 후 리포지토리와 상호작용

### 📁 File System Server
- **상태**: **연결됨**
- **기능**: 파일 읽기/쓰기/편집, 프로젝트 관리, 로그 분석
- **GitHub**: [Filesystem MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- **사용법**: 안전한 파일 작업을 위한 구성 가능한 액세스 제어

### 🧠 Memory Server
- **상태**: **연결됨**
- **기능**: 대화 기록 및 컨텍스트 유지, 프로젝트 상태 관리
- **GitHub**: [Memory MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/memory)
- **사용법**: 세션 간 정보 유지 및 지식 그래프 생성

### 🤔 Sequential Thinking Server
- **상태**: **연결됨**
- **기능**: 복잡한 작업을 논리적 단계로 분해하여 아키텍처, 리팩토링, 계획 수립
- **GitHub**: [Sequential Thinking MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/sequential-thinking)
- **사용법**: 복잡한 프로젝트 관리 및 문제 해결에 유용

### 🎨 Figma MCP Server (Framelink)
- **상태**: **연결됨**
- **기능**: Figma 디자인을 코드로 자동 변환, 디자인 시스템 통합
- **GitHub**: [Figma Context MCP](https://github.com/GLips/Figma-Context-MCP)
- **패키지**: `figma-developer-mcp`

**🚀 주요 기능:**
- **디자인-투-코드 변환**: Figma 프레임을 HTML/CSS, React, Vue, Angular 등으로 원샷 변환
- **스마트 분석**: 복잡한 Figma API 응답을 AI가 이해하기 쉬운 레이아웃/스타일 정보로 단순화
- **이미지 자동화**: 디자인 내 모든 이미지를 PNG/JPG/SVG로 자동 다운로드 및 최적화
- **컴포넌트 추출**: Figma 컴포넌트와 스타일 가이드를 재사용 가능한 코드 컴포넌트로 변환
- **반응형 지원**: 다양한 화면 크기에 맞는 CSS Grid/Flexbox 및 미디어 쿼리 자동 생성

**🔧 고급 설정 옵션:**
```bash
# 기본 설정 (YAML 형식)
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=YOUR_TOKEN --stdio"

# JSON 형식으로 데이터 출력 (구조화된 분석용)
claude mcp add figma-json --scope user "npx figma-developer-mcp --figma-api-key=YOUR_TOKEN --json --stdio"

# 이미지 다운로드 스킵 (성능 최적화)
claude mcp add figma-light --scope user "npx figma-developer-mcp --figma-api-key=YOUR_TOKEN --skip-image-downloads --stdio"

# OAuth 토큰 사용 (팀/조직 계정용)
claude mcp add figma-oauth --scope user "npx figma-developer-mcp --figma-oauth-token=YOUR_OAUTH_TOKEN --stdio"
```

**📋 사용 가능한 도구들:**
1. **`get_figma_file`**: 전체 Figma 파일 분석 및 구조 파악
2. **`get_figma_frame`**: 특정 프레임의 상세 디자인 정보 추출
3. **`download_figma_images`**: 디자인 내 모든 이미지 자동 다운로드
4. **`analyze_design_system`**: 컴포넌트, 스타일, 토큰 시스템 분석
5. **`convert_to_code`**: 다양한 프레임워크로 코드 변환

**📝 사용 예시:**
```bash
# Claude에서 사용
"이 Figma 파일을 React 컴포넌트로 변환해주세요: https://www.figma.com/file/abc123/MyDesign"
"이 프레임의 CSS를 Tailwind CSS로 생성해주세요"
"디자인 시스템에서 버튼 컴포넌트만 추출해서 코드로 만들어주세요"
```

## 🔄 테스트 필요한 MCP 서버들

### 개발 도구

#### Browser Automation (Puppeteer)
- **상태**:  **테스트 필요**
- **기능**: 웹 자동화 기능
- **GitHub**: [Browser MCP](https://github.com/adhikasp/browser-mcp)
- **사용법**: 로컬 브라우저 자동화

#### Fetch Server
- **상태**: ⚠️ **패키지 미존재** (`@modelcontextprotocol/server-fetch` 찾을 수 없음)
- **기능**: 웹 콘텐츠 가져오기 (현재 내장 WebFetch 도구로 대체 가능)
- **대안**: 내장 WebFetch 도구 사용 권장

### 데이터베이스 & API

#### PostgreSQL/Database Server
- **상태**:  **테스트 필요**
- **기능**: PostgreSQL, MySQL, BigQuery 등 다중 데이터베이스 지원
- **GitHub**: [PostgreSQL MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres)
- **사용법**: 범용 데이터베이스 MCP 서버

#### Apidog MCP Server
- **상태**:  **테스트 필요**
- **기능**: API 문서화, 테스팅, 코드 생성
- **설명**: API 개발 워크플로우 통합

### AI 및 자동화

#### Zen MCP Server
- **상태**:  **테스트 필요**
- **기능**: 여러 AI 모델을 개발팀으로 조직화, Claude가 각 작업에 최적의 모델 선택
- **GitHub**: [Zen MCP Server](https://github.com/BeehiveInnovations/zen-mcp-server)
- **특징**: Gemini, OpenAI, Grok, OpenRouter, Ollama, 커스텀 모델 지원

### 특수 목적 서버들

#### AgentOps
- **상태**:  **테스트 필요**
- **기능**: AI 에이전트 디버깅을 위한 관찰성 및 추적

### 클라우드 서비스 통합

#### Alibaba Cloud
- **상태**:  **테스트 필요**
- AnalyticDB for MySQL
- AnalyticDB for PostgreSQL
- DataWorks
- OpenSearch
- Cloud OPS
- RDS

## 🛠️ MCP 서버 관리

### 관리 명령어
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

동일한 이름의 서버가 여러 범위에 있을 경우, 위 순서대로 적용.

### 🛠 문제 해결
- **서버가 연결되지 않을 때**: `npx` 패키지가 설치되어 있는지 확인
- **GitHub 서버 인증 실패**: 환경 변수 `GITHUB_PERSONAL_ACCESS_TOKEN` 확인
- **Figma 서버 연결 실패**: Figma API 토큰이 올바른지 확인
- **다른 프로젝트에서 서버가 보이지 않을 때**: `--scope user` 옵션으로 다시 설정

## 참고 자료

- [Awesome MCP Servers (wong2)](https://github.com/wong2/awesome-mcp-servers)
- [Awesome MCP Servers (punkpeye)](https://github.com/punkpeye/awesome-mcp-servers)
- [Official MCP Servers](https://github.com/modelcontextprotocol/servers)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)

---

*이 목록은 2025년 8월 기준으로 작성되었으며, 지속적으로 업데이트된다.*

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI  
**검증된 서버 수**: 5개 (filesystem, github, memory, sequential-thinking, figma-framelink)