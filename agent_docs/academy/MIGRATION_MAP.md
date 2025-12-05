# 🏫 Academy (학원) Migration Map

## 1. 개요
- **Domain**: Academy (학원)
- **Description**: 학원 정보, 강좌 소개, 상담 신청, 예약 시스템 등 오프라인 학원 관련 기능
- **Base URL**: `/regi` (기존), `/academy` (신규 API)

## 2. 소스/타겟 매핑 (Mapping)

분석 및 구현은 **Priority(우선순위)** 순서대로 진행하십시오.

| Priority | 기능 (Feature) | PHP Source (Legacy) | Java Target (New) | 비고 |
|:---:|---|---|---|---|
| **P1** | **개강일 체크** | `academy/menu_1.php` | `AcademyService.getSeasonInfo()` | `jr_season_open` (Admin의 `jr_season`과 관계 확인 필요) |
| **P1** | **학원 캘린더** | `academy/menu_1.php` | `AcademyService.getCalendar()` | `SETUP_CLASS_CALENDAR` 테이블 조회 |
| **P1** | **선생님 목록** | `academy/menu_10.php` | `AcademyTeacherController.list()` | `SETUP_PROFILE` 테이블 단순 조회 |
| **P2** | **선생님 상세(Ajax)** | `academy/teacher_detail_ajax.php` | `AcademyTeacherService.getDetail()` | HTML 디코딩 필요 |
| **P2** | **학원 메인** | `academy/index.php` | `AcademyController.index()` | 여러 컴포넌트 조합 |
| **P2** | **강좌 리스트** | `academy/lecture_list.php` | `AcademyLectureController.list()` | 필터링 로직 포함 |
| **P3** | **상담 신청** | `academy/consult_write.php` | `AcademyConsultController.create()` | 폼 데이터 처리 (INSERT) |

## 3. 주요 엔티티 (Entities)

| PHP Table | Java Entity | 설명 |
|---|---|---|
| `jr_season_open` | `AcademySeason` | 학원 개강일/시즌 정보 |
| `SETUP_CLASS_CALENDAR` | `AcademyCalendar` | 학원 주요 일정 캘린더 |
| `SETUP_PROFILE` | `AcademyTeacher` | 선생님 프로필 정보 (소개, 이미지 등) |
| `jrjumpi.lecture_teacher_join` | `LectureTeacher` | 강좌-선생님 연결 정보 (DB 교차 참조 주의) |

## 4. 마이그레이션 주의사항
1. **DB 연결**: `jrjump` DB와 `jrjumpi` DB(인강)가 혼용되어 사용됨. `Academy` 클래스(`common/func/class_Academy.php`) 참조 필수.
2. **인코딩**: DB 데이터 조회 시 `EUC-KR` -> `UTF-8` 변환 필수 (`iconv` 사용).
3. **경로**: 기존 `/regi` 하위 경로가 많으므로 URL 매핑 시 주의.
4. **하드코딩**: `menu_10.php` 등에 선생님 번호(`no`) 매핑 로직이 하드코딩 되어 있으므로, 이를 설정화하거나 DB화 하는 방안 고려 필요 (단, **기능적 100% 이식**이 우선이므로 로직 유지는 필요).
