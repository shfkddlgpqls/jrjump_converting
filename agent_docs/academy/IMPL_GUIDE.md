# 🏫 Academy Implementation Guide (구현 가이드)

## 1. 개요
본 문서는 Academy(학원) 도메인의 비즈니스 로직(`Service`)과 API(`Controller`) 구현을 위한 핵심 전략과 주의사항을 기술합니다.

---

## 2. 아키텍처 설계 (Architecture)

### 2.1. Package Structure
```
com.hackers.jrjump.domain.academy
├── controller      # API 엔드포인트 (AcademyController 등)
├── service         # 비즈니스 로직 (AcademyService 등)
├── repository      # 데이터 접근 (JPA + QueryDSL)
├── entity          # JPA Entities
└── dto             # Data Transfer Objects (Request/Response 분리)
```

---

## 3. 구현 상세 가이드

### 3.1. Service Layer (비즈니스 로직)
- **PHP 로직 분해**: 뷰 렌더링 로직과 데이터 조회 로직을 철저히 분리하십시오.
- **트랜잭션**: `@Transactional(readOnly = true)`를 기본으로 적용하십시오.
- **인코딩**: DB 조회 후 `EUC-KR` → `UTF-8` 변환 로직을 필수적으로 적용하십시오.
- **공통 로직**: `class_Academy.php` 등의 공통 로직은 `AcademySupportService`로 분리하십시오.

#### 🔍 주요 서비스 메서드 매핑
- `menu_1.php` → `AcademyService.getSeasonInfo()`, `getMonthlyCalendar()`
- `menu_10.php` → `AcademyTeacherService.getTeacherList()`
- `teacher_detail_ajax.php` → `AcademyTeacherService.getTeacherDetail()` (HTML 디코딩 필수)

### 3.2. Controller Layer (API)
- **URL Prefix**: `/api/v1/academy`
- **REST API**: 자원 중심의 URL 설계를 지향하되, 레거시 뷰와의 호환성을 고려하십시오.

### 3.3. Repository Layer (DB 접근)
- **QueryDSL**: 동적 쿼리 및 복잡한 조인은 QueryDSL을 사용하십시오.
- **SQL Injection 방지**: 레거시의 `$query` 문자열 조합 방식을 버리고, 반드시 파라미터 바인딩을 사용하십시오.
