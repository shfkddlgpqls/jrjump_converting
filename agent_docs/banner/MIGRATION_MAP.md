# 🎨 Banner Migration Map

## 1. 개요
- **Domain**: Banner (배너)
- **Description**: 메인/서브 페이지의 배너 및 팝업 관리
- **Base URL**: `/admin/Banner` (관리자), `/` (사용자 노출)

## 2. 소스/타겟 매핑

| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **메인 배너 목록** | `admin/Banner/BannerMainCateList.php` | `BannerAdminController.list()` | 연도별 테이블 조회 |
| **P1** | **배너 등록/수정** | `admin/Banner/BannerMainReMod20.php` | `BannerAdminController.save()` | 이미지 업로드 필수 |
| **P2** | **텍스트 배너** | `admin/System/MainTextBanner.php` | `BannerAdminController.textBannerList()` | `SETUP_MAIN_TEXT_BANNER` |
| **P3** | **배너 노출(API)** | `layer_banner_new.php` | `BannerController.getLayerBanner()` | 사용자단 API |

## 3. 엔티티 (Entity)
상세 내용은 `ENTITY_GUIDE.md` 참조.
- `BannerMain20`, `BannerMain18`
- `SetupBanner`

