# Useful MCP Servers for Claude Code

Claude CLI와 함께 사용할 수 있는 유용한 MCP (Model Context Protocol) 서버들을 정리

## MCP란?

MCP (Model Context Protocol)는 Claude가 외부 도구, API, 데이터베이스, 서비스와 실시간으로 상호작용할 수 있게 해주는 프로토콜이다. MCP 서버들은 Claude Code를 동적이고 컨텍스트 인식이 가능한 어시스턴트로 변환시켜, 터미널을 떠나지 않고도 작업을 자동화하고 워크플로우를 간소화할 수 있게 해준다.

### MCP 서버 연결 범위 (Scope)

Claude Code는 3가지 범위에서 MCP 서버를 설정할 수 있지만 본인은 로컬 전역 범위로만 설정함

#### 1. **User Scope** - 모든 프로젝트에서 사용
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
- **패키지**: `@modelcontextprotocol/server-github`
- **GitHub**: [Official GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)
- **기능**: 완전한 GitHub API 통합

<details>
<summary>🚀 주요 기능</summary>

**📊 리포지토리 관리:**
- **리포지토리 CRUD**: 생성, 포크, 검색, 메타데이터 조회
- **파일 관리**: 단일/다중 파일 생성, 업데이트, 읽기
- **브랜치 관리**: 새 브랜치 생성, 전환, 커밋 히스토리 조회
- **콘텐츠 검색**: 코드, 이슈, PR, 사용자 검색

**🔧 이슈 및 PR 관리:**
- **이슈 관리**: 생성, 업데이트, 댓글 추가, 라벨/마일스톤 설정
- **풀 리퀘스트**: 생성, 리뷰, 머지, 상태 확인
- **코드 리뷰**: 리뷰 작성, 댓글 추가, 승인/변경요청
- **자동화**: 상태 체크, CI/CD 트리거
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

**리포지토리 관리:**
- `create_repository`: 새 리포지토리 생성
- `search_repositories`: 리포지토리 검색
- `fork_repository`: 리포지토리 포크
- `get_file_contents`: 파일 내용 조회
- `create_or_update_file`: 파일 생성/업데이트
- `push_files`: 여러 파일 한 번에 커밋

**이슈 관리:**
- `create_issue`: 새 이슈 생성
- `list_issues`: 이슈 목록 조회 (필터링 지원)
- `get_issue`: 특정 이슈 상세 조회
- `update_issue`: 이슈 업데이트
- `add_issue_comment`: 이슈에 댓글 추가

**풀 리퀘스트:**
- `create_pull_request`: PR 생성
- `list_pull_requests`: PR 목록 조회
- `get_pull_request`: PR 상세 정보
- `get_pull_request_files`: PR 변경 파일 목록
- `create_pull_request_review`: PR 리뷰 작성
- `merge_pull_request`: PR 머지

**검색 기능:**
- `search_code`: 코드 검색
- `search_issues`: 이슈/PR 검색
- `search_users`: 사용자 검색
</details>

<details>
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"이 리포지토리의 모든 열린 이슈를 우선순위별로 정렬해서 보여주세요"
"main 브랜치에서 feature/new-auth 브랜치를 생성해주세요"
"이 PR을 검토하고 코드 리뷰를 작성해주세요"
"최근 일주일간의 커밋을 분석해서 변경사항을 요약해주세요"
"버그 리포트 이슈를 생성하고 적절한 라벨을 추가해주세요"
"이 파일을 여러 브랜치에 동시에 업데이트해주세요"
```

**⚡ 자동화 워크플로우 예시:**
- 이슈 트리거 기반 자동 PR 생성
- 코드 리뷰 자동화 및 피드백
- 릴리스 노트 자동 생성
- CI/CD 파이프라인 상태 모니터링
- 프로젝트 메트릭 수집 및 보고서 생성
</details>

### 📁 File System Server  
- **상태**: **연결됨**
- **패키지**: `@modelcontextprotocol/server-filesystem`
- **GitHub**: [Filesystem MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- **기능**: 안전하고 강력한 파일 시스템 관리

<details>
<summary>🚀 주요 기능</summary>

**📂 파일 관리:**
- **파일 CRUD**: 생성, 읽기, 수정, 삭제, 이동/이름변경
- **디렉토리 관리**: 생성, 나열, 트리 구조 조회
- **다중 파일 처리**: 여러 파일 동시 읽기 및 배치 작업
- **메타데이터**: 파일 크기, 수정일, 권한 등 상세 정보

**🔍 검색 및 탐색:**
- **패턴 기반 검색**: 파일명 및 경로 패턴 매칭
- **재귀 검색**: 하위 디렉토리 포함 전체 검색
- **제외 패턴**: 불필요한 파일/디렉토리 필터링
- **크기별 정렬**: 파일 크기 기준 정렬 및 분석
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

- `read_text_file`: 텍스트 파일 읽기 (부분 읽기 지원)
- `read_multiple_files`: 여러 파일 동시 읽기  
- `write_file`: 파일 생성/덮어쓰기
- `edit_file`: 라인 기반 파일 편집
- `create_directory`: 디렉토리 생성
- `list_directory`: 디렉토리 내용 나열
- `list_directory_with_sizes`: 크기 정보 포함 나열
- `directory_tree`: 재귀적 트리 구조 조회
- `move_file`: 파일/디렉토리 이동/이름변경
- `search_files`: 패턴 기반 파일 검색
- `get_file_info`: 파일 메타데이터 조회
</details>

<details>
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"프로젝트의 모든 .py 파일에서 deprecated 함수를 찾아주세요"
"이 디렉토리를 정리해서 파일을 용도별로 분류해주세요"
"로그 파일들을 크기별로 정렬하고 가장 큰 10개 파일을 보여주세요"
"이 설정 파일의 특정 값을 모든 환경에서 동일하게 업데이트해주세요"
"백업 파일들 중 30일 이상 된 파일들을 찾아주세요"
```
</details>

### 🧠 Memory Server
- **상태**: **연결됨**  
- **패키지**: `@modelcontextprotocol/server-memory`
- **GitHub**: [Memory MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/memory)
- **기능**: 지속적인 기억과 컨텍스트 관리

<details>
<summary>🚀 주요 기능</summary>

**🧩 지식 그래프:**
- **엔티티 관리**: 사람, 프로젝트, 개념 등 구조화된 정보 저장
- **관계 매핑**: 엔티티 간 복잡한 관계 정의 및 탐색
- **관찰 기록**: 각 엔티티에 대한 시간순 관찰 사항 누적
- **컨텍스트 유지**: 대화 세션 간 정보 연속성 보장

**🔍 스마트 검색:**
- **의미론적 검색**: 키워드뿐만 아니라 의미 기반 검색
- **관계 추론**: 직간접적 연결 관계를 통한 정보 발견
- **시간적 추적**: 정보 변화 과정 및 히스토리 추적
- **자동 분류**: 유사한 패턴 및 주제별 자동 그룹핑
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

- `create_entities`: 새로운 엔티티 생성 (여러 개 동시 생성)
- `create_relations`: 엔티티 간 관계 정의
- `add_observations`: 기존 엔티티에 새 관찰 사항 추가
- `delete_entities`: 엔티티 및 관련 관계 삭제
- `delete_observations`: 특정 관찰 사항 삭제
- `delete_relations`: 엔티티 간 관계 삭제
- `read_graph`: 전체 지식 그래프 조회
- `search_nodes`: 패턴 기반 노드 검색
- `open_nodes`: 특정 엔티티들의 상세 정보 조회
</details>

<details>
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"프로젝트 A와 관련된 모든 사람과 기술을 기록해주세요"
"지금까지 논의한 API 설계 요구사항들을 정리해서 저장해주세요"  
"이전에 언급한 성능 이슈와 관련된 모든 정보를 찾아주세요"
"팀 멤버들의 전문 분야와 담당 업무를 매핑해주세요"
"이 버그와 유사한 과거 이슈들을 찾아서 해결 방안을 제안해주세요"
```
</details>

### 🤔 Sequential Thinking Server
- **상태**: **연결됨**
- **패키지**: `@modelcontextprotocol/server-sequential-thinking`  
- **GitHub**: [Sequential Thinking MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/sequential-thinking)
- **기능**: 구조화된 사고 과정 및 문제 해결

<details>
<summary>🚀 주요 기능</summary>

**🧠 체계적 사고:**
- **단계별 분해**: 복잡한 문제를 논리적 단계로 체계화
- **가설 검증**: 가정 설정 → 검증 → 수정의 반복 과정
- **다각적 분석**: 여러 관점에서 문제 접근 및 분석
- **동적 조정**: 사고 과정 중 방향 전환 및 깊이 조절

**🔄 적응형 프로세스:**
- **브랜치 사고**: 여러 해결 경로 동시 탐색
- **백트래킹**: 막다른 길에서 이전 단계로 돌아가기
- **점진적 개선**: 초기 해결책을 지속적으로 정교화
- **불확실성 관리**: 확신이 없는 부분을 명시적으로 표현
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

- `sequentialthinking`: 구조화된 사고 과정 실행
  - `thought`: 현재 사고 단계 내용
  - `thoughtNumber`: 현재 사고 단계 번호  
  - `totalThoughts`: 예상 총 사고 단계 수
  - `nextThoughtNeeded`: 추가 사고 단계 필요 여부
  - `isRevision`: 이전 사고 수정 여부
  - `revisesThought`: 수정하는 사고 단계 번호
  - `branchFromThought`: 분기점 사고 단계
  - `branchId`: 분기 식별자
</details>

<details>  
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"이 아키텍처 설계를 단계별로 검토하고 개선점을 찾아주세요"
"복잡한 알고리즘 문제를 체계적으로 분해해서 해결해주세요"
"이 비즈니스 요구사항을 기술적 구현 계획으로 변환해주세요"
"여러 기술 선택지를 비교 분석해서 최적의 솔루션을 제안해주세요"
"이 버그의 근본 원인을 논리적으로 추적해서 찾아주세요"
```

**⚡ 적용 영역:**
- 시스템 설계 및 아키텍처 계획
- 복잡한 디버깅 및 문제 해결  
- 프로젝트 계획 수립 및 리스크 분석
- 코드 리팩토링 전략 수립
- 기술 의사결정 프로세스
</details>

### 🎨 Figma MCP Server (Framelink)
- **상태**: **연결됨**
- **패키지**: `figma-developer-mcp`
- **GitHub**: [Figma Context MCP](https://github.com/GLips/Figma-Context-MCP)
- **기능**: 디자인을 코드로 변환하는 고급 Figma 통합

<details>
<summary>🚀 주요 기능</summary>

**🎨 디자인-투-코드 변환:**
- **다중 프레임워크 지원**: HTML/CSS, React, Vue, Angular, Svelte 등으로 변환
- **스마트 레이아웃 분석**: Figma Auto Layout을 CSS Grid/Flexbox로 자동 변환
- **반응형 디자인**: 다양한 화면 크기에 맞는 미디어 쿼리 자동 생성
- **컴포넌트 시스템**: Figma 컴포넌트를 재사용 가능한 코드 컴포넌트로 변환

**📊 디자인 시스템 분석:**
- **스타일 토큰 추출**: 색상, 타이포그래피, 간격 등을 CSS 변수로 변환
- **컴포넌트 라이브러리**: 디자인 시스템의 모든 컴포넌트를 코드로 생성
- **일관성 검사**: 디자인 시스템 내 스타일 일관성 검증
- **변경 사항 추적**: 디자인 업데이트 시 코드 동기화

**🖼️ 에셋 관리:**
- **자동 이미지 최적화**: PNG, JPG, SVG 형식으로 자동 추출 및 최적화
- **아이콘 시스템**: SVG 아이콘을 컴포넌트화하여 관리
- **이미지 크롭**: 정확한 크기와 비율로 이미지 자동 크롭
- **리소스 번들링**: 모든 에셋을 프로젝트 구조에 맞게 조직화
</details>

<details>
<summary>📋 사용 가능한 도구들</summary>

- `get_figma_data`: 전체 Figma 파일 또는 특정 노드 분석
- `download_figma_images`: 이미지 및 아이콘 자동 다운로드 및 최적화

**설정 옵션:**
- `fileKey`: Figma 파일 키 (URL에서 추출)
- `nodeId`: 특정 노드/프레임 ID (선택적)
- `depth`: 노드 트리 탐색 깊이 제어
- `localPath`: 이미지 저장 경로
- `pngScale`: PNG 이미지 스케일 (기본값: 2)
</details>

<details>
<summary>🔧 고급 설정 옵션</summary>

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
</details>

<details>
<summary>📝 사용 예시</summary>

```bash
# Claude에서 사용 예시:
"이 Figma 파일을 React 컴포넌트로 변환해주세요: https://www.figma.com/file/abc123/MyDesign"
"이 프레임의 CSS를 Tailwind CSS로 생성해주세요"
"디자인 시스템에서 버튼 컴포넌트만 추출해서 코드로 만들어주세요"
"모든 아이콘을 SVG로 다운로드하고 React 컴포넌트로 만들어주세요"
"이 페이지 디자인을 반응형 HTML로 변환해주세요"
"Figma 컴포넌트 라이브러리를 Storybook으로 생성해주세요"
```

**⚡ 자동화 워크플로우 예시:**
- 디자인 시스템 업데이트 시 자동 코드 동기화
- Figma → GitHub PR 자동 생성
- 디자인 토큰 자동 추출 및 스타일 가이드 생성
- 프로토타입을 실제 작동하는 코드로 변환
- A/B 테스트용 다중 디자인 버전 코드 생성
</details>

### 🌐 Puppeteer MCP Server
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

## 🔄 테스트 필요한 MCP 서버들

### 개발 도구

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