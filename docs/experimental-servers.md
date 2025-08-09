# 🔄 실험적 및 미구현 MCP 서버들

이 문서는 아직 테스트되지 않았거나 구현 중인 MCP 서버들을 정리합니다. 이들 서버는 잠재적으로 유용하지만 안정성이나 가용성이 확인되지 않았습니다.

## ⚠️ 주의사항

- **실험적 상태**: 이 서버들은 완전히 테스트되지 않았습니다
- **호환성 미확인**: 현재 환경에서 정상 작동하지 않을 수 있습니다
- **문서 부족**: 일부 서버는 문서가 불완전할 수 있습니다
- **유지보수 상태 불명**: 개발자 지원이나 업데이트가 불확실합니다

## 개발 도구

### 🗄️ PostgreSQL/Database Server
- **패키지**: `@modelcontextprotocol/server-postgres`
- **상태**: ⚠️ **테스트 필요**
- **GitHub**: [PostgreSQL MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres)

#### 예상 기능:
- PostgreSQL, MySQL, BigQuery 등 다중 데이터베이스 지원
- SQL 쿼리 실행 및 결과 분석
- 데이터베이스 스키마 관리
- 데이터 마이그레이션 및 백업

#### 설치 시도:
```bash
# 시도해볼 수 있는 명령어 (미확인)
claude mcp add postgres --scope user npx @modelcontextprotocol/server-postgres
```

### 🌐 Fetch Server
- **패키지**: `@modelcontextprotocol/server-fetch`
- **상태**: ❌ **패키지 미존재**
- **대안**: 내장 WebFetch 도구 사용 권장

#### 참고사항:
- 해당 패키지가 npm에서 찾을 수 없음
- Claude Code의 내장 WebFetch 도구로 동일한 기능 제공
- 별도 설치 불필요

