# 🎨 Figma MCP Server (Framelink)

**패키지**: `mcp-figma`  
**GitHub**: [mcp-figma npm](https://www.npmjs.com/package/mcp-figma)  
**상태**: ✅ **연결됨** (테스트 완료)  

## 개요

Figma MCP Server는 Figma 디자인을 실제 코드로 변환하는 혁신적인 도구입니다. 디자인 시스템 분석부터 다양한 프레임워크로의 코드 생성, 에셋 관리까지 디자인-투-개발 워크플로우를 완전히 자동화합니다.

## 설치 및 설정

### 1. Figma Personal Access Token 생성

#### 단계별 설정
1. [Figma](https://www.figma.com) 로그인
2. **Settings** → **Personal Access Tokens** 이동
3. **Generate new token** 클릭
4. 토큰 이름 입력 (예: "Claude MCP")
5. 생성된 토큰 복사 ⚠️ **한 번만 표시됩니다!**

#### 권한 범위
- **File access**: 팀 또는 개인 파일 접근
- **Team library access**: 디자인 시스템 컴포넌트 접근
- **Webhooks**: 실시간 변경 알림 (선택사항)

#### 환경 변수 설정 (선택사항)
```bash
# Windows에서 환경 변수로 관리하려면
setx FIGMA_ACCESS_TOKEN "figd_your-token-here"

# Linux/macOS
export FIGMA_ACCESS_TOKEN="figd_your-token-here"

# 영구 설정 (Linux/macOS)
echo 'export FIGMA_ACCESS_TOKEN="figd_your-token-here"' >> ~/.bashrc
source ~/.bashrc
```

### 2. MCP 서버 패키지 설치
```bash
# mcp-figma 패키지 전역 설치
npm install -g mcp-figma
```

### 3. MCP 서버 추가
```bash
# 환경 변수로 API 키 설정
claude mcp add figma --scope user npx mcp-figma -e FIGMA_API_KEY=YOUR_TOKEN

# 또는 시스템 환경 변수 설정 후
setx FIGMA_API_KEY "YOUR_TOKEN"  # Windows
export FIGMA_API_KEY="YOUR_TOKEN"  # Linux/macOS
claude mcp add figma --scope user npx mcp-figma
```

### 4. 연결 확인
```bash
claude mcp list
# figma: npx mcp-figma - ✓ Connected 확인
```

## ✅ 실제 테스트 결과

### 테스트 파일: Uni-con 프로젝트
- **파일 ID**: `EYQU5IrBSVEHOmlcqFYGYA`
- **파일 URL**: `https://www.figma.com/design/EYQU5IrBSVEHOmlcqFYGYA/Uni-con`
- **데이터 크기**: 약 8.4MB
- **테스트 결과**: ✅ 성공적으로 디자인 데이터 추출

### 발견된 화면 구조
- **홈 화면**: 메인 랜딩 페이지
- **로그인/회원가입**: 사용자 인증 화면
- **계약서 분석**: 의심 조항 질문 리스트
- **룸메이트 매칭**: 프로필 및 매칭 시스템
- **원룸 정보**: 매물 상세 정보 화면
- **동네지도**: 지역별 매물 표시

## 주요 기능

### 🎨 디자인-투-코드 변환
- **다중 프레임워크 지원**: HTML/CSS, React, Vue, Angular, Svelte 등으로 변환
- **스마트 레이아웃 분석**: Figma Auto Layout을 CSS Grid/Flexbox로 자동 변환
- **반응형 디자인**: 다양한 화면 크기에 맞는 미디어 쿼리 자동 생성
- **컴포넌트 시스템**: Figma 컴포넌트를 재사용 가능한 코드 컴포넌트로 변환

### 📊 디자인 시스템 분석
- **스타일 토큰 추출**: 색상, 타이포그래피, 간격 등을 CSS 변수로 변환
- **컴포넌트 라이브러리**: 디자인 시스템의 모든 컴포넌트를 코드로 생성
- **일관성 검사**: 디자인 시스템 내 스타일 일관성 검증
- **변경 사항 추적**: 디자인 업데이트 시 코드 동기화

### 🖼️ 에셋 관리
- **자동 이미지 최적화**: PNG, JPG, SVG 형식으로 자동 추출 및 최적화
- **아이콘 시스템**: SVG 아이콘을 컴포넌트화하여 관리
- **이미지 크롭**: 정확한 크기와 비율로 이미지 자동 크롭
- **리소스 번들링**: 모든 에셋을 프로젝트 구조에 맞게 조직화

## 사용 가능한 도구들

### get_figma_data
Figma 파일의 전체 구조와 디자인 정보를 분석하는 핵심 도구입니다.

#### 매개변수:
- **`fileKey`**: Figma 파일 키 (URL에서 추출, 필수)
- **`nodeId`**: 특정 노드/프레임 ID (선택적)
- **`depth`**: 노드 트리 탐색 깊이 제어 (선택적)

### download_figma_images  
이미지 및 아이콘을 자동으로 다운로드하고 최적화하는 도구입니다.

#### 매개변수:
- **`fileKey`**: Figma 파일 키 (필수)
- **`localPath`**: 이미지 저장 경로 (절대 경로, 필수)
- **`nodes`**: 다운로드할 노드 정보 배열 (필수)
- **`pngScale`**: PNG 이미지 스케일 (기본값: 2)

## 사용 예시

### 기본 디자인 변환
```bash
# Claude에서 사용 예시:
"이 Figma 파일을 React 컴포넌트로 변환해주세요: https://www.figma.com/file/abc123/MyDesign"
"이 프레임의 CSS를 Tailwind CSS로 생성해주세요"
"디자인 시스템에서 버튼 컴포넌트만 추출해서 코드로 만들어주세요"
"모든 아이콘을 SVG로 다운로드하고 React 컴포넌트로 만들어주세요"
"이 페이지 디자인을 반응형 HTML로 변환해주세요"
```

### 고급 활용
```bash
"Figma 컴포넌트 라이브러리를 Storybook으로 생성해주세요"
"이 디자인의 CSS 변수들을 추출해서 Design Token으로 만들어주세요"
"모바일과 데스크톱 버전을 각각 분석해서 반응형 코드를 생성해주세요"
"디자인 시스템의 일관성을 검증하고 문제점을 리포트해주세요"
```

### 팀 협업
```bash
"개발자를 위한 디자인 스펙 문서를 자동으로 생성해주세요"
"디자인 변경사항을 이전 버전과 비교해서 업데이트할 코드를 찾아주세요"
"이 프로토타입을 실제 작동하는 코드로 변환해주세요"
```

## 자동화 워크플로우 예시

### 🔄 디자인 시스템 동기화
- **자동 코드 업데이트**: Figma 디자인 시스템 변경 시 코드베이스 자동 업데이트
- **컴포넌트 라이브러리 생성**: 새로운 컴포넌트 추가 시 자동으로 코드 컴포넌트 생성
- **스타일 가이드 동기화**: 색상, 타이포그래피 변경 시 CSS 변수 자동 업데이트

### 🚀 개발 워크플로우 통합
- **Figma → GitHub PR**: 디자인 완료 시 자동으로 코드 생성 후 PR 생성
- **프로토타입 → MVP**: 프로토타입을 기반으로 실제 작동하는 MVP 코드 생성
- **A/B 테스트 지원**: 여러 디자인 버전에 대한 코드를 동시 생성

### 📊 품질 관리
- **디자인 일관성 검증**: 디자인 시스템 규칙 위반 자동 탐지
- **접근성 검사**: 색상 대비, 폰트 크기 등 접근성 기준 검증
- **성능 최적화**: 이미지 최적화, CSS 최적화 등 자동 적용

## 고급 사용법

### 복잡한 레이아웃 처리
```bash
# 중첩된 Auto Layout 변환
"이 복잡한 카드 레이아웃을 CSS Grid와 Flexbox를 조합해서 구현해주세요"

# 반응형 브레이크포인트
"모바일, 태블릿, 데스크톱 버전을 모두 고려한 반응형 코드를 생성해주세요"
```

### 컴포넌트 시스템 구축
```bash
# 변형 관리
"이 버튼 컴포넌트의 모든 변형(primary, secondary, disabled)을 코드로 만들어주세요"

# 상태 관리
"호버, 포커스, 액티브 상태를 모두 포함한 인터랙티브 컴포넌트를 만들어주세요"
```

### 디자인 토큰 활용
```bash
# 토큰 추출
"이 디자인 시스템에서 색상, 간격, 타이포그래피를 Design Token으로 추출해주세요"

# 브랜드 시스템
"다크모드와 라이트모드를 지원하는 CSS 변수 시스템을 만들어주세요"
```

## URL 패턴 이해

### Figma URL 구조
```
https://www.figma.com/file/[FILE_KEY]/[FILE_NAME]?node-id=[NODE_ID]
```

- **FILE_KEY**: `get_figma_data`의 `fileKey` 매개변수에 사용
- **NODE_ID**: 특정 프레임이나 컴포넌트를 지정할 때 사용

### 예시:
```
URL: https://www.figma.com/file/abc123def456/Design-System?node-id=1%3A2
FILE_KEY: abc123def456
NODE_ID: 1:2
```

## 성능 최적화

### 대용량 파일 처리
- `depth` 매개변수로 분석 깊이 제한
- 필요한 프레임만 선택적으로 분석
- `skip-image-downloads` 옵션으로 초기 분석 속도 향상

### 네트워크 최적화
- 이미지는 필요한 경우에만 다운로드
- 캐싱을 활용한 반복 요청 최소화
- 배치 처리로 API 호출 효율화

## 지원하는 출력 형식

### 프레임워크
- **React**: JSX + CSS Modules/Styled Components
- **Vue**: Single File Components (.vue)
- **Angular**: Component + Template + Styles
- **Svelte**: .svelte 파일
- **HTML/CSS**: 순수 HTML + CSS

### 스타일링 방법
- **CSS**: 일반 CSS 파일
- **Tailwind CSS**: 유틸리티 클래스 기반
- **Styled Components**: CSS-in-JS
- **CSS Modules**: 모듈화된 CSS
- **Design Tokens**: JSON/YAML 형식

## 문제 해결

### 인증 오류
```bash
# 토큰 확인
# Figma에서 토큰이 아직 유효한지 확인
# 팀 파일의 경우 적절한 권한이 있는지 확인

# 토큰 재생성
# 새 토큰 생성 후 MCP 서버 재설정
claude mcp remove figma-framelink
claude mcp add figma-framelink --scope user "npx figma-developer-mcp --figma-api-key=NEW_TOKEN --stdio"
```

### 파일 접근 오류
- 파일이 공개되어 있거나 토큰에 접근 권한이 있는지 확인
- 팀 파일의 경우 팀 멤버십 상태 확인

### 이미지 다운로드 실패
- 로컬 경로의 쓰기 권한 확인
- 충분한 디스크 공간 확보
- 방화벽이나 프록시 설정 확인

## 참고 자료

- [Figma API Documentation](https://www.figma.com/developers/api)
- [Figma Design Tokens](https://www.figma.com/community/plugin/888356646278934516/Design-Tokens)
- [Design System Best Practices](https://www.designsystems.com/)
- [Official Figma Context MCP](https://github.com/GLips/Figma-Context-MCP)

---

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI