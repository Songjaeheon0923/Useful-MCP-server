# 🔄 실험적 및 미구현 MCP 서버들

이 문서는 아직 테스트되지 않았거나 구현 중인 MCP 서버들을 정리. 이들 서버는 잠재적으로 유용하지만 안정성이나 가용성이 확인되지 않았다.

## 개발 도구

### 🗄️ PostgreSQL/Database Server
- **패키지**: `@modelcontextprotocol/server-postgres`
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

#### 참고사항:
- 해당 패키지가 npm에서 찾을 수 없음
- Claude Code의 내장 WebFetch 도구로 동일한 기능 제공
- 별도 설치 불필요

### 🧪 Browser MCP 
- **패키지**: `browser-mcp`
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
- **예상 기능**: API 문서화, 테스팅, 코드 생성

#### 참고사항:
- 정확한 패키지명 미확인
- API 개발 워크플로우 통합 도구로 추정
- 공식 문서나 GitHub 저장소 찾기 어려움

## AI 및 자동화

### 🧘 Zen MCP Server
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
- **예상 기능**: AI 에이전트 디버깅을 위한 관찰성 및 추적

#### 참고사항:
- 패키지명이나 설치 방법 미확인
- AI 에이전트 모니터링 및 분석 도구로 추정

## 클라우드 서비스 통합

### ☁️ Alibaba Cloud MCP 서버들

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


## 참고 자료

### 커뮤니티 리스트
- [Awesome MCP Servers (wong2)](https://github.com/wong2/awesome-mcp-servers)
- [Awesome MCP Servers (punkpeye)](https://github.com/punkpeye/awesome-mcp-servers)
- [Official MCP Servers](https://github.com/modelcontextprotocol/servers)

### 개발 리소스
- [MCP Specification](https://github.com/modelcontextprotocol/specification)
- [Creating MCP Servers](https://docs.anthropic.com/en/docs/claude-code/mcp)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)


---

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI  
