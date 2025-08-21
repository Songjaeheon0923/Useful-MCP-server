# 🎨 Figma MCP 사용 가이드

## 빠른 참조

### 기본 설정
```bash
# 패키지 설치
npm install -g mcp-figma

# 서버 추가
claude mcp add figma --scope user npx mcp-figma -e FIGMA_API_KEY=YOUR_TOKEN

# 연결 확인
claude mcp list
```

### API 토큰 발급
1. https://www.figma.com → Settings → Personal Access Tokens
2. **Generate new token** 클릭
3. 토큰 이름 입력: "Claude MCP"
4. 권한 선택:
   - ✅ File access
   - ✅ Team library access
5. 토큰 복사 (형식: `figd_...`)

## 실제 사용 예시

### Figma 파일 데이터 추출
```bash
# Figma 파일 URL에서 파일 ID 추출
# URL: https://www.figma.com/design/EYQU5IrBSVEHOmlcqFYGYA/Uni-con
# 파일 ID: EYQU5IrBSVEHOmlcqFYGYA

# Claude에서 사용:
"Figma 파일 EYQU5IrBSVEHOmlcqFYGYA의 디자인 구조를 분석해주세요"
"이 Figma 파일에서 색상 팔레트를 추출해주세요"
"메인 화면의 레이아웃을 React 컴포넌트로 변환해주세요"
```

### 테스트 완료된 기능들

#### ✅ 디자인 데이터 추출
- **파일 구조 분석**: 페이지, 프레임, 컴포넌트 계층 구조
- **스타일 정보**: 색상, 폰트, 크기, 위치 데이터
- **컴포넌트 정보**: 버튼, 입력 필드, 카드 등의 디자인 스펙

#### ✅ 실제 테스트 결과 (Uni-con 프로젝트)
- **파일 크기**: 8.4MB의 상세 디자인 데이터
- **발견된 화면**: 홈, 로그인, 룸메이트 매칭, 계약서 분석 등
- **UI 컴포넌트**: 버튼, 폼, 카드, 아이콘 등 다양한 컴포넌트

### 주요 활용 사례

#### 1. 디자인 시스템 분석
```
"이 Figma 파일에서 사용된 모든 색상과 폰트를 정리해주세요"
"디자인 토큰을 CSS 변수로 변환해주세요"
"컴포넌트별 스타일 가이드를 만들어주세요"
```

#### 2. 코드 생성
```
"홈 화면을 React 컴포넌트로 변환해주세요"
"이 버튼 디자인을 CSS로 구현해주세요"
"반응형 레이아웃을 Tailwind CSS로 작성해주세요"
```

#### 3. 에셋 추출
```
"모든 아이콘을 SVG로 추출해주세요"
"이미지 파일들의 다운로드 링크를 생성해주세요"
"로고를 다양한 크기로 내보내주세요"
```

## 문제 해결

### 연결 실패 시
```bash
# 1. 패키지 재설치
npm uninstall -g mcp-figma
npm install -g mcp-figma

# 2. 서버 재설정
claude mcp remove figma -s user
claude mcp add figma --scope user npx mcp-figma -e FIGMA_API_KEY=YOUR_TOKEN

# 3. API 키 확인
echo $FIGMA_API_KEY  # Linux/macOS
echo %FIGMA_API_KEY%  # Windows
```

### API 오류 시
- Figma 토큰이 유효한지 확인
- 파일에 대한 접근 권한이 있는지 확인
- 토큰의 권한 설정(File access, Team library access) 확인

### 파일 접근 불가 시
- 파일이 공개되어 있거나 공유되어 있는지 확인
- 올바른 파일 ID를 사용하고 있는지 확인
- 팀 멤버인 경우 팀 라이브러리 접근 권한 확인

## 팁과 권장사항

### 효율적인 사용법
1. **파일 ID 저장**: 자주 사용하는 Figma 파일의 ID를 메모해두기
2. **단계별 요청**: 큰 파일의 경우 페이지별로 나누어 분석
3. **스타일 우선**: 디자인 토큰과 컴포넌트 스타일을 먼저 추출

### 성능 최적화
- 큰 파일의 경우 특정 페이지나 컴포넌트만 분석
- 이미지 다운로드가 필요한 경우에만 요청
- 캐시된 결과 활용

## 지원되는 Figma 기능

### ✅ 완전 지원
- 기본 도형 (Rectangle, Ellipse, Text 등)
- 프레임 및 그룹
- 컴포넌트 및 인스턴스
- 스타일 속성 (색상, 폰트, 효과 등)
- Auto Layout 정보

### ⚠️ 부분 지원
- 복잡한 벡터 그래픽
- 고급 효과 및 블렌딩
- 프로토타이핑 인터랙션

### ❌ 미지원
- 댓글 및 피드백
- 버전 히스토리
- 실시간 협업 데이터

---

**마지막 업데이트**: 2025-08-21  
**테스트 환경**: Windows, Claude CLI, mcp-figma  
**테스트 파일**: Uni-con 프로젝트 (8.4MB)