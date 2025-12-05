# 🔧 Admin - Academy Migration Map

## 1. 개요
- **Domain**: Academy (학원 운영/강사/강좌)
- **Target Controller**: `AcademyAdminController`, `AcademyBasicAdminController`

## 2. 소스/타겟 매핑

### 2-1. 기초 코드 관리 (admin/System)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **학기(Season) 관리** | `admin/System/SeasonList.php` | `AcademyBasicAdminController.seasonList()` | `jr_season_open` |
| **P1** | **과목(Subject) 관리** | `admin/System/SubjectList.php` | `AcademyBasicAdminController.subjectList()` | |
| **P1** | **과정(Course) 관리** | `admin/System/CourseList_NEW.php` | `AcademyBasicAdminController.courseList()` | |
| **P2** | **강의실(Room) 관리** | `admin/System/RoomList.php` | `AcademyBasicAdminController.roomList()` | |

### 2-2. 강사/홈피 관리 (admin/Homepy)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **강사 목록** | `admin/Homepy/TeacherList.php` | `AcademyAdminController.teacherList()` | |
| **P1** | **강사 프로필** | `admin/Homepy/TeacherProfile.php` | `AcademyAdminController.teacherProfile()` | `SETUP_PROFILE` |

### 2-3. 수강/반 변경 (admin/Lecture 일부)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **반 변경 신청** | `admin/Lecture/ClassChangeRegist.php` | `AcademyAdminController.classChange()` | |
| **P2** | **수강 취소/환불** | `admin/Lecture/LectureRefundRegist.php` | `AcademyAdminController.refund()` | 결제 도메인 협업 필요 |
