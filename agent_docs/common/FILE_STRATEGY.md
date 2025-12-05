# 📂 File & Document Strategy (파일 및 문서 전략)

## 1. File Storage (S3 & Local)
레거시 시스템(`S3File*.php`, `class_FileTransfer.php`)의 기능을 대체합니다.

- **AWS S3**: `Spring Cloud AWS` 또는 `AWS SDK v2`를 사용하여 구현합니다.
- **Local Upload**: 개발/테스트 환경을 위해 로컬 업로드 기능도 인터페이스(`StorageService`)로 추상화하여 지원해야 합니다.
- **Path Compatibility**: 레거시 파일 경로(DB에 저장된 경로)와의 호환성을 위해 경로 매핑 로직(`PathStrategy`)이 필요합니다.

## 2. Excel Processing
레거시의 HTML 헤더 변경 방식(`_system_/_excel.php`)을 지양하고, 표준 라이브러리를 사용합니다.

- **Library**: `Apache POI` (대용량 처리가 필요한 경우 `SXSSF` 방식 권장).
- **View**: `AbstractXlsxView`를 상속받은 커스텀 뷰를 사용하여 컨트롤러와 뷰를 분리합니다.

## 3. PDF Generation
레거시의 `fpdf`, `tcpdf` 라이브러리를 대체합니다.

- **Library**: `OpenPDF` (iText의 오픈소스 포크) 또는 `Thymeleaf` + `Flying Saucer` 조합을 권장합니다.
- **Template**: HTML 템플릿 기반으로 생성하여 유지보수성을 높입니다.

## 4. DRM (Digital Rights Management)
`drm.class.php` 및 `S3DrmFile.php`의 로직은 별도 `DrmService`로 캡슐화해야 합니다.
- **Note**: 레거시 DRM 해제/적용 바이너리나 라이브러리가 필요한 경우 JNI 또는 외부 프로세스 실행 방식을 검토해야 합니다.

