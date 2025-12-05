# 🎨 Admin View Mapping Guide

## 1. 매핑 규칙
- **구조**: `/admin/{Category}/{File}.php` → `/resources/templates/admin/{category}/{file}.html`
- **케이스**: CamelCase 파일명 → snake_case 파일명 변환 권장.

## 2. 주요 매핑 (Key Mappings)

| PHP Source | Target View | Controller Method |
|---|---|---|
| `admin/System/SeasonList.php` | `admin/system/season_list.html` | `AcademyBasicAdminController.seasonList()` |
| `admin/Homepy/TeacherList.php` | `admin/academy/teacher_list.html` | `AcademyAdminController.teacherList()` |
| `admin/Lecture/MemberList.php` | `admin/member/list.html` | `MemberAdminController.list()` |
| `admin/Banner/BannerMainCateList.php` | `admin/banner/main_list.html` | `BannerAdminController.mainList()` |

## 3. 변환 규칙 (Migration Rules)
- **Static Resources**: `/admin/{css,js}/` → `/static/admin/{css,js}/`
- **Form Action**: `.php` → Thymeleaf URL Expression (`@{/admin/...}`)
- **Popup**: `window.open` 경로 수정 필수.
- **Variable**: `<?=$row['name']?>` → `<span th:text="${row.name}">` (DTO Getter 활용)
