# Useful MCP Servers for Claude Code

Claude CLI와 함께 사용할 수 있는 유용한 MCP (Model Context Protocol) 서버들을 정리한 종합 가이드

## MCP란?

MCP (Model Context Protocol)는 Claude가 외부 도구, API, 데이터베이스, 서비스와 실시간으로 상호작용할 수 있게 해주는 프로토콜 MCP 서버들은 Claude Code를 동적이고 컨텍스트 인식이 가능한 어시스턴트로 변환시켜, 터미널을 떠나지 않고도 작업을 자동화하고 워크플로우를 간소화할 수 있게 해준다.

## 빠른 시작

### 필수 조건
- [Claude CLI](https://claude.ai/code) 설치됨
- Node.js 설치됨 (MCP 서버들이 npm을 통해 실행됨)

### 원클릭 설치 

<details>
<summary> 검증된 모든 MCP 서버 한번에 설치</summary>

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

| 서버 | 주요 기능 | readme |
|------|----------|------|
| 🗂️ **Filesystem** | 파일 시스템 관리, 검색, 편집 | [link](docs/servers/filesystem.md) |
| 🐙 **GitHub** | GitHub API 통합, 이슈/PR 관리 | [link](docs/servers/github.md) |
| 🧠 **Memory** | 지식 그래프, 대화 기록 유지 | [link](docs/servers/memory.md) |
| 🤔 **Sequential Thinking** | 구조화된 사고 과정, 문제 해결 | [link](docs/servers/sequential-thinking.md) |
| 🎨 **Figma** | 디자인-투-코드 변환, 에셋 관리 | [link](docs/servers/figma.md) |
| 🌐 **Puppeteer** | 브라우저 자동화, 웹 스크래핑 | [link](docs/servers/puppeteer.md) |
| 📝 **Notion** | Notion 워크스페이스 통합 | [link](docs/servers/notion.md) |

### 🔄 실험적 서버들
테스트가 필요하거나 개발 중인 MCP 서버들: [미실현 서버 목록](docs/experimental-servers.md)



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


## 📊 프로젝트 상태

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI  
**검증된 서버 수**: 7개  
**실험적 서버 수**: 5+개  
