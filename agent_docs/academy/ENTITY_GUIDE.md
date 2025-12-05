# 🏫 Academy Entity Guide (엔티티 설계 가이드)

## 1. 개요
이 문서는 Academy(학원) 도메인의 주요 엔티티 설계 정보를 담고 있습니다.
개발 시 본 가이드를 참고하여 JPA Entity 클래스를 생성하십시오.

> **⚠️ 중요 원칙**
> 1. **테이블명 유지**: `@Table(name = "...")`을 사용하여 레거시 테이블명을 그대로 매핑합니다.
> 2. **인코딩 처리**: `EUC-KR` 데이터가 포함된 컬럼은 조회/저장 시 인코딩 변환 로직이 필요할 수 있으나, Entity 레벨에서는 `String`으로 받고 Service/Converter에서 처리하는 것을 권장합니다.
> 3. **불변성**: 가능한 `Setter` 사용을 지양하고, 비즈니스 메서드를 통해 상태를 변경합니다.

---

## 2. 주요 엔티티 상세

### 2.1. AcademySeason (시즌 정보)
- **Legacy Table**: `jr_season_open`
- **Description**: 학원/인강 수강신청 시즌(기간) 관리

| Field Name | Column Name | Type | Constraints | Description |
|---|---|---|---|---|
| `id` | `seasid` | `String` | PK, Length: 6 | 시즌ID (YYYYMM 형식, 예: 202503) |
| `openDate` | `open_date` | `LocalDate` | | 시즌 오픈 일자 |
| `mainOutput` | `main_output` | `String` | Length: 1 | 메인 페이지 노출 여부 (Y/N) |

**Implementation Hint:**
```java
@Entity
@Table(name = "jr_season_open")
public class AcademySeason {
    @Id
    @Column(name = "seasid", length = 6)
    private String id;
    // ...
}
```

---

### 2.2. AcademyCalendar (학원 일정)
- **Legacy Table**: `SETUP_CLASS_CALENDAR`
- **Description**: 학원 주요 행사 및 일정 캘린더

| Field Name | Column Name | Type | Constraints | Description |
|---|---|---|---|---|
| `id` | `no` | `Long` | PK, Auto Inc | 고유 번호 |
| `color` | `color` | `String` | Length: 20 | 일정 표시 색상 (CSS 클래스 등) |
| `content` | `content` | `String` | TEXT | 일정 상세 내용 (**EUC-KR**) |
| `eventDate` | `event_dt` | `LocalDateTime` | | 일정 날짜/시간 |
| `sortNo` | `sort_no` | `Integer` | | 정렬 순서 |
| `insertDate` | `ins_dt` | `LocalDateTime` | | 등록일시 |
| `updateDate` | `upd_dt` | `LocalDateTime` | | 수정일시 |

**Implementation Hint:**
- `content` 컬럼은 한글이 포함되므로 인코딩 변환(`EUC-KR` -> `UTF-8`)에 유의해야 합니다.

---

### 2.3. AcademyTeacher (선생님 프로필)
- **Legacy Table**: `SETUP_PROFILE`
- **Description**: 학원 선생님 소개, 사진, 약력 정보

| Field Name | Column Name | Type | Constraints | Description |
|---|---|---|---|---|
| `id` | `no` | `Long` | PK, Auto Inc | 고유 번호 |
| `courseType` | `course_type` | `String` | | 강좌 구분 (영어, 일본어 등) |
| `courseName` | `course` | `String` | | 강좌/과목명 (**EUC-KR**) |
| `name` | `pro_name` | `String` | | 선생님 이름 (**EUC-KR**) |
| `mainStatus` | `main_status` | `String` | Length: 1 | 메인 노출 여부 (Y/N) |
| `isUse` | `is_use` | `String` | Length: 1 | 사용 여부 (Y/N) |
| `imageMain` | `img_main` | `String` | | 메인 프로필 이미지 경로 |
| `imageListBig` | `img_list_big` | `String` | | 리스트용 큰 이미지 |
| `imageListSmall`| `img_list_small`| `String` | | 리스트용 작은 이미지 |
| `achievement` | `achievement` | `String` | TEXT | 학력/약력 (**EUC-KR**, HTML) |
| `writing` | `writing` | `String` | TEXT | 저서 정보 (**EUC-KR**, HTML) |
| `introduction` | `contents` | `String` | LONGTEXT | 상세 소개 (**EUC-KR**, HTML) |
| `vodUrl` | `vod_url` | `String` | | 맛보기 영상 URL |
| `teacherUrl` | `teacher_url` | `String` | | 선생님 개인 홈페이지 URL |

**Implementation Hint:**
- `achievement`, `writing`, `contents` 등 텍스트 필드는 HTML 태그를 포함할 수 있으며, **반드시 EUC-KR 디코딩**이 필요합니다.
- 이미지 경로는 기존 경로(`/images/...`)를 그대로 유지하거나, CDN 경로로 변환하는 로직이 필요할 수 있습니다.

---

## 3. 연관 관계 (Relations)

### 3.1. LectureTeacher (강좌-선생님 연결)
- **Legacy Table**: `jrjumpi.lecture_teacher_join` (External DB)
- **Note**: 인강 DB(`jrjumpi`)에 있는 테이블이므로, JPA 연관관계(`@OneToMany` 등)를 직접 맺기 어렵습니다.
- **Strategy**:
    1. `teacher_no` (선생님ID)를 기준으로 **논리적 연결**만 수행합니다.
    2. 필요 시 `JdbcTemplate`이나 별도의 `DataSource`를 통해 조회합니다.
    3. Entity 레벨에서의 직접적인 참조(`@ManyToOne`)는 **지양**합니다.

