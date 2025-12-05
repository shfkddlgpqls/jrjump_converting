# PHP to Spring Boot 마이그레이션

## 프로젝트 개요
- **목표**: PHP 코드를 Spring Boot로 기능적 100% 동일하게 이식 (리팩토링 금지)
- **경로**: `/Volumes/web/jrjump` (원본) → `/Volumes/web/jrjump-new` (대상)
- **스택**: PHP → Java 21, Spring Boot 3.x, Thymeleaf, JPA, MySQL

## 핵심 원칙
1. **추측 금지**: 원본 의도가 100% 확실할 때만 변경. 추측 구현 절대 금지.
2. **누락 금지**: HTML 속성, 공백, 주석, 예외 처리 등 모든 요소를 빠짐없이 이식.
3. **인코딩 확인**: 
  - `file -I` 확인 후 UTF-8 변환 필수. (EUC-KR)
  - EUC-KR 인 경우 `iconv -f EUC-KR -t UTF-8` 활용.