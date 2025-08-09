# Useful MCP Servers for Claude Code

Claude CLI와 함께 사용할 수 있는 유용한 MCP (Model Context Protocol) 서버들을 정리한 종합 가이드입니다.

## MCP란?

MCP (Model Context Protocol)는 Claude가 외부 도구, API, 데이터베이스, 서비스와 실시간으로 상호작용할 수 있게 해주는 프로토콜입니다. MCP 서버들은 Claude Code를 동적이고 컨텍스트 인식이 가능한 어시스턴트로 변환시켜, 터미널을 떠나지 않고도 작업을 자동화하고 워크플로우를 간소화할 수 있게 해줍니다.

## 빠른 시작

### 필수 조건
- [Claude CLI](https://claude.ai/code) 설치됨
- Node.js 설치됨 (MCP 서버들이 npm을 통해 실행됨)

### 원클릭 설치 

<details>
<summary>🚀 검증된 모든 MCP 서버 한번에 설치</summary>

다음 명령어들로 검증된 MCP 서버들을 User Scope으로 설정할 수 있습니다:

```bash
# 1. 파일시스템 서버 (파일 읽기/쓰기)
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem C:\

# 2. GitHub 서버 (리포지토리 관리) - 토큰 설정 필요
claude mcp add github --scope user npx @modelcontextprotocol/server-github

# 3. 메모리 서버 (대화 기록 유지)
claude mcp add memory --scope user npx @modelcontextprotocol/server-memory

# 4. 순차적 사고 서버 (복잡한 작업 분해)
claude mcp add sequential-thinking --scope user npx @modelcontextprotocol/server-sequential-thinking

# 5. Figma 서버 (디자인-투-코드 변환) - 토큰 설정 필요
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=YOUR_FIGMA_TOKEN --stdio"

# 6. Puppeteer 서버 (브라우저 자동화)
claude mcp add puppeteer-server --scope user npx @hisma/server-puppeteer

# 7. Notion 서버 (Notion 워크스페이스 통합) - 토큰 설정 필요
claude mcp add notion-server --scope user npx @notionhq/notion-mcp-server -e NOTION_TOKEN=YOUR_NOTION_TOKEN
```

**토큰이 필요한 서버들**: GitHub, Figma, Notion - 각 서버 문서에서 토큰 생성 방법 확인
</details>

### 설치 확인
```bash
claude mcp list
# 모든 서버가 "✓ Connected" 상태인지 확인
```

## 📋 구현된 MCP 서버들

현재 **7개의 검증된 MCP 서버**가 사용 가능합니다:

| 서버 | 패키지 | 주요 기능 | 문서 |
|------|--------|----------|------|
| 🗂️ **Filesystem** | `@modelcontextprotocol/server-filesystem` | 파일 시스템 관리, 검색, 편집 | [📖 상세 가이드](docs/servers/filesystem.md) |
| 🐙 **GitHub** | `@modelcontextprotocol/server-github` | GitHub API 통합, 이슈/PR 관리 | [📖 상세 가이드](docs/servers/github.md) |
| 🧠 **Memory** | `@modelcontextprotocol/server-memory` | 지식 그래프, 대화 기록 유지 | [📖 상세 가이드](docs/servers/memory.md) |
| 🤔 **Sequential Thinking** | `@modelcontextprotocol/server-sequential-thinking` | 구조화된 사고 과정, 문제 해결 | [📖 상세 가이드](docs/servers/sequential-thinking.md) |
| 🎨 **Figma** | `figma-developer-mcp` | 디자인-투-코드 변환, 에셋 관리 | [📖 상세 가이드](docs/servers/figma.md) |
| 🌐 **Puppeteer** | `@hisma/server-puppeteer` | 브라우저 자동화, 웹 스크래핑 | [📖 상세 가이드](docs/servers/puppeteer.md) |
| 📝 **Notion** | `@notionhq/notion-mcp-server` | Notion 워크스페이스 통합 | [📖 상세 가이드](docs/servers/notion.md) |

### 🔄 실험적 서버들
테스트가 필요하거나 개발 중인 MCP 서버들: [📋 실험적 서버 목록](docs/experimental-servers.md)

## 🚀 인기 있는 사용 사례

### 개발자 워크플로우
- **코드 리뷰 자동화**: GitHub MCP로 PR 자동 리뷰 및 피드백
- **디자인-투-코드**: Figma MCP로 디자인을 실제 React/Vue 컴포넌트로 변환
- **프로젝트 문서화**: Memory MCP로 프로젝트 지식 체계화
- **테스트 자동화**: Puppeteer MCP로 웹 애플리케이션 자동 테스트

### 비즈니스 자동화
- **프로젝트 관리**: Notion MCP로 작업 추적 및 리포팅 자동화
- **경쟁사 모니터링**: Puppeteer MCP로 경쟁사 웹사이트 변화 추적
- **고객 지원**: 다중 MCP 서버 조합으로 고객 이슈 자동 분류 및 대응

### 콘텐츠 관리
- **소셜 미디어 관리**: 여러 플랫폼의 콘텐츠 수집 및 분석
- **SEO 최적화**: 웹사이트 성능 모니터링 및 개선 제안
- **브랜드 모니터링**: 온라인 브랜드 언급 추적 및 분석

## 🔧 환경 변수 설정

토큰이 필요한 서버들의 설정 가이드:

<details>
<summary>🔑 GitHub Personal Access Token</summary>

```bash
# 1. GitHub에서 토큰 생성
# https://github.com/settings/tokens

# 2. Windows에서 환경 변수 설정
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-token-here"
```
[👆 상세한 GitHub 토큰 설정 가이드](docs/servers/github.md#설치-및-설정)
</details>

<details>
<summary>🎨 Figma API Token</summary>

```bash
# 1. Figma에서 토큰 생성
# https://www.figma.com/developers/api#access-tokens

# 2. MCP 서버에 토큰 포함하여 설치
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=figd_YOUR_TOKEN --stdio"
```
[👆 상세한 Figma 토큰 설정 가이드](docs/servers/figma.md#설치-및-설정)
</details>

<details>
<summary>📝 Notion Integration Token</summary>

```bash
# 1. Notion에서 통합 생성
# https://www.notion.so/my-integrations

# 2. MCP 서버에 토큰 포함하여 설치
claude mcp add notion-server --scope user npx @notionhq/notion-mcp-server -e NOTION_TOKEN=secret_YOUR_TOKEN
```
[👆 상세한 Notion 토큰 설정 가이드](docs/servers/notion.md#설치-및-설정)
</details>

## 🛠 MCP 서버 관리

### 기본 명령어
```bash
# 서버 목록 확인
claude mcp list

# 특정 서버 정보 보기
claude mcp get <서버이름>

# 서버 제거
claude mcp remove <서버이름>

# User scope에서 제거
claude mcp remove <서버이름> -s user
```

### 범위 (Scope) 이해
- **User Scope** (권장): 모든 프로젝트에서 사용 가능
- **Local Scope**: 현재 디렉토리에서만 사용
- **Project Scope**: 팀과 공유 (`.mcp.json` 파일)

## 🔍 문제 해결

### 일반적인 문제
- **서버 연결 실패**: `npx` 패키지가 설치되어 있는지 확인
- **토큰 인증 오류**: 환경 변수나 토큰이 올바르게 설정되었는지 확인
- **권한 오류**: 파일 시스템 접근 권한이나 API 토큰 권한 확인

### 도움 받기
- **Claude Code 도움말**: `claude --help`
- **MCP 서버 도움말**: `claude mcp --help`
- **이슈 리포트**: [GitHub Issues](https://github.com/anthropics/claude-code/issues)

## 🤝 기여하기

### 새로운 MCP 서버 제안
1. [실험적 서버 목록](docs/experimental-servers.md)에서 테스트 진행
2. 성공적으로 테스트된 서버는 상세 문서 작성
3. Pull Request로 메인 목록에 추가 제안

### 문서 개선
- 오타나 부정확한 정보 수정
- 새로운 사용 사례 추가  
- 번역 기여

## 📚 참고 자료

- [Claude Code 공식 문서](https://docs.anthropic.com/en/docs/claude-code)
- [MCP 사양 문서](https://github.com/modelcontextprotocol/specification)
- [Awesome MCP Servers (wong2)](https://github.com/wong2/awesome-mcp-servers)
- [Awesome MCP Servers (punkpeye)](https://github.com/punkpeye/awesome-mcp-servers)

## 📊 프로젝트 상태

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI  
**검증된 서버 수**: 7개  
**실험적 서버 수**: 5+개  
**기여자**: 커뮤니티 기여 환영 🙌

---

💡 **팁**: MCP 서버들을 조합해서 사용하면 더욱 강력한 자동화 워크플로우를 만들 수 있습니다. 예를 들어, Figma에서 디자인을 가져와 코드로 변환한 후, GitHub에 자동으로 커밋하고, Notion에 작업 내역을 기록하는 전체 워크플로우가 가능합니다!