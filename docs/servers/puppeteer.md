# 🌐 Puppeteer MCP Server

**패키지**: `@hisma/server-puppeteer`  
**GitHub**: [Puppeteer MCP Server](https://github.com/hisma/server-puppeteer)  
**상태**: ✅ **연결됨**  

## 개요

Puppeteer MCP Server는 Claude가 브라우저를 완전히 제어할 수 있게 해주는 강력한 웹 자동화 도구입니다. 웹 스크래핑부터 자동화된 테스팅, 스크린샷 캡처까지 모든 브라우저 기반 작업을 Claude를 통해 수행할 수 있습니다.

## 설치 및 설정

### 1. MCP 서버 추가
```bash
claude mcp add puppeteer-server --scope user npx @hisma/server-puppeteer
```

### 2. 연결 확인
```bash
claude mcp list
# puppeteer-server: npx @hisma/server-puppeteer - ✓ Connected 확인
```

### 3. 추가 설정 (선택사항)
```bash
# 특정 Chrome 바이너리 사용
claude mcp add puppeteer-custom --scope user "npx @hisma/server-puppeteer --chrome-path=/path/to/chrome"

# 헤드풀 모드 (브라우저 UI 표시)
claude mcp add puppeteer-headful --scope user "npx @hisma/server-puppeteer --headful"
```

## 주요 기능

### 🔧 브라우저 제어
- **페이지 네비게이션**: URL로 이동, 뒤로/앞으로 이동, 새로고침
- **요소 상호작용**: 클릭, 텍스트 입력, 드롭다운 선택, 호버
- **스크린샷**: 전체 페이지 또는 특정 요소 캡처 (PNG/JPEG)
- **JavaScript 실행**: 브라우저 컨텍스트에서 커스텀 JS 코드 실행

### 📊 웹 스크래핑
- **DOM 요소 추출**: CSS 셀렉터로 텍스트, 속성, HTML 콘텐츠 추출
- **폼 자동화**: 로그인, 양식 작성, 제출 자동화
- **페이지 대기**: 특정 요소나 조건까지 대기
- **동적 콘텐츠**: JavaScript로 렌더링된 SPA 콘텐츠 스크래핑

### 🛠️ 고급 기능
- **헤드리스/헤드풀 모드**: UI 표시 여부 선택
- **모바일 에뮬레이션**: 다양한 디바이스 크기 시뮬레이션
- **네트워크 제어**: 요청 인터셉트, 응답 모킹
- **PDF 생성**: 웹 페이지를 PDF로 변환

## 사용 가능한 도구들

### 기본 네비게이션
- **`puppeteer_navigate`**: 지정된 URL로 이동
- **`puppeteer_screenshot`**: 페이지 또는 요소 스크린샷 캡처
- **`puppeteer_evaluate`**: 브라우저에서 JavaScript 코드 실행

### 요소 상호작용
- **`puppeteer_click`**: CSS 셀렉터로 요소 클릭
- **`puppeteer_fill`**: 입력 필드에 텍스트 입력
- **`puppeteer_select`**: 드롭다운에서 값 선택
- **`puppeteer_hover`**: 요소에 마우스 호버

### 콘텐츠 추출
- **`puppeteer_get_content`**: 페이지의 HTML 콘텐츠 가져오기
- **`puppeteer_wait_for_selector`**: 특정 요소가 나타날 때까지 대기

### 고급 기능
- **`puppeteer_pdf_generate`**: 페이지를 PDF로 변환
- **`puppeteer_emulate_device`**: 모바일 디바이스 에뮬레이션
- **`puppeteer_set_viewport`**: 뷰포트 크기 설정

## 사용 예시

### 기본 브라우저 작업
```bash
# Claude에서 사용 예시:
"네이버 메인페이지를 스크린샷으로 캡처해주세요"
"구글에서 'Claude AI'를 검색하고 결과를 캡처해주세요"
"이 웹사이트의 로그인 폼을 자동으로 채워주세요"
"이 페이지를 PDF로 변환해주세요"
"동적으로 로드되는 콘텐츠를 기다린 후 스크래핑해주세요"
```

### 웹 스크래핑
```bash
"이 사이트에서 제품 정보를 스크래핑해서 정리해주세요: https://example-shop.com"
"뉴스 사이트에서 최신 헤드라인 10개를 추출해주세요"
"이 부동산 사이트에서 매물 정보와 가격을 수집해주세요"
"소셜 미디어에서 특정 해시태그의 최근 게시물을 가져와주세요"
```

### 자동화 테스트
```bash
"이 웹 애플리케이션의 회원가입 프로세스를 자동으로 테스트해주세요"
"체크아웃 프로세스가 정상적으로 작동하는지 확인해주세요"
"다양한 화면 크기에서 레이아웃이 올바르게 표시되는지 테스트해주세요"
"폼 유효성 검증이 제대로 작동하는지 확인해주세요"
```

### 모니터링 및 분석
```bash
"경쟁사 웹사이트의 변경사항을 정기적으로 모니터링해주세요"
"웹사이트 로딩 속도를 측정하고 성능 리포트를 만들어주세요"
"광고 배너가 올바른 위치에 표시되는지 확인해주세요"
"웹사이트의 접근성을 자동으로 테스트해주세요"
```

## 자동화 워크플로우 예시

### 📊 데이터 수집 자동화
- **가격 모니터링**: E-commerce 사이트의 가격 변동 추적
- **경쟁사 분석**: 경쟁사 웹사이트의 컨텐츠 및 기능 변화 모니터링
- **소셜 미디어 분석**: 브랜드 멘션, 해시태그 트렌드 수집
- **뉴스 수집**: 특정 키워드 관련 뉴스 자동 수집 및 분류

### 🧪 자동화된 테스팅
- **회귀 테스트**: 새로운 배포 후 핵심 기능 자동 검증
- **크로스 브라우저 테스트**: 다양한 브라우저에서 일관성 확인
- **성능 테스트**: 페이지 로딩 시간, 렌더링 성능 측정
- **접근성 테스트**: WCAG 가이드라인 준수 여부 자동 검증

### 📈 비즈니스 인텔리전스
- **시장 조사**: 업계 동향, 가격 정보 자동 수집
- **고객 행동 분석**: 웹사이트 사용 패턴 분석
- **SEO 모니터링**: 검색 엔진 순위 변화 추적
- **컨텐츠 감시**: 브랜드 언급, 리뷰 모니터링

### 🔄 운영 자동화
- **정기 백업**: 웹 컨텐츠 자동 백업 및 아카이브
- **상태 확인**: 웹사이트 다운타임 모니터링
- **보안 감시**: 웹사이트 변조나 악성 코드 탐지
- **업데이트 알림**: 중요 페이지 변경사항 자동 알림

## 고급 사용법

### 복잡한 사용자 시나리오
```bash
# 다단계 사용자 플로우
"회원가입 → 로그인 → 상품 구매 → 리뷰 작성까지의 전체 플로우를 자동화해주세요"

# 조건부 액션
"만약 재고가 있으면 구매하고, 없으면 알림 신청을 해주세요"
```

### 데이터 처리 및 분석
```bash
# 대량 데이터 처리
"100페이지에 걸친 검색 결과를 모두 수집해서 CSV로 저장해주세요"

# 실시간 모니터링
"주식 가격을 1분마다 확인해서 특정 조건에서 알림을 보내주세요"
```

### 고급 브라우저 제어
```bash
# 네트워크 조작
"특정 API 호출을 인터셉트해서 응답을 수정하고 테스트해주세요"

# 성능 프로파일링
"페이지 로딩 과정을 상세히 분석해서 병목점을 찾아주세요"
```

## CSS 선택자 활용

### 기본 선택자
```css
/* ID 선택자 */
#login-button

/* 클래스 선택자 */
.product-card

/* 속성 선택자 */
[data-testid="submit-button"]

/* 복합 선택자 */
.navbar .menu-item:nth-child(2)
```

### 고급 선택자
```css
/* 텍스트 포함 */
:contains("로그인")

/* 가상 선택자 */
input:not([disabled])

/* 구조 선택자 */
table tr:nth-of-type(even)
```

## 성능 최적화

### 브라우저 설정
```javascript
// 헤드리스 모드 (기본값)
// 더 빠른 실행 속도

// 이미지 로딩 비활성화
// 대역폭 절약 및 속도 향상

// 캐시 활용
// 반복 요청 시 속도 개선
```

### 대기 전략
```bash
# 명시적 대기 (권장)
"특정 요소가 나타날 때까지 기다린 후 액션을 수행해주세요"

# 네트워크 대기
"모든 네트워크 요청이 완료될 때까지 기다려주세요"
```

## 보안 고려사항

### 민감 정보 처리
- 로그인 정보는 환경 변수나 보안 저장소 사용
- 스크린샷에서 민감 정보 자동 마스킹
- 세션 정보 자동 정리

### 사이트 정책 준수
- robots.txt 확인 및 준수
- 요청 빈도 제한 (Rate limiting)
- 사이트 이용약관 검토

### 법적 고려사항
- 저작권 보호 컨텐츠 처리 주의
- 개인정보 수집 시 관련 법규 준수
- 웹 스크래핑 관련 현지 법률 확인

## 문제 해결

### 브라우저 실행 오류
```bash
# Chrome/Chromium 설치 확인
# Windows: Chrome 자동 다운로드
# Linux: apt-get install chromium-browser
# macOS: brew install chromium

# 권한 문제 (Linux)
# --no-sandbox 옵션 추가 고려
```

### 요소 찾기 실패
```bash
# 대기 시간 증가
"페이지 로딩을 충분히 기다린 후 요소를 찾아주세요"

# 선택자 검증
# 브라우저 개발자 도구에서 선택자 테스트
```

### 메모리 누수
```bash
# 페이지 정리
"작업 완료 후 브라우저 탭을 정리해주세요"

# 세션 관리
"장시간 실행 시 주기적으로 브라우저를 재시작해주세요"
```

## 모니터링 및 로깅

### 실행 과정 추적
- 각 단계별 스크린샷 자동 저장
- 네트워크 요청/응답 로그 기록
- 오류 발생 시 상세 컨텍스트 저장

### 성능 메트릭
- 페이지 로딩 시간 측정
- JavaScript 실행 시간 추적
- 메모리 사용량 모니터링

## 참고 자료

- [Puppeteer Official Documentation](https://pptr.dev/)
- [CSS Selectors Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [Web Scraping Best Practices](https://blog.apify.com/web-scraping-best-practices/)
- [Puppeteer MCP Server](https://github.com/hisma/server-puppeteer)

---

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI