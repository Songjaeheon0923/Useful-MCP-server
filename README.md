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

# 6. Puppeteer 서버 (브라우저 자동화)
claude mcp add puppeteer-server --scope user npx @hisma/server-puppeteer

# 7. Notion 서버 (Notion 워크스페이스 통합)
# Notion 통합 토큰으로 YOUR_NOTION_TOKEN을 교체
claude mcp add notion-server --scope user npx @notionhq/notion-mcp-server -e NOTION_TOKEN=YOUR_NOTION_TOKEN
```

### 환경 변수 설정

<details>
<summary>🔧 GitHub 토큰 설정</summary>

#### GitHub 토큰 생성
1. [GitHub Settings > Personal Access Tokens](https://github.com/settings/tokens) 이동
2. **"Generate new token (classic)"** 클릭
3. 필요한 권한 선택:
   - `repo`: 리포지토리 액세스
   - `user`: 사용자 정보 읽기
   - `workflow`: GitHub Actions 관리
4. 생성된 토큰 복사

```bash
# Windows에서 영구적으로 설정
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-github-token-here"

# 현재 세션에서만 설정 (임시)
set GITHUB_PERSONAL_ACCESS_TOKEN=your-github-token-here
```
</details>

<details>
<summary>🎨 Figma 토큰 설정</summary>

#### Figma 토큰 생성
1. [Figma](https://www.figma.com) 로그인
2. **Settings** → **Personal Access Tokens** 이동
3. **Generate new token** 클릭
4. 토큰 이름 입력 (예: "Claude MCP")
5. 생성된 토큰 복사 (⚠️ 한 번만 표시됨!)

```bash
# 위에서 복사한 토큰으로 교체
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=figd_YOUR_ACTUAL_TOKEN_HERE --stdio"

# 연결 상태 확인
claude mcp list
```
</details>

<details>
<summary>📝 Notion 통합 설정</summary>

#### Notion 통합 토큰 생성
1. [Notion Integrations](https://www.notion.so/my-integrations) 페이지 이동
2. **"New integration"** 클릭
3. 통합 정보 입력:
   - **Name**: "Claude MCP" (또는 원하는 이름)
   - **Workspace**: 사용할 워크스페이스 선택
   - **Content Capabilities**: Read, Update, Insert 권한 선택
4. **Submit** 클릭하여 통합 생성
5. **Internal Integration Token** 복사 (secret_으로 시작)

#### 워크스페이스에 통합 연결
1. Notion에서 사용할 페이지나 데이터베이스 열기
2. 페이지 우상단 **"..."** → **"Connections"** 클릭
3. 생성한 통합 선택하여 연결

```bash
# 위에서 복사한 토큰으로 교체
claude mcp add notion-server --scope user npx @notionhq/notion-mcp-server -e NOTION_TOKEN=secret_YOUR_ACTUAL_TOKEN_HERE

# 연결 상태 확인
claude mcp list
```
</details>

### 설정 확인
```bash
# 연결된 MCP 서버 목록 확인
claude mcp list

# 다른 디렉토리에서도 테스트
cd C:\temp
claude mcp list  # User Scope 서버들이 모든 곳에서 보여야 함
```

## 구현된 MCP 서버 상세 가이드

<details>
<summary>📊 연결된 MCP 서버 현황</summary>

| 서버명 | 상태 | 주요기능 | 범위 |
|--------|------|----------|------|
| 🗂️ filesystem | ✅ 연결됨 | 파일 시스템 관리 | User |
| 🐙 github | ✅ 연결됨 | GitHub API 통합 | User |
| 🧠 memory | ✅ 연결됨 | 대화 기록 유지 | User |
| 🤔 sequential-thinking | ✅ 연결됨 | 복잡한 작업 분해 | User |
| 🎨 figma-framelink | ✅ 연결됨 | 디자인-투-코드 | User |
| 🌐 puppeteer-server | ✅ 연결됨 | 브라우저 자동화 | User |
| 📝 notion-server | ✅ 연결됨 | Notion 워크스페이스 | User |

**총 7개 서버 연결됨** | 모든 서버가 User Scope로 설정되어 모든 프로젝트에서 사용 가능
</details>

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

### 🌐 Puppeteer MCP Server (Browser Automation)
- **상태**: **연결됨**
- **패키지**: `@hisma/server-puppeteer`
- **GitHub**: [Puppeteer MCP Server](https://github.com/hisma/server-puppeteer)
- **기능**: 완전한 브라우저 자동화 및 웹 스크래핑

<details>
<summary>🚀 주요 기능</summary>

**🔧 브라우저 제어:**
- **페이지 네비게이션**: URL로 이동, 뒤로/앞으로 이동, 새로고침
- **요소 상호작용**: 클릭, 텍스트 입력, 드롭다운 선택, 호버
- **스크린샷**: 전체 페이지 또는 특정 요소 캡처 (PNG/JPEG)
- **JavaScript 실행**: 브라우저 컨텍스트에서 커스텀 JS 코드 실행

**📊 웹 스크래핑:**
- **DOM 요소 추출**: CSS 셀렉터로 텍스트, 속성, HTML 콘텐츠 추출
- **폼 자동화**: 로그인, 양식 작성, 제출 자동화
- **페이지 대기**: 특정 요소나 조건까지 대기
- **동적 콘텐츠**: JavaScript로 렌더링된 SPA 콘텐츠 스크래핑

**🛠️ 고급 기능:**
- **헤드리스/헤드풀 모드**: UI 표시 여부 선택
- **모바일 에뮬레이션**: 다양한 디바이스 크기 시뮬레이션
- **네트워크 제어**: 요청 인터셉트, 응답 모킹
- **PDF 생성**: 웹 페이지를 PDF로 변환
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

1. **`puppeteer_navigate`**: 지정된 URL로 이동
2. **`puppeteer_screenshot`**: 페이지 또는 요소 스크린샷 캡처
3. **`puppeteer_click`**: CSS 셀렉터로 요소 클릭
4. **`puppeteer_fill`**: 입력 필드에 텍스트 입력
5. **`puppeteer_select`**: 드롭다운에서 값 선택
6. **`puppeteer_hover`**: 요소에 마우스 호버
7. **`puppeteer_evaluate`**: 브라우저에서 JavaScript 코드 실행
8. **`puppeteer_get_content`**: 페이지의 HTML 콘텐츠 가져오기
9. **`puppeteer_wait_for_selector`**: 특정 요소가 나타날 때까지 대기
</details>

<details>
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"네이버 메인페이지를 스크린샷으로 캡처해주세요"
"이 사이트에서 제품 정보를 스크래핑해서 정리해주세요: https://example-shop.com"
"구글에서 'Claude AI' 검색 결과를 캡처해주세요"
"이 웹사이트의 로그인 폼을 자동으로 채워주세요"
"이 페이지를 PDF로 변환해주세요"
"동적으로 로드되는 콘텐츠를 기다린 후 스크래핑해주세요"
```

**⚡ 자동화 워크플로우 예시:**
- 웹사이트 모니터링 및 변경 사항 감지
- E-commerce 가격 추적 및 알림
- 소셜 미디어 콘텐츠 자동 수집
- 웹 애플리케이션 자동 테스트
- 정기적인 웹사이트 스크린샷 수집
</details>

### 📝 Notion MCP Server
- **상태**: **연결됨**
- **패키지**: `@notionhq/notion-mcp-server`
- **GitHub**: [Notion MCP Server](https://github.com/notionhq/notion-mcp-server)
- **기능**: Notion 워크스페이스와의 완전한 통합

<details>
<summary>🚀 주요 기능</summary>

**📊 페이지 및 데이터베이스 관리:**
- **페이지 CRUD**: 페이지 생성, 읽기, 수정, 삭제
- **데이터베이스 쿼리**: 복잡한 필터링 및 정렬 조건으로 데이터 검색
- **블록 관리**: 텍스트, 이미지, 표, 코드 블록 등 추가/편집
- **속성 관리**: 제목, 태그, 날짜, 체크박스 등 다양한 속성 처리

**🔍 검색 및 분석:**
- **전체 텍스트 검색**: 워크스페이스 전체에서 콘텐츠 검색
- **메타데이터 추출**: 페이지 생성일, 수정일, 작성자 정보
- **관계 분석**: 페이지 간 연결 및 백링크 추적
- **댓글 시스템**: 페이지 댓글 읽기 및 작성

**📝 콘텐츠 생성 자동화:**
- **템플릿 기반 페이지 생성**: 일관된 형식의 문서 자동 생성
- **bulk 작업**: 여러 페이지/항목을 한 번에 처리
- **데이터 동기화**: 외부 소스에서 Notion으로 데이터 자동 동기화
- **워크플로우 자동화**: 조건부 업데이트 및 알림
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

**사용자 관리:**
- `API-get-users`: 워크스페이스 사용자 목록 조회
- `API-get-user`: 특정 사용자 정보 조회
- `API-get-self`: 현재 봇 사용자 정보 조회

**검색:**
- `API-post-search`: 제목으로 페이지/데이터베이스 검색

**페이지 관리:**
- `API-retrieve-a-page`: 페이지 내용 및 속성 조회
- `API-patch-page`: 페이지 속성 업데이트
- `API-post-page`: 새 페이지 생성

**블록 관리:**
- `API-get-block-children`: 블록의 하위 콘텐츠 조회
- `API-patch-block-children`: 블록에 새로운 콘텐츠 추가
- `API-retrieve-a-block`: 특정 블록 정보 조회
- `API-update-a-block`: 블록 내용 수정
- `API-delete-a-block`: 블록 삭제

**데이터베이스:**
- `API-post-database-query`: 데이터베이스 쿼리 (필터링, 정렬)
- `API-create-a-database`: 새 데이터베이스 생성
- `API-update-a-database`: 데이터베이스 구조 수정
- `API-retrieve-a-database`: 데이터베이스 정보 조회

**댓글 시스템:**
- `API-retrieve-a-comment`: 페이지 댓글 조회
- `API-create-a-comment`: 새 댓글 작성

**속성 관리:**
- `API-retrieve-a-page-property`: 페이지 속성값 조회
</details>

<details>
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"내 Notion 워크스페이스에서 '프로젝트' 데이터베이스의 모든 항목을 보여주세요"
"새로운 회의록 페이지를 생성하고 오늘 날짜로 설정해주세요"
"'개발' 태그가 있는 모든 페이지를 찾아서 우선순위별로 정렬해주세요"
"이 페이지에 새로운 할 일 체크리스트를 추가해주세요"
"지난주에 수정된 모든 문서를 찾아주세요"
"이 템플릿을 사용해서 10개의 새로운 제품 페이지를 생성해주세요"
```

**⚡ 자동화 워크플로우 예시:**
- 일일 업무 보고서 자동 생성
- 프로젝트 상태 업데이트 자동화
- 외부 데이터를 Notion 데이터베이스로 자동 동기화
- 마감일 알림 및 상태 변경 자동화
- 회의록 템플릿 자동 생성 및 참석자 태그
</details>

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
**검증된 서버 수**: 7개 (filesystem, github, memory, sequential-thinking, figma-framelink, puppeteer-server, notion-server)