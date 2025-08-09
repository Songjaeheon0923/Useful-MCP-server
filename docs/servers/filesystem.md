# 📁 File System Server

**패키지**: `@modelcontextprotocol/server-filesystem`  
**GitHub**: [Filesystem MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)  
**상태**: ✅ **연결됨**  

## 개요

File System MCP Server는 Claude가 로컬 파일 시스템과 안전하게 상호작용할 수 있게 해주는 핵심 도구입니다. 파일 및 디렉토리 관리부터 검색, 메타데이터 조회까지 모든 파일 시스템 작업을 Claude를 통해 수행할 수 있습니다.

## 설치 및 설정

### 1. MCP 서버 추가
```bash
# 전체 시스템 액세스 (권장)
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem C:\

# 특정 디렉토리만 액세스
claude mcp add filesystem --scope user npx @modelcontextprotocol/server-filesystem "C:\project"
```

### 2. 연결 확인
```bash
claude mcp list
# filesystem: npx @modelcontextprotocol/server-filesystem C:\ - ✓ Connected 확인
```

## 주요 기능

### 📂 파일 관리
- **파일 CRUD**: 생성, 읽기, 수정, 삭제, 이동/이름변경
- **디렉토리 관리**: 생성, 나열, 트리 구조 조회
- **다중 파일 처리**: 여러 파일 동시 읽기 및 배치 작업
- **메타데이터**: 파일 크기, 수정일, 권한 등 상세 정보

### 🔍 검색 및 탐색
- **패턴 기반 검색**: 파일명 및 경로 패턴 매칭
- **재귀 검색**: 하위 디렉토리 포함 전체 검색
- **제외 패턴**: 불필요한 파일/디렉토리 필터링
- **크기별 정렬**: 파일 크기 기준 정렬 및 분석

### 🛡️ 보안 및 제어
- **경로 제한**: 지정된 디렉토리 내에서만 작업
- **안전한 편집**: 라인 기반 정확한 파일 수정
- **백업 호환**: 기존 파일 보존하며 안전한 업데이트

## 사용 가능한 도구들

### 파일 읽기
- `read_text_file`: 텍스트 파일 읽기 (부분 읽기 지원)
- `read_multiple_files`: 여러 파일 동시 읽기
- `read_media_file`: 이미지/오디오 파일 읽기

### 파일 작성
- `write_file`: 파일 생성/덮어쓰기
- `edit_file`: 라인 기반 파일 편집 (정확한 수정)

### 디렉토리 관리
- `create_directory`: 디렉토리 생성 (중첩 생성 지원)
- `list_directory`: 디렉토리 내용 나열
- `list_directory_with_sizes`: 크기 정보 포함 나열
- `directory_tree`: 재귀적 트리 구조 조회

### 파일 작업
- `move_file`: 파일/디렉토리 이동/이름변경
- `get_file_info`: 파일 메타데이터 조회

### 검색
- `search_files`: 패턴 기반 파일 검색

## 사용 예시

### 기본 파일 작업
```bash
# Claude에서 사용 예시:
"프로젝트의 모든 .py 파일에서 deprecated 함수를 찾아주세요"
"이 디렉토리를 정리해서 파일을 용도별로 분류해주세요"
"로그 파일들을 크기별로 정렬하고 가장 큰 10개 파일을 보여주세요"
"이 설정 파일의 특정 값을 모든 환경에서 동일하게 업데이트해주세요"
"백업 파일들 중 30일 이상 된 파일들을 찾아주세요"
```

### 프로젝트 관리
```bash
"이 프로젝트의 코드베이스 구조를 분석해서 README에 정리해주세요"
"모든 JavaScript 파일에서 사용되지 않는 import 구문을 찾아주세요"
"package.json과 실제 사용되는 dependencies를 비교해주세요"
"중복된 코드 패턴을 찾아서 공통 함수로 리팩토링 제안해주세요"
```

### 로그 분석
```bash
"error 키워드가 포함된 모든 로그 파일을 찾아서 분석해주세요"
"지난 주 서버 로그에서 가장 자주 발생한 오류 TOP 10을 찾아주세요"
"접근 로그를 분석해서 가장 인기있는 API 엔드포인트를 알려주세요"
```

## 자동화 워크플로우 예시

### 📊 프로젝트 유지보수
- **코드 정리**: 사용되지 않는 파일, 중복 코드, deprecated 함수 자동 탐지
- **의존성 관리**: package.json, requirements.txt 등과 실제 사용 비교
- **문서 동기화**: 코드 변경사항을 기반으로 문서 자동 업데이트

### 🔍 모니터링 및 분석
- **로그 분석**: 오류 패턴, 성능 이슈, 사용 통계 자동 분석
- **파일 시스템 정리**: 임시 파일, 오래된 백업, 큰 파일 자동 정리
- **보안 스캔**: 민감한 정보가 포함된 파일 탐지 및 알림

### 🛠️ 개발 도구 통합
- **빌드 최적화**: 불필요한 파일 제외, 에셋 압축, 번들 크기 분석
- **테스트 관리**: 테스트 파일과 실제 코드 매칭, 커버리지 분석
- **배포 준비**: 환경별 설정 파일 자동 생성 및 검증

## 고급 사용법

### 대용량 파일 처리
```bash
# 부분 읽기로 메모리 효율성 확보
"이 큰 로그 파일의 마지막 100줄만 읽어서 최근 오류를 확인해주세요"
"1GB 크기의 데이터 파일을 청크 단위로 나누어 처리해주세요"
```

### 배치 작업
```bash
# 여러 파일 동시 처리
"src 디렉토리의 모든 TypeScript 파일의 헤더 주석을 업데이트해주세요"
"프로젝트 내 모든 README 파일을 표준 형식으로 통일해주세요"
```

### 패턴 매칭
```bash
# 정규식을 활용한 고급 검색
"*.config.js 파일들에서 특정 설정값을 찾아서 일괄 변경해주세요"
"test/**/*.spec.js 패턴의 모든 테스트 파일을 분석해주세요"
```

## 보안 고려사항

### 액세스 제한
- MCP 서버는 지정된 루트 디렉토리 외부로는 액세스할 수 없습니다
- 시스템 파일이나 민감한 디렉토리는 신중하게 설정하세요

### 안전한 편집
- `edit_file` 도구는 정확한 라인 매칭을 통해 의도하지 않은 변경을 방지합니다
- 중요한 파일은 편집 전 백업을 권장합니다

### 권한 관리
- 읽기 전용이 필요한 경우 별도의 읽기 전용 MCP 서버 설정을 고려하세요

## 문제 해결

### 권한 오류
```bash
# Windows에서 액세스 거부 오류 시
# 관리자 권한으로 CMD/PowerShell 실행 후 다시 시도

# 특정 디렉토리 권한 문제 시
# 해당 디렉토리의 보안 설정 확인
```

### 성능 최적화
```bash
# 대용량 디렉토리 처리 시
# exclude 패턴으로 불필요한 파일 제외
"node_modules와 .git 디렉토리를 제외하고 검색해주세요"
```

### 인코딩 문제
- UTF-8이 아닌 파일의 경우 명시적으로 인코딩을 지정하세요
- 바이너리 파일은 `read_media_file` 도구를 사용하세요

## 참고 자료

- [Node.js File System API](https://nodejs.org/api/fs.html)
- [Official Filesystem MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- [File Pattern Matching](https://en.wikipedia.org/wiki/Glob_(programming))

---

**마지막 업데이트**: 2025-08-09  
**테스트 환경**: Windows, Claude CLI