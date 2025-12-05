# 🛠️ Legacy Utility Mapping (레거시 유틸리티 매핑)

## 1. Global Functions (`_function.php`)
PHP 전역 함수들을 Java 유틸리티 클래스로 매핑합니다.

| Legacy Function | Java Strategy | Note |
|:---:|:---:|:---:|
| `__sendSMS`, `__logSMS` | `CrmService` (Domain Service) | CRM 도메인으로 로직 이관 |
| `convertText` (Encoding) | `String` (Native) | Java는 내부적으로 UTF-16 사용. 입출력 시 인코딩 변환 주의 |
| `objectToArray` | `Jackson ObjectMapper` | `convertValue()` 사용 |
| Date Functions | `java.time` (LocalTime, ZonedDateTime) | `java.util.Date` 지양 |

## 2. Common Classes (`common/func/*.php`)
공통 폴더에 있지만 실제로는 특정 도메인 로직인 클래스들을 재배치합니다.

- **Domain-Specific**:
  - `class_Academy.php` → `AcademyService`
  - `class_Member.php` → `MemberService`
  - `class_Sms.php` → `CrmService`
- **Pure Utility**:
  - `class_FileTransfer.php` → `FileService` / `StorageUtil`
  - `class_PopupWindow.php` → `PopupService` (CRM/Admin Domain)

## 3. Configuration (`_config.php`)
- **Constants**: 전역 상수는 `application.yml` (프로파일별 분리) 또는 `GlobalConst` 인터페이스로 정의합니다.

