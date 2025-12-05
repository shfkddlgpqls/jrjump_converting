# 📡 API Standard Guide (API 표준 가이드)

## 1. Response Format
모든 API는 통일된 래퍼(Wrapper) 객체를 반환해야 합니다.

- **Structure**:
  - `code` (String): 성공 시 "SUCCESS", 실패 시 에러 코드.
  - `message` (String): 사용자에게 노출 가능한 메시지.
  - `data` (T): 실제 페이로드 (Generic).

## 2. Exception Handling
- **Global Handling**: `@RestControllerAdvice`를 통해 모든 예외를 포착하고 위 표준 포맷으로 변환합니다.
- **Custom Exceptions**: `BusinessException`을 상속받아 도메인별 예외를 정의합니다.

## 3. Data Types
- **Date/Time**: `ISO 8601` 형식을 준수합니다.
- **Boolean**: JSON `true`/`false` 타입을 사용합니다. (문자열 "Y"/"N" 금지)
