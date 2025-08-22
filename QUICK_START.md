# MCP 서버 빠른 시작 가이드

새로운 사용자가 바로 따라할 수 있는 단계별 명령어 모음입니다.

## 전체 설정 과정 

### 1단계: GitHub 토큰 생성
1. https://github.com/settings/tokens 접속
2. **Generate new token (classic)** 클릭
3. 권한 선택:
   -  `repo` (저장소 접근)
   -  `read:user` (사용자 정보)  
   -  `read:org` (조직 정보)
4. 토큰 복사

### 2단계: 환경 변수 설정

**방법 1: .env 파일 사용 (권장)**
```bash
# 프로젝트에 .env 파일이 있으면 토큰을 입력하세요:
# 파일을 열어서 다음 라인을 수정:
GITHUB_PERSONAL_ACCESS_TOKEN=your-github-token-here
TWENTY_FIRST_API_KEY=your-magic-api-key-here
```

**방법 2: 시스템 환경 변수**
```bash
# Windows (PowerShell/CMD)
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-github-token-here"

# macOS/Linux
export GITHUB_PERSONAL_ACCESS_TOKEN="your-github-token-here"
echo 'export GITHUB_PERSONAL_ACCESS_TOKEN="your-github-token-here"' >> ~/.bashrc
```

### 3단계: MCP 서버 설치 (User Scope - 모든 프로젝트에서 사용)

#### 3-1. 패키지 글로벌 설치
```bash
# 모든 MCP 서버 패키지를 먼저 설치
npm install -g @modelcontextprotocol/server-filesystem
npm install -g @modelcontextprotocol/server-github
npm install -g @modelcontextprotocol/server-memory
npm install -g @modelcontextprotocol/server-sequential-thinking
npm install -g mcp-server-fetch-typescript
npm install -g @upstash/context7-mcp
npm install -g @21st-dev/magic
npm install -g @notionhq/notion-mcp-server
npm install -g mcp-figma
```

#### 3-2. MCP 서버 추가
```bash
# 1. 파일시스템 서버 - 파일 읽기/쓰기/편집
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem "C:\\"

# 2. GitHub 서버 - 리포지토리, 이슈, PR 관리  
claude mcp add github --scope user npx @modelcontextprotocol/server-github

# 3. 메모리 서버 - 대화 기록 및 컨텍스트 유지
claude mcp add memory --scope user npx @modelcontextprotocol/server-memory

# 4. 웹 페치 서버 - 웹 콘텐츠 가져오기 및 분석 (TypeScript 기반)
claude mcp add fetch-typescript --scope user npx mcp-server-fetch-typescript

# 5. 순차적 사고 서버 - 복잡한 작업을 단계별로 분해
claude mcp add sequential-thinking --scope user npx @modelcontextprotocol/server-sequential-thinking

# 6. Context7 서버 - 최신 라이브러리 문서 실시간 제공
claude mcp add context7 --scope user npx @upstash/context7-mcp

# 7. Magic 서버 - AI 기반 UI 컴포넌트 생성 (API 키 필요)
claude mcp add magic --scope user npx @21st-dev/magic

# 8. Notion 서버 - Notion 워크스페이스 통합 (API 키 필요)
claude mcp add notion --scope user npx @notionhq/notion-mcp-server

# 9. Figma 서버 - Figma 디자인 파일 데이터 추출 (API 키 필요)
claude mcp add figma --scope user npx mcp-figma
```

### 4단계: 설정 확인
```bash
# 설치된 MCP 서버 목록 확인
claude mcp list

# 다른 디렉토리에서도 작동하는지 테스트
cd C:\temp
claude mcp list

# 또는 macOS/Linux
cd /tmp  
claude mcp list
```

## 예상 결과 (모든 서버 연결 성공)
설정이 완료되면 다음과 같이 표시됩니다:
```
Checking MCP server health...

filesystem: npx @modelcontextprotocol/server-filesystem C:\ - ✓ Connected
github: npx @modelcontextprotocol/server-github - ✓ Connected
memory: npx @modelcontextprotocol/server-memory - ✓ Connected
sequential-thinking: npx @modelcontextprotocol/server-sequential-thinking - ✓ Connected
fetch-typescript: npx mcp-server-fetch-typescript - ✓ Connected
figma: npx mcp-figma - ✓ Connected
context7: npx @upstash/context7-mcp - ✓ Connected
magic: npx @21st-dev/magic - ✓ Connected
notion: npx @notionhq/notion-mcp-server - ✓ Connected
```

✅ **총 9개 서버 모두 연결 성공!**

### 추가 설정 (API 키가 필요한 서버들) ✅ **테스트 완료**

#### Magic 서버
```bash
# 1. https://21st.dev/magic/console에서 API 키 발급
# 2. 환경 변수 설정
export TWENTY_FIRST_API_KEY="your-api-key-here"  # Linux/macOS
set TWENTY_FIRST_API_KEY=your-api-key-here       # Windows
```

#### Notion 서버
```bash
# 1. https://www.notion.so/my-integrations에서 Integration 생성
# 2. "Internal Integration Token" 복사
# 3. 환경 변수 설정
export NOTION_API_KEY="secret_your-token-here"  # Linux/macOS
set NOTION_API_KEY=secret_your-token-here       # Windows
# 4. 워크스페이스 페이지에 Integration 연결
```

#### Figma 서버
```bash
# 1. Figma Settings > Personal Access Tokens에서 토큰 생성
# 2. 환경 변수 설정
export FIGMA_API_KEY="figd_your-token-here"  # Linux/macOS
set FIGMA_API_KEY=figd_your-token-here       # Windows

# 검증된 기능 (2025-08-11):
# - 서버 연결: 정상 (735ms)
# - Logo Search: GitHub 아이콘 JSX 생성 성공
# - API 통신: 21st.dev와 정상 연동
```

## 추가 서버 설치 (선택사항)

### 데이터베이스 서버
```bash
# PostgreSQL 서버 (데이터베이스가 있는 경우)
claude mcp add postgres --scope user npx @modelcontextprotocol/server-postgres "postgresql://username:password@localhost/database"

# SQLite 서버 (가벼운 데이터베이스)
claude mcp add sqlite --scope user npx @modelcontextprotocol/server-sqlite /path/to/database.db
```

### 검색 및 API 서버
```bash
# Brave 검색 서버 (API 키 필요)
claude mcp add brave-search --scope user npx @modelcontextprotocol/server-brave-search

# Slack 서버 (봇 토큰 필요)  
claude mcp add slack --scope user npx @modelcontextprotocol/server-slack
```

### 브라우저 자동화
```bash
# Puppeteer 브라우저 서버
claude mcp add puppeteer --scope user npx @modelcontextprotocol/server-puppeteer
```

## 환경 변수 파일 (.env) 사용법

이 프로젝트에는 `.env` 파일이 포함되어 있어 모든 API 키와 토큰을 안전하게 관리할 수 있습니다.

### .env 파일 설정
```bash
# .env 파일을 텍스트 에디터로 열어서 필요한 키들을 입력하세요:
GITHUB_PERSONAL_ACCESS_TOKEN=ghp_your_actual_token_here
TWENTY_FIRST_API_KEY=your_magic_api_key_here
FIGMA_API_KEY=your_figma_api_key_here
```

### Windows에서 .env 파일 로드
```bash
# 명령 프롬프트에서 환경 변수 로드
for /f "tokens=1,2 delims==" %i in (.env) do set %i=%j

# 또는 PowerShell에서
Get-Content .env | ForEach-Object { $name, $value = $_ -split '=', 2; [Environment]::SetEnvironmentVariable($name, $value) }
```

### Linux/macOS에서 .env 파일 로드
```bash
export $(cat .env | xargs)
```

### 보안 주의사항
- `.env` 파일은 `.gitignore`에 포함되어 Git에 업로드되지 않습니다
- 실제 토큰을 입력할 때 따옴표는 사용하지 마세요
- 토큰이 노출되지 않도록 주의하세요

## 유용한 관리 명령어

```bash
# 특정 서버 정보 보기
claude mcp get <서버이름>

# 서버 제거
claude mcp remove <서버이름>

# 모든 서버 상태 확인
claude mcp list

# Claude Code 실행하여 MCP 기능 테스트
claude
```

## 자동 설치 스크립트 사용

### Windows 사용자
```bash
# 이 저장소의 스크립트 다운로드 후 실행
quick-setup.bat
```

### macOS/Linux 사용자
```bash
# 이 저장소의 스크립트 다운로드 후 실행
chmod +x quick-setup.sh
./quick-setup.sh
```

## 문제 해결

### GitHub 서버가 연결되지 않을 때
```bash
# 환경 변수 확인
echo %GITHUB_PERSONAL_ACCESS_TOKEN%  # Windows
echo $GITHUB_PERSONAL_ACCESS_TOKEN   # macOS/Linux

# 새 터미널을 열어서 다시 시도
claude mcp list
```

### 서버가 실패할 때
```bash
# npx 캐시 정리
npx clear-npx-cache

# 특정 서버 재설치
claude mcp remove <서버이름>
claude mcp add <서버이름> --scope user npx @modelcontextprotocol/server-<서버이름>
```

### 권한 오류가 발생할 때
```bash
# npm 전역 권한 확인 (macOS/Linux)
sudo npm install -g @modelcontextprotocol/server-filesystem
sudo npm install -g @modelcontextprotocol/server-github
```

##  완료 후 할 수 있는 것들

 **파일 관리**: 모든 파일 읽기/쓰기/편집  
 **GitHub 작업**: 리포지토리 분석, 이슈 생성, PR 리뷰  
 **웹 스크래핑**: 웹사이트 콘텐츠 분석  
 **프로젝트 기억**: 대화 내용과 컨텍스트 유지  
 **복잡한 작업**: 단계별 분해하여 체계적 처리  
 **실시간 문서**: 최신 라이브러리 문서와 코드 예시 자동 제공  
 **UI 생성**: 자연어 설명만으로 모던한 UI 컴포넌트 즉시 생성  

---

 **팁**: 모든 명령어는 한 번만 실행하면 되고, 이후 모든 프로젝트에서 자동으로 사용할 수 있습니다!