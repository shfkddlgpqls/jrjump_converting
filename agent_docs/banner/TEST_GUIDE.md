# 🏳️ Banner Test Guide (배너 테스트 가이드)

## 1. Test Strategy
배너 도메인은 **노출 로직(기간, 확률)**의 정확성 검증이 핵심입니다.

### 1.1. Service Logic Test
- **Exposure Logic**: `class_Banner.php`의 확률 로직(Weight 기반 랜덤 선택)이 통계적으로 유효한지 검증 (반복 실행 테스트).
- **Period Check**: `sdate` ~ `edate` 사이의 배너만 정확히 필터링되는지 검증 (Boundary Value Analysis).

### 1.2. Data Integrity Test
- **Fragmented Tables**: 연도별 테이블(`banner_2024` 등)에서 데이터를 올바르게 취합(Union)하는지 검증.
- **Encoding**: 구형 DB의 한글 제목이 깨지지 않는지 확인.

## 2. Key Scenarios
- **랜덤 노출**: 가중치(Weight)가 0인 배너는 절대 노출되지 않아야 함.
- **기간 만료**: 종료일(`edate`)이 1초라도 지난 배너는 노출되지 않아야 함.
- **카테고리 매핑**: 특정 카테고리(`cate`) 요청 시 해당 배너만 반환되는지 검증.

