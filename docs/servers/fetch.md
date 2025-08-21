# 🌐 Fetch MCP Server (TypeScript)

**패키지**: `mcp-server-fetch-typescript`  
**GitHub**: [MCP Server Fetch TypeScript](https://github.com/tatn/mcp-server-fetch-typescript)  
**상태**: ✅ **연결됨**  

## 개요

Fetch MCP Server는 Claude가 웹 콘텐츠를 가져오고 처리할 수 있게 해주는 강력한 도구입니다. Playwright 기반으로 동적 웹사이트도 처리할 수 있으며, HTML을 읽기 쉬운 Markdown으로 변환하여 Claude가 분석할 수 있게 합니다.

## 설치 및 설정

### 1. MCP 서버 추가
```bash
claude mcp add fetch-typescript --scope user npx mcp-server-fetch-typescript
```

### 2. 연결 확인
```bash
claude mcp list
# fetch-typescript: npx mcp-server-fetch-typescript - ✓ Connected 확인
```

## 주요 기능

### 🌐 웹 콘텐츠 가져오기
- **정적 페이지**: HTML, CSS, JavaScript로 구성된 일반 웹사이트
- **동적 페이지**: SPA, React, Vue 등 JavaScript로 렌더링되는 페이지
- **API 응답**: JSON, XML 등 API 엔드포인트 데이터
- **이미지 및 미디어**: 웹상의 이미지, 비디오 메타데이터

### 📝 콘텐츠 변환 및 처리
- **HTML → Markdown**: 웹 페이지를 읽기 쉬운 Markdown으로 변환
- **텍스트 추출**: 불필요한 태그 제거하고 핵심 내용만 추출
- **구조화된 데이터**: 제목, 링크, 이미지 등을 체계적으로 정리
- **메타데이터 추출**: 페이지 제목, 설명, 키워드 등 메타 정보

### 🚀 고급 브라우저 기능
- **JavaScript 실행**: 동적으로 로드되는 콘텐츠 처리
- **사용자 에이전트 설정**: 다양한 디바이스/브라우저로 페이지 접근
- **쿠키 및 세션**: 로그인이 필요한 페이지 접근 (제한적)
- **스크린샷**: 페이지의 시각적 스냅샷 생성

## 사용 가능한 도구들

### 웹 페이지 가져오기
- `fetch_url`: 지정된 URL의 콘텐츠를 가져와서 Markdown으로 변환
- `fetch_multiple_urls`: 여러 URL을 동시에 처리
- `extract_text`: 웹 페이지에서 텍스트만 추출

### 콘텐츠 분석
- `analyze_page_structure`: 페이지의 구조와 주요 요소 분석
- `extract_links`: 페이지 내 모든 링크 추출 및 분류
- `get_page_metadata`: 메타 태그, 제목, 설명 등 페이지 정보

### 검색 및 크롤링
- `search_in_page`: 페이지 내 특정 텍스트나 패턴 검색
- `follow_sitemap`: 사이트맵을 따라 페이지들을 체계적으로 크롤링
- `crawl_website`: 웹사이트의 여러 페이지를 순차적으로 방문

## 사용 예시

### 기본 사용법
```bash
# Claude에서 사용 예시:
"https://example.com 페이지의 내용을 가져와서 요약해주세요"
"이 뉴스 사이트의 최신 기사들을 분석해주세요"
"GitHub 저장소의 README 파일을 가져와서 주요 기능을 정리해주세요"
"이 API 문서 페이지를 읽고 사용법을 설명해주세요"
"Stack Overflow의 이 질문과 답변들을 정리해주세요"
```

### 고급 활용
```bash
"여러 경쟁사 웹사이트를 분석해서 기능 비교표를 만들어주세요"
"이 온라인 강의 사이트의 커리큘럼을 정리해주세요"
"기술 블로그의 최신 포스트들을 수집해서 트렌드를 분석해주세요"
"제품 리뷰 사이트에서 평점과 주요 의견들을 수집해주세요"
```

## 자동화 워크플로우 예시

### 📰 뉴스 및 콘텐츠 모니터링
- **일일 뉴스 요약**: 지정된 뉴스 사이트들의 헤드라인 수집 및 요약
- **경쟁사 분석**: 경쟁업체 웹사이트의 제품 업데이트나 블로그 포스트 모니터링
- **기술 트렌드 추적**: 기술 블로그, 문서 사이트의 새로운 내용 추적

### 🔍 리서치 및 데이터 수집
- **시장 조사**: 여러 웹사이트에서 가격 정보, 제품 스펙 수집
- **학술 자료 수집**: 논문 사이트나 연구 기관 웹사이트에서 최신 연구 동향 파악
- **법률/규정 모니터링**: 정부 사이트나 규제 기관의 새로운 공지사항 추적

### 📊 비즈니스 인텔리전스
- **고객 리뷰 분석**: 리뷰 사이트에서 제품 평가 및 피드백 수집
- **소셜 미디어 모니터링**: 브랜드 언급이나 고객 의견 추적
- **채용 정보 수집**: 구인 사이트에서 업계 동향 및 스킬 트렌드 분석

## 보안 및 윤리적 고려사항

### 🔒 보안 주의사항
- **개인정보 보호**: 로그인이 필요한 사이트나 개인 정보가 포함된 페이지 접근 주의
- **API 키 보호**: 인증이 필요한 API 접근 시 키 노출 방지
- **쿠키 관리**: 세션 쿠키나 인증 토큰이 로그에 남지 않도록 주의

### ⚖️ 윤리적 사용
- **robots.txt 준수**: 웹사이트의 크롤링 정책 확인 및 준수
- **요청 빈도 제한**: 서버에 과부하를 주지 않도록 적절한 간격으로 요청
- **저작권 존중**: 가져온 콘텐츠의 저작권 및 이용 약관 확인
- **서비스 약관 준수**: 대상 웹사이트의 서비스 이용 약관 검토

## 문제 해결

### 연결 실패
```bash
# 패키지 설치 확인
npx mcp-server-fetch-typescript --help

# MCP 서버 재연결
claude mcp remove fetch-typescript
claude mcp add fetch-typescript --scope user npx mcp-server-fetch-typescript
```

### 페이지 로딩 실패
- **JavaScript 필요 페이지**: 동적 페이지의 경우 로딩 시간을 늘려서 재시도
- **차단된 요청**: User-Agent나 요청 헤더를 조정해서 차단 우회
- **네트워크 오류**: 인터넷 연결 상태 및 방화벽 설정 확인

### 성능 최적화
- **대용량 페이지**: 필요한 부분만 추출하도록 셀렉터 사용
- **다중 요청**: 동시 요청 수를 제한해서 서버 부하 방지
- **캐싱 활용**: 자주 접근하는 페이지는 캐시 활용

## 지원되는 형식

### 웹 콘텐츠 유형
- **HTML 페이지**: 일반적인 웹사이트, 블로그, 뉴스 사이트
- **SPA 애플리케이션**: React, Vue, Angular 등으로 만든 싱글 페이지 앱
- **API 엔드포인트**: REST API, GraphQL 등의 데이터 API
- **문서 사이트**: Gitbook, Confluence, Notion 등의 문서 플랫폼

### 출력 형식
- **Markdown**: 구조화된 텍스트 형태로 변환
- **Plain Text**: 순수 텍스트만 추출
- **JSON**: 구조화된 데이터로 파싱
- **HTML**: 원본 HTML 유지 (필요시)

## 참고 자료

- [Playwright Documentation](https://playwright.dev/)
- [HTML to Markdown Conversion](https://github.com/remarkjs/remark)
- [Web Scraping Best Practices](https://blog.apify.com/web-scraping-best-practices/)
- [MCP Server Fetch TypeScript](https://www.npmjs.com/package/mcp-server-fetch-typescript)

---

**마지막 업데이트**: 2025-08-21  
**테스트 환경**: Windows, Claude CLI  
**검증 상태**: ✅ 웹 콘텐츠 가져오기 및 Markdown 변환 테스트 완료