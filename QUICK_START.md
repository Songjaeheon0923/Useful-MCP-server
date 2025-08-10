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
```bash
# Windows (PowerShell/CMD)
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-github-token-here"

# macOS/Linux
export GITHUB_PERSONAL_ACCESS_TOKEN="your-github-token-here"
echo 'export GITHUB_PERSONAL_ACCESS_TOKEN="your-github-token-here"' >> ~/.bashrc
```

### 3단계: MCP 서버 설치 (User Scope - 모든 프로젝트에서 사용)
```bash
# 1. 파일시스템 서버 - 파일 읽기/쓰기/편집
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem C:\

# 2. GitHub 서버 - 리포지토리, 이슈, PR 관리  
claude mcp add github --scope user npx @modelcontextprotocol/server-github

# 3. 메모리 서버 - 대화 기록 및 컨텍스트 유지
claude mcp add memory --scope user npx @modelcontextprotocol/server-memory

# 4. 웹 페치 서버 - 웹 콘텐츠 가져오기 및 분석
claude mcp add fetch --scope user npx @modelcontextprotocol/server-fetch

# 5. 순차적 사고 서버 - 복잡한 작업을 단계별로 분해
claude mcp add sequential-thinking --scope user npx @modelcontextprotocol/server-sequential-thinking

# 6. Context7 서버 - 최신 라이브러리 문서 실시간 제공
npm install -g @upstash/context7-mcp
claude mcp add context7 --scope user context7-mcp

# 7. Magic 서버 - AI 기반 UI 컴포넌트 생성 (API 키 필요)
npm install -g @21st-dev/magic
claude mcp add magic --scope user magic

# 8. Notion 서버 - Notion 워크스페이스 통합 (즉시 사용 가능)
claude mcp add notion --scope user https://mcp.notion.com/mcp
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

## 예상 결과
설정이 완료되면 다음과 같이 표시됩니다:
```
Checking MCP server health...

filesystem: npx @modelcontextprotocol/server-filesystem C:\ - ✓ Connected
github: npx @modelcontextprotocol/server-github - ✓ Connected  
memory: npx @modelcontextprotocol/server-memory - ✓ Connected
fetch: npx @modelcontextprotocol/server-fetch - ✓ Connected
sequential-thinking: npx @modelcontextprotocol/server-sequential-thinking - ✓ Connected
context7: context7-mcp - ✓ Connected
magic: magic - ✓ Connected
notion: https://mcp.notion.com/mcp (HTTP) - ✓ Connected
```

### 추가 설정 (Magic 서버)
Magic 서버를 사용하려면 API 키가 필요합니다:
```bash
# 1. https://21st.dev/magic/console에서 API 키 발급
# 2. 환경 변수 설정
export TWENTY_FIRST_API_KEY="your-api-key-here"  # Linux/macOS
set TWENTY_FIRST_API_KEY=your-api-key-here       # Windows
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