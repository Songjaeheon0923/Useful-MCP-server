# 📚 Context7 MCP Server

**패키지**: `@upstash/context7-mcp`  
**GitHub**: [Context7 MCP Server](https://github.com/upstash/context7)  
**상태**: ✅ **연결됨**  

## 개요

Context7 MCP Server는 Claude가 최신 버전별 문서와 코드 예시를 실시간으로 가져올 수 있게 해주는 혁신적인 문서 서비스입니다. 프롬프트에 직접 최신 라이브러리 문서를 삽입하여 항상 정확하고 최신의 개발 정보를 제공합니다.

## 설치 및 설정

### 1. 전역 설치 (권장)
```bash
# npm으로 전역 설치
npm install -g @upstash/context7-mcp

# MCP 서버 추가
claude mcp add context7 --scope user context7-mcp
```

### 2. NPX 사용 (대안)
```bash
# NPX로 직접 사용
claude mcp add context7 --scope user "npx @upstash/context7-mcp"
```

### 3. 연결 확인
```bash
claude mcp list
# context7: context7-mcp - ✓ Connected 확인
```

## 주요 기능

### 📖 실시간 문서 제공
- **최신 문서**: 항상 최신 버전의 라이브러리 문서 제공
- **버전별 문서**: 특정 버전에 맞는 정확한 API 문서
- **코드 예시**: 실제 사용 가능한 코드 스니펫 포함
- **API 참조**: 완전한 API 레퍼런스 및 매개변수 정보

### 🚀 자동 라이브러리 감지
- **스마트 매칭**: 프롬프트에서 언급된 라이브러리 자동 감지
- **컨텍스트 분석**: 코드 컨텍스트를 기반으로 관련 문서 추천
- **다중 라이브러리**: 여러 라이브러리를 동시에 처리
- **언어별 지원**: 다양한 프로그래밍 언어 및 프레임워크

### 🎯 정확성 보장
- **출처 검증**: 공식 문서에서만 정보 추출
- **버전 일치**: 사용 중인 버전과 정확히 일치하는 문서 제공
- **실시간 업데이트**: 문서 변경사항 즉시 반영
- **품질 보증**: 검증된 고품질 문서만 선별

## 지원되는 라이브러리

### 🔧 웹 프레임워크
- **React**: 컴포넌트, 훅, 라이프사이클
- **Vue.js**: 컴포지션 API, 디렉티브, 라우터
- **Angular**: 컴포넌트, 서비스, 의존성 주입
- **Svelte**: 반응성, 스토어, 라우팅

### ⚡ 백엔드 프레임워크
- **Express.js**: 미들웨어, 라우팅, 인증
- **FastAPI**: 타입 힌트, 의존성 주입, 자동 문서화
- **Django**: 모델, 뷰, 템플릿, ORM
- **Spring Boot**: 애노테이션, 자동 구성, 액추에이터

### 📦 유틸리티 라이브러리
- **Lodash**: 배열, 객체, 함수 조작
- **Axios**: HTTP 클라이언트, 인터셉터
- **Moment.js/Day.js**: 날짜 시간 처리
- **UUID**: 고유 식별자 생성

### 🗄️ 데이터베이스 및 ORM
- **Prisma**: 스키마, 쿼리, 마이그레이션
- **TypeORM**: 엔티티, 관계, 데코레이터
- **Mongoose**: 스키마, 모델, 미들웨어
- **Sequelize**: 모델, 연관관계, 트랜잭션

### 🎨 UI 라이브러리
- **Material-UI**: 컴포넌트, 테마, 스타일링
- **Ant Design**: 디자인 시스템, 폼 컴포넌트
- **Chakra UI**: 심플한 모듈형 접근성
- **Bootstrap**: 그리드, 컴포넌트, 유틸리티

## 사용 방법

### 기본 사용법
```bash
# Claude에서 자연스럽게 사용
"React의 useState 훅을 사용해서 카운터 컴포넌트를 만들어주세요"
"FastAPI에서 JWT 인증을 구현하는 방법을 알려주세요"
"Prisma ORM으로 사용자 모델을 정의하는 코드를 작성해주세요"
"Material-UI의 DataGrid 컴포넌트 사용법을 보여주세요"
```

### 명시적 사용
```bash
# "use context7" 키워드로 명시적 활성화
"use context7로 React Router v6의 네이비게이션 방법을 알려주세요"
"use context7: Express.js에서 미들웨어를 작성하는 모범 사례"
```

### 특정 버전 지정
```bash
# 버전을 명시하여 정확한 문서 요청
"React 18.2 버전의 새로운 기능들을 context7로 조회해주세요"
"Vue 3.3에서 추가된 컴포지션 API 기능을 설명해주세요"
```

## 사용 예시

### React 개발
```bash
"React 함수형 컴포넌트에서 상태 관리하는 방법을 context7로 알려주세요"
"useEffect 훅의 의존성 배열 사용법과 주의사항을 설명해주세요"
"React Query로 서버 상태를 관리하는 패턴을 보여주세요"
"React.memo와 useMemo의 차이점과 적절한 사용 시점을 알려주세요"
```

### 백엔드 개발
```bash
"FastAPI에서 비동기 데이터베이스 연결을 설정하는 방법"
"Express.js의 에러 핸들링 미들웨어 작성법"
"Django REST Framework의 시리얼라이저 사용법"
"Spring Boot의 JPA Repository 사용 예시"
```

### 데이터베이스
```bash
"Prisma에서 복잡한 관계 쿼리 작성하는 방법"
"MongoDB와 Mongoose를 사용한 스키마 설계"
"TypeORM에서 트랜잭션 처리하는 패턴"
"Redis를 활용한 세션 관리 구현"
```

### 프론트엔드 UI
```bash
"Material-UI의 테마 커스터마이징 방법"
"Ant Design의 Form 컴포넌트 유효성 검사"
"Chakra UI로 반응형 레이아웃 구성"
"Tailwind CSS의 유틸리티 클래스 활용법"
```

## 자동화 워크플로우 예시

### 📝 코드 작성 지원
- **API 구현**: 라이브러리 문서를 참조한 정확한 API 구현
- **컴포넌트 개발**: 최신 패턴과 모범 사례를 적용한 컴포넌트 작성
- **설정 파일**: 프레임워크별 올바른 설정 파일 생성
- **테스트 코드**: 라이브러리별 테스트 패턴 적용

### 🔧 문제 해결
- **에러 디버깅**: 특정 라이브러리 에러의 원인과 해결책
- **마이그레이션**: 버전 업그레이드 시 변경사항 안내
- **호환성**: 라이브러리 간 호환성 이슈 해결
- **성능 최적화**: 라이브러리별 성능 향상 기법

### 📚 학습 지원
- **튜토리얼**: 단계별 학습 가이드 제공
- **예제 코드**: 실제 동작하는 예제 생성
- **모범 사례**: 업계 표준 패턴 학습
- **트렌드 파악**: 최신 개발 트렌드 이해

### 🚀 프로젝트 초기화
- **보일러플레이트**: 프로젝트 구조 및 초기 설정
- **의존성 관리**: 필요한 패키지와 버전 추천
- **환경 설정**: 개발 환경 구성 가이드
- **배포 준비**: 프로덕션 배포를 위한 설정

## 고급 사용법

### 컨텍스트 ID 활용
```bash
# 라이브러리의 Context7 ID를 사용하여 직접 지정
"react:18.2로 새로운 서버 컴포넌트 패턴을 설명해주세요"
"nextjs:13으로 앱 라우터 사용법을 보여주세요"
```

### 다중 라이브러리 조합
```bash
# 여러 라이브러리를 함께 사용하는 패턴
"React + TypeScript + Prisma를 사용한 풀스택 애플리케이션 구조"
"Vue 3 + Pinia + Vite로 모던 SPA 개발하기"
"Express + JWT + bcrypt로 인증 시스템 구축"
```

### 특정 기능 집중
```bash
# 특정 기능이나 패턴에 대한 상세 설명
"React Hook Form의 폼 유효성 검사 모든 기능"
"Zustand의 상태 관리 고급 패턴"
"Next.js의 API Routes 보안 모범 사례"
```

## 지원되는 Context7 ID 예시

### 프론트엔드
- `react`: React 라이브러리
- `vue`: Vue.js 프레임워크
- `angular`: Angular 프레임워크
- `nextjs`: Next.js 프레임워크
- `nuxtjs`: Nuxt.js 프레임워크

### 백엔드
- `express`: Express.js 웹 프레임워크
- `fastapi`: FastAPI Python 프레임워크
- `django`: Django Python 프레임워크
- `rails`: Ruby on Rails 프레임워크

### 데이터베이스
- `prisma`: Prisma ORM
- `typeorm`: TypeORM
- `mongoose`: Mongoose ODM
- `sequelize`: Sequelize ORM

### 유틸리티
- `lodash`: Lodash 유틸리티 라이브러리
- `axios`: Axios HTTP 클라이언트
- `dayjs`: Day.js 날짜 라이브러리
- `uuid`: UUID 생성 라이브러리

## 모범 사례

### 효과적인 질문 작성
```bash
# 구체적인 질문
"React의 useCallback을 언제 사용해야 하는지 실제 예시와 함께 설명해주세요"

# 컨텍스트 제공
"Next.js 13 앱 라우터에서 동적 라우팅과 서버 컴포넌트를 함께 사용하는 방법"

# 문제 상황 설명
"Material-UI의 DataGrid에서 행 선택 시 상태가 제대로 업데이트되지 않는 문제"
```

### 버전 명시
```bash
# 명확한 버전 지정
"React 18.2.0에서 Concurrent Features 사용법"
"Node.js 18.17의 새로운 기능과 변경사항"
"TypeScript 5.1에서 추가된 타입 기능"
```

### 프로젝트 컨텍스트 포함
```bash
# 프로젝트 정보 제공
"TypeScript + React + Prisma 스택에서 타입 안전한 API 호출 구현"
"Vue 3 Composition API를 사용한 커스텀 훅 패턴"
```

## 성능 최적화

### 캐싱 활용
- Context7은 자주 사용되는 문서를 캐시하여 응답 속도 향상
- 동일한 라이브러리 재요청 시 빠른 응답 제공
- 네트워크 사용량 최적화

### 정확한 요청
- 구체적인 라이브러리명과 버전 명시로 검색 정확도 향상
- 불필요한 라이브러리 문서 요청 방지
- 관련성 높은 문서만 선별적 제공

## 문제 해결

### 라이브러리를 찾을 수 없는 경우
```bash
# 정확한 라이브러리명 사용
"react-router-dom" (O) vs "react-router" (X)
"@mui/material" (O) vs "material-ui" (X)
```

### 문서가 최신이 아닌 경우
```bash
# Context7에 피드백 제공
# 해당 라이브러리의 최신 문서 업데이트 요청 가능
```

### 특정 버전 문서가 없는 경우
```bash
# 가장 가까운 버전의 문서 제공
# 버전 차이에 따른 변경사항 안내
```

## 제한사항

### 지원 범위
- 주요 오픈소스 라이브러리에 중점
- 내부 또는 비공개 라이브러리는 지원하지 않음
- 매우 새로운 라이브러리는 추가에 시간 소요

### 언어 지원
- 영어 문서 위주로 제공
- 일부 라이브러리는 다국어 문서 지원
- 한국어 번역이 필요한 경우 별도 요청

## 참고 자료

- [Context7 공식 GitHub](https://github.com/upstash/context7)
- [Context7 웹사이트](https://context7.dev)
- [Upstash 블로그](https://upstash.com/blog)
- [MCP 프로토콜 명세](https://github.com/modelcontextprotocol/specification)

---

**마지막 업데이트**: 2025-08-10  
**테스트 환경**: Windows, Claude CLI  
**설치 방법**: npm 전역 설치 + Claude MCP 등록