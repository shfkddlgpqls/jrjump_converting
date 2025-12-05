# 🔧 Admin Implementation Guide (구현 가이드)

## 1. 아키텍처 (Architecture)

### 1.1. Package Structure
Admin 기능은 별도의 최상위 패키지(`admin`) 또는 각 도메인 하위의 `admin` 패키지로 구성할 수 있으나, 본 프로젝트는 **통합 관리를 위해 최상위 `admin` 패키지**를 권장합니다.

```
com.hackers.jrjump.domain.admin
├── controller      # AdminController
├── service         # AdminService (필요시 도메인 서비스 호출)
├── dto             # Admin 전용 DTO
└── config          # SecurityConfig (Admin 전용)
```

### 1.2. 엔티티 재사용 (Entity Reuse)
- Admin은 데이터를 소유하지 않습니다. `domain.academy.entity`, `domain.member.entity` 등을 Import 하여 사용합니다.
- **DTO 분리**: 엔티티를 그대로 쓰지 말고, Admin 전용 `Request/Response DTO`를 만들어야 합니다. (예: `AcademyTeacherAdminRequest`)

---

## 2. 공통 구현 전략

### 2.1. 인증/권한 (Security)
- **URL 패턴**: `/admin/**`
- **권한 체크**: `hasRole('ADMIN')` 또는 IP 접근 제어
- **로그인**: 기존 `admin_intra_login.php` 로직을 분석하여, 사내 통합 로그인(Intra) 또는 별도 테이블(`SETUP_ADMIN` 등) 인증을 구현해야 합니다.

### 2.2. 공통 레이아웃 (Thymeleaf)
- PHP의 `admin/inc/header.php`, `footer.php`를 Thymeleaf `Fragment`로 변환합니다.
- `layout/admin_layout.html`을 만들어 모든 Admin 페이지가 상속받도록 합니다.

### 2.3. 파일 업로드
- 선생님 프로필 이미지 등록(`ProfileModify.php`) 시 파일 업로드가 필수입니다.
- `MultipartFile`을 처리하는 공통 유틸리티(`FileUploader`)를 구현하여 사용합니다.
- **경로 유지**: 원본 PHP가 `/home/web/jrjump/data/File/` 경로를 사용한다면, Spring Boot에서도 `application.yml`에 `file.upload-dir`을 설정하여 동일한(또는 호환되는) 경로에 저장해야 합니다. DB에는 **상대 경로**만 저장합니다.

### 2.4. View 호환성 (View Compatibility)
- **변수명 보존**: PHP View에서 `$teacher_list`로 사용했다면, Java Model에도 `model.addAttribute("teacher_list", list)`와 같이 **스네이크 케이스**를 그대로 사용하십시오.
- **DTO 호환성**: PHP의 `PageInfo`(`total`, `curr`, `scale`) 구조를 모방한 DTO를 사용하여 View 수정 비용을 최소화합니다.

## 3. 공통/레거시 라이브러리 (Legacy Libs)
- **Source**: `admin/inc/`, `admin/inc/DB/`
- **Strategy**:
    - DB 연결(`db_connect`)은 Spring `DataSource`로 대체합니다.
    - 문자열 처리/날짜 계산 등 유틸리티성 함수는 `com.hackers.jrjump.common.util.LegacyUtil` 등으로 이관합니다.
    - **주의**: `EUC-KR` 처리를 위한 `iconv` 등의 함수는 Java의 `String` 인코딩 처리로 대체합니다.
