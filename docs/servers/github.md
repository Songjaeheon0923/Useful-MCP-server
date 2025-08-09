# 🐙 GitHub MCP Server

**패키지**: `@modelcontextprotocol/server-github`  
**GitHub**: [Official GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)  
**상태**: ✅ **연결됨**  

## 개요

GitHub MCP Server는 Claude가 GitHub API와 완전히 통합할 수 있게 해주는 강력한 도구입니다. 리포지토리 관리부터 이슈 추적, 풀 리퀘스트 관리까지 GitHub의 모든 기능을 Claude를 통해 자동화할 수 있습니다.

## 설치 및 설정

### 1. MCP 서버 추가
```bash
claude mcp add github --scope user npx @modelcontextprotocol/server-github
```

### 2. GitHub Personal Access Token 설정

#### GitHub 토큰 생성
1. [GitHub Settings > Personal Access Tokens](https://github.com/settings/tokens) 이동
2. **"Generate new token (classic)"** 클릭
3. 필요한 권한 선택:
   - `repo`: 리포지토리 액세스
   - `user`: 사용자 정보 읽기
   - `workflow`: GitHub Actions 관리
   - `admin:org`: 조직 관리 (필요시)
4. 생성된 토큰 복사

#### 환경 변수 설정
```bash
# Windows에서 영구적으로 설정
setx GITHUB_PERSONAL_ACCESS_TOKEN "your-github-token-here"

# 현재 세션에서만 설정 (임시)
set GITHUB_PERSONAL_ACCESS_TOKEN=your-github-token-here

# 설정 확인
echo %GITHUB_PERSONAL_ACCESS_TOKEN%

# Linux/macOS
export GITHUB_PERSONAL_ACCESS_TOKEN="your-github-token-here"

# 영구 설정 (Linux/macOS)
echo 'export GITHUB_PERSONAL_ACCESS_TOKEN="your-github-token-here"' >> ~/.bashrc
source ~/.bashrc
```

### 3. 연결 확인
```bash
claude mcp list
# github: npx @modelcontextprotocol/server-github - ✓ Connected 확인
```

## 주요 기능

### 🏢 리포지토리 관리
- **리포지토리 CRUD**: 생성, 포크, 검색, 메타데이터 조회
- **파일 관리**: 단일/다중 파일 생성, 업데이트, 읽기
- **브랜치 관리**: 새 브랜치 생성, 전환, 커밋 히스토리 조회
- **콘텐츠 검색**: 코드, 이슈, PR, 사용자 검색

### 🎯 이슈 및 PR 관리
- **이슈 관리**: 생성, 업데이트, 댓글 추가, 라벨/마일스톤 설정
- **풀 리퀘스트**: 생성, 리뷰, 머지, 상태 확인
- **코드 리뷰**: 리뷰 작성, 댓글 추가, 승인/변경요청
- **자동화**: 상태 체크, CI/CD 트리거

## 사용 가능한 도구들

### 리포지토리 관리
- `create_repository`: 새 리포지토리 생성
- `search_repositories`: 리포지토리 검색
- `fork_repository`: 리포지토리 포크
- `get_file_contents`: 파일 내용 조회
- `create_or_update_file`: 파일 생성/업데이트
- `push_files`: 여러 파일 한 번에 커밋

### 이슈 관리
- `create_issue`: 새 이슈 생성
- `list_issues`: 이슈 목록 조회 (필터링 지원)
- `get_issue`: 특정 이슈 상세 조회
- `update_issue`: 이슈 업데이트
- `add_issue_comment`: 이슈에 댓글 추가

### 풀 리퀘스트
- `create_pull_request`: PR 생성
- `list_pull_requests`: PR 목록 조회
- `get_pull_request`: PR 상세 정보
- `get_pull_request_files`: PR 변경 파일 목록
- `create_pull_request_review`: PR 리뷰 작성
- `merge_pull_request`: PR 머지

### 검색 기능
- `search_code`: 코드 검색
- `search_issues`: 이슈/PR 검색
- `search_users`: 사용자 검색

### 브랜치 관리
- `create_branch`: 새 브랜치 생성
- `list_commits`: 커밋 히스토리 조회

## 사용 예시

### 기본 사용법
```bash
# Claude에서 사용 예시:
"이 리포지토리의 모든 열린 이슈를 우선순위별로 정렬해서 보여주세요"
"main 브랜치에서 feature/new-auth 브랜치를 생성해주세요"
"이 PR을 검토하고 코드 리뷰를 작성해주세요"
"최근 일주일간의 커밋을 분석해서 변경사항을 요약해주세요"
"버그 리포트 이슈를 생성하고 적절한 라벨을 추가해주세요"
"이 파일을 여러 브랜치에 동시에 업데이트해주세요"
```

### 고급 워크플로우
```bash
"릴리스 v2.0.0을 위한 체크리스트를 이슈로 생성하고 마일스톤을 설정해주세요"
"지난 달 가장 많이 기여한 개발자 5명을 분석해주세요"
"보안 취약점 관련 모든 이슈와 PR을 찾아서 상태를 확인해주세요"
"CI/CD 파이프라인 실패 횟수를 주간별로 분석해주세요"
```

## 자동화 워크플로우 예시

### 📊 프로젝트 관리 자동화
- **이슈 트리거 기반 자동 PR 생성**: 특정 라벨의 이슈 생성 시 관련 PR 자동 생성
- **릴리스 노트 자동 생성**: 마일스톤별 변경사항을 취합하여 릴리스 노트 작성
- **프로젝트 메트릭 수집**: 코드 기여도, 이슈 해결률, PR 머지율 등 정기 분석

### 🔍 코드 품질 관리
- **코드 리뷰 자동화**: PR 생성 시 자동 리뷰 및 피드백 제공
- **CI/CD 파이프라인 모니터링**: 빌드 실패 시 관련자 자동 알림
- **보안 스캔 결과 추적**: 보안 이슈 발견 시 자동 이슈 생성 및 담당자 할당

### 📈 팀 협업 개선
- **일일 스탠드업 리포트**: 전날 커밋, PR, 이슈 활동 요약
- **마일스톤 진행률 추적**: 마일스톤별 완료율 및 예상 완료일 계산
- **기술 부채 관리**: TODO, FIXME 주석 추적 및 이슈화

## 문제 해결

### 인증 실패
```bash
# 토큰 권한 확인
# GitHub에서 토큰의 권한(scope)이 올바른지 확인

# 환경 변수 재설정
setx GITHUB_PERSONAL_ACCESS_TOKEN "new-token-here"

# Claude CLI 재시작
```

### 연결 문제
```bash
# MCP 서버 상태 확인
claude mcp list

# 서버 재연결
claude mcp remove github
claude mcp add github --scope user npx @modelcontextprotocol/server-github
```

### 권한 오류
- 리포지토리 액세스가 거부될 경우 토큰 권한을 확인하세요
- 조직 리포지토리의 경우 조직 설정에서 Personal Access Token 사용을 허용해야 할 수 있습니다

## 참고 자료

- [GitHub API Documentation](https://docs.github.com/en/rest)
- [GitHub Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- [Official MCP GitHub Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)

---

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI