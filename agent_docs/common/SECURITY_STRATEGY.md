# 🛡️ Security & Auth Strategy (보안 및 인증 전략)

## 1. Authentication & Authorization
`admin_intra_login.php` 및 `member` 인증 로직을 대체합니다.

- **Framework**: `Spring Security`를 전면 도입합니다.
- **Legacy Session**: PHP 세션(`PHPSESSID`)과의 호환성이 필요한 경우, `Redis` 등을 통한 세션 공유 또는 JWT 토큰 기반의 이중화 전략이 필요할 수 있습니다. (우선순위: **신규 인증 체계 구축**)
- **Password**: 레거시 DB의 해시 알고리즘(예: `MySQL PASSWORD()`, `MD5`, `SHA1`)을 지원하는 `PasswordEncoder`를 커스텀 구현해야 합니다.

## 2. Vulnerability Protection
`check_xss.php`, `sql_injection_block.php` 등 수동 방어 로직을 프레임워크 기능으로 대체합니다.

- **SQL Injection**: `JPA`와 `QueryDSL` 사용으로 원천 차단합니다. (Raw SQL 사용 시 주의)
- **XSS (Cross-Site Scripting)**:
  - 입/출력 시 `Lucy XSS Filter` 또는 Jackson의 `CharacterEscapes` 설정을 적용합니다.
  - Thymeleaf 사용 시 기본 이스케이프(`th:text`)를 활용합니다.

## 3. Network Security
- **IP Restriction**: 관리자 페이지 등 민감한 영역은 Spring Security의 `IpAddressMatcher`로 접근 제어를 구현합니다.