### 🧪 Browser MCP (대안)
- **패키지**: `browser-mcp`
- **상태**: ⚠️ **테스트 필요**
- **GitHub**: [Browser MCP](https://github.com/adhikasp/browser-mcp)

#### 예상 기능:
- Puppeteer 대안 브라우저 자동화
- 경량화된 브라우저 제어
- 기본적인 스크래핑 기능

#### 설치 시도:
```bash
# 시도해볼 수 있는 명령어 (미확인)
claude mcp add browser-mcp --scope user npx browser-mcp
```

## 데이터베이스 & API

### 📊 Apidog MCP Server
- **상태**: ⚠️ **테스트 필요**
- **예상 기능**: API 문서화, 테스팅, 코드 생성

#### 참고사항:
- 정확한 패키지명 미확인
- API 개발 워크플로우 통합 도구로 추정
- 공식 문서나 GitHub 저장소 찾기 어려움

## AI 및 자동화

### 🧘 Zen MCP Server
- **상태**: ⚠️ **테스트 필요**
- **GitHub**: [Zen MCP Server](https://github.com/BeehiveInnovations/zen-mcp-server)

#### 예상 기능:
- 여러 AI 모델을 개발팀으로 조직화
- Claude가 각 작업에 최적의 모델 선택
- Gemini, OpenAI, Grok, OpenRouter, Ollama, 커스텀 모델 지원

#### 설치 시도:
```bash
# GitHub 저장소 기반 설치 시도
claude mcp add zen --scope user "npx zen-mcp-server"
```

### 🔍 AgentOps
- **상태**: ⚠️ **테스트 필요**
- **예상 기능**: AI 에이전트 디버깅을 위한 관찰성 및 추적

#### 참고사항:
- 패키지명이나 설치 방법 미확인
- AI 에이전트 모니터링 및 분석 도구로 추정

## 클라우드 서비스 통합

### ☁️ Alibaba Cloud MCP 서버들
- **상태**: ⚠️ **테스트 필요**

#### 포함된 서비스들:
- **AnalyticDB for MySQL**: 분석용 MySQL 데이터베이스
- **AnalyticDB for PostgreSQL**: 분석용 PostgreSQL 데이터베이스  
- **DataWorks**: 데이터 통합 및 개발 플랫폼
- **OpenSearch**: 검색 및 분석 엔진
- **Cloud OPS**: 클라우드 운영 관리
- **RDS**: 관계형 데이터베이스 서비스

#### 참고사항:
- 각 서비스별로 별도 MCP 서버가 있을 것으로 추정
- Alibaba Cloud 계정 및 API 키 필요
- 중국 클라우드 서비스로 지역 제한이 있을 수 있음

## 실험 가이드

### 새로운 MCP 서버 테스트 방법

#### 1단계: 기본 정보 수집
```bash
# npm에서 패키지 검색
npm search [패키지명]

# GitHub에서 저장소 확인
# 문서, 예제, 이슈 등 확인
```

#### 2단계: 안전한 환경에서 테스트
```bash
# 로컬 범위로 먼저 테스트
claude mcp add test-server [패키지명] [옵션]

# 연결 상태 확인
claude mcp list

# 기본 기능 테스트
# Claude에서 간단한 작업 요청
```

#### 3단계: 문제 해결
```bash
# 연결 실패 시 로그 확인
claude mcp get test-server

# 서버 제거
claude mcp remove test-server

# 다른 설치 방법 시도
```

#### 4단계: 성공 시 문서화
- 설치 명령어 기록
- 사용 가능한 도구들 정리
- 예제 사용법 작성
- 주의사항 및 제한사항 기록

### 문제 해결 팁

#### 패키지 찾기 어려울 때:
```bash
# GitHub에서 검색
# "mcp server [기능명]" 또는 "[서비스명] mcp"

# npm 레지스트리에서 검색
# 패키지명이 다를 수 있음

# 커뮤니티 리스트 확인
# awesome-mcp-servers 저장소들 참고
```

#### 설치 실패 시:
```bash
# 직접 패키지 설치 시도
npm install -g [패키지명]

# 시스템 요구사항 확인
# Node.js 버전, 운영체제 호환성

# 대안 패키지 검색
# 유사한 기능을 제공하는 다른 MCP 서버
```

## 기여 가이드

### 성공적으로 테스트한 서버가 있다면:

1. **문서 작성**: 상세한 설치 및 사용 가이드 작성
2. **예제 제공**: 실제 사용 예시 및 코드 스니펫
3. **이슈 리포트**: 발견한 문제점이나 제한사항 기록
4. **메인 README 업데이트**: 검증된 서버 목록에 추가

### 새로운 서버를 발견했다면:

1. **기본 정보 수집**: 패키지명, GitHub 링크, 기능 설명
2. **이 문서에 추가**: 실험적 서버 목록에 추가
3. **테스트 계획 수립**: 체계적인 테스트 방법 설계
4. **커뮤니티 공유**: 다른 사용자들과 정보 공유

## 참고 자료

### 커뮤니티 리스트
- [Awesome MCP Servers (wong2)](https://github.com/wong2/awesome-mcp-servers)
- [Awesome MCP Servers (punkpeye)](https://github.com/punkpeye/awesome-mcp-servers)
- [Official MCP Servers](https://github.com/modelcontextprotocol/servers)

### 개발 리소스
- [MCP Specification](https://github.com/modelcontextprotocol/specification)
- [Creating MCP Servers](https://docs.anthropic.com/en/docs/claude-code/mcp)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)

### 검색 키워드
- "mcp server"
- "model context protocol"
- "claude mcp"
- "[서비스명] mcp server"
- "anthropic mcp"

---

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI  

⚠️ **면책조항**: 이 문서의 정보는 추정에 기반하며, 실제 동작이나 가용성을 보장하지 않습니다. 실험 시 주의하시고, 중요한 시스템에서는 사전에 충분한 테스트를 수행하시기 바랍니다.