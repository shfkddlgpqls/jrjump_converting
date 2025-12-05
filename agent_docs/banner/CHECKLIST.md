# ✅ Banner Implementation Checklist

## 1. 노출 로직 검증
- [ ] **기간 체크**: `class_Banner.php`의 로직을 분석하여 `start_date` ~ `end_date` 체크 로직이 정확히 구현되었는가?
- [ ] **활성 상태**: `use_yn='Y'`(또는 `status`)인 배너만 노출되는가?
- [ ] **우선순위**: `sort_no` 순서대로 배너가 정렬되는가?

## 2. 테이블 및 파편화 대응
- [ ] **테이블 확인**: `bannerCateList` 테이블을 기본으로 하되, 연도별 테이블(`bannerTotalMain24` 등) 사용 여부를 `class_Banner.php`에서 반드시 교차 검증했는가?
- [ ] **새 탭 여부**: `target='_blank'` 설정 시 새 창으로 뜨는지 확인.

## 3. 성능 및 캐싱
- [ ] **캐시 적용**: 배너는 변경 빈도가 낮으므로 `@Cacheable` 적용 여부 및 갱신 테스트.
- [ ] **이미지 로딩 속도**: 고화질 배너 이미지가 적절한 속도로 로딩되는가?
