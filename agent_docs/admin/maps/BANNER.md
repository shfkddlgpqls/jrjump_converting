# 🔧 Admin - Banner Migration Map

## 1. 개요
- **Source Path**: `admin/Banner/`
- **Target Path**: `com.hackers.jrjump.domain.admin.controller.BannerAdminController`

## 2. 매핑
| Priority | 기능 | PHP Source | Java Target |
|:---:|---|---|---|
| **P1** | **메인 배너 관리** | `admin/Banner/BannerMainCateList.php` | `BannerAdminController.mainList()` |
| **P2** | **텍스트 배너 관리** | `admin/System/MainTextBanner.php` | `BannerAdminController.textList()` |

