# 🔧 Admin - Common/System Migration Map

## 1. 개요
- **Domain**: System (시스템 설정, 과정/과목/시즌 관리, 관리자 로그)
- **Source Path**: `admin/System/`, `admin/inc/`
- **Target Controller**: `SystemAdminController`, `CourseAdminController`, `SeasonAdminController`

---

## 2. 소스/타겟 매핑

### 2-1. 시스템 관리 (System)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **관리자 로그인** | `admin/admin_intra_login.php` | Spring Security | 사내 통합 로그인(Intra) 연동 |
| **P2** | **관리자 로그** | `admin/System/AdminLog.php` | `SystemAdminController.logList()` | |
| **P2** | **일정 관리(캘린더)** | `admin/System/Calendar.php` | `SystemAdminController.calendar()` | |
| **P3** | **공통 코드 관리** | `admin/inc/` (참조) | `CodeAdminController` | 레거시 공통 코드 테이블 분석 필요 |

### 2-2. 과정(Course) 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **과정 목록** | `admin/System/CourseList.php` | `CourseAdminController.list()` | |
| **P1** | **과정 등록/수정** | `admin/System/CourseWrite.php`, `CourseRegist.php` | `CourseAdminController.save()` | |
| **P2** | **과정 소개 수정** | `admin/System/CourseIntroModify.php` | `CourseAdminController.updateIntro()` | |
| **P2** | **과정 미리보기** | `admin/System/CoursePreviewModify.php` | `CourseAdminController.updatePreview()` | |

### 2-3. 과목(Subject) 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **과목 목록** | `admin/System/SubjectList.php` | `SubjectAdminController.list()` | |
| **P1** | **과목 등록/수정** | `admin/System/SubjectWrite.php`, `SubjectRegist.php` | `SubjectAdminController.save()` | |

### 2-4. 시즌(Season) 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **시즌 목록** | `admin/System/SeasonList.php` | `SeasonAdminController.list()` | |
| **P1** | **시즌 등록/수정** | `admin/System/SeasonWrite.php`, `SeasonRegist.php` | `SeasonAdminController.save()` | |
| **P2** | **시즌 오픈 설정** | `admin/System/SeasonOpen.php`, `SeasonOpenWrite.php` | `SeasonAdminController.openSeason()` | |

### 2-5. 반(Class) 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **반 목록** | `admin/System/ClassList.php` | `ClassAdminController.list()` | |
| **P1** | **반 등록/수정** | `admin/System/ClassWrite.php`, `ClassRegist.php` | `ClassAdminController.save()` | |
| **P2** | **반별 수강생 조회** | `admin/System/ClassListMem.php` | `ClassAdminController.memberList()` | 엑셀 다운로드 포함 |
| **P2** | **반 레벨 관리** | `admin/System/ClassLevelList.php`, `ClassLevelWrite.php` | `ClassAdminController.levelList()` | |

### 2-6. 강의실(Room) 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **강의실 목록** | `admin/System/RoomList.php` | `RoomAdminController.list()` | |
| **P2** | **강의실 등록/수정** | `admin/System/RoomReg.php`, `RoomModify.php` | `RoomAdminController.save()` | |

### 2-7. 강좌(Lecture) 기본 설정
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **강좌 목록** | `admin/System/LectureList.php` | `LectureAdminController.list()` | |
| **P1** | **강좌 등록/수정** | `admin/System/LectureWrite.php`, `LectureRegist.php` | `LectureAdminController.save()` | |
| **P2** | **라이브 클래스 설정** | `admin/System/LectureWriteLiveClass.php` | `LectureAdminController.saveLiveClass()` | |

---

## 3. 핵심 엔티티 참조
- `Course` → `agent_docs/lecture/ENTITY_GUIDE.md` (예정)
- `Subject` → `agent_docs/lecture/ENTITY_GUIDE.md` (예정)
- `Season` → `agent_docs/lecture/ENTITY_GUIDE.md` (예정)
- `Room` → `agent_docs/academy/ENTITY_GUIDE.md`

## 4. 주의사항
- `admin/System/`과 `admin/Lecture/`에 유사한 기능이 분산되어 있음
- Course, Subject, Season은 강좌(Lecture) 도메인의 기초 마스터 데이터
- 시즌 오픈은 수강신청 기간 설정과 연관

