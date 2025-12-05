# 🏫 Academy Test Guide (테스트 작성 가이드)

## 1. 테스트 전략 (Test Strategy)

### 1.1. Unit Test (Service)
- **목표**: 비즈니스 로직 검증 (DB 의존성 없음).
- **도구**: `Mockito` 활용.
- **중점**: 인코딩 변환 로직, 날짜 계산 로직 등이 PHP 원본과 동일하게 동작하는지 검증.

### 1.2. Repository Test (Data Access)
- **목표**: 실제 쿼리 및 매핑 검증.
- **도구**: `@DataJpaTest`.
- **주의**: 레거시 DB 연결 시 **Read-Only 트랜잭션** 필수.

### 1.3. Integration Test (Controller)
- **목표**: API 엔드포인트 호출 및 응답 구조 검증.
- **도구**: `@SpringBootTest`, `MockMvc`.

---

## 2. 주요 테스트 시나리오

### 2.1. Encoding & Data Integrity
- DB의 `EUC-KR` 한글 데이터가 깨지지 않고 조회되는지 검증하는 테스트 케이스 필수.
- 특수문자(`&`, `<` 등)가 포함된 데이터 처리 검증.

### 2.2. Legacy Compatibility
- `menu_1.php` (시즌 정보)와 동일한 로직으로 현재 시즌을 가져오는지 검증.
- 선생님 정렬 순서(`sort_no`)가 PHP 원본과 일치하는지 검증.

## 3. 체크리스트 연동
테스트 코드는 `CHECKLIST.md`의 항목을 커버리지 기준으로 삼아야 합니다. 각 테스트 메서드 명에 체크리스트 항목을 반영하는 것을 권장합니다.
