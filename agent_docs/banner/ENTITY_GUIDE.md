# 🎨 Banner Entity Guide (배너 엔티티 가이드)

## 1. 개요
배너 시스템은 연도별(`18`, `20`) 또는 용도별(`Main`, `Etc`)로 테이블이 파편화되어 있습니다.
Admin에서는 이를 **통합 관리**하거나, **각각의 엔티티**로 매핑해야 합니다.

## 2. 주요 엔티티

### 2.1. BannerMain18 / BannerMain20 (메인 배너)
- **Legacy Table**: `bannerTotalMain18`, `bannerTotalMain20`
- **Description**: 연도별 메인 배너 정보

| Field Name | Column Name | Type | Description |
|---|---|---|---|
| `id` | `idx` | `Long` | 고유 번호 |
| `section` | `section` | `String` | 배너 위치/섹션 코드 |
| `title` | `title` | `String` | 배너 제목 |
| `imgUrl` | `imgBanner` | `String` | 이미지 경로 |
| `linkUrl` | `link` | `String` | 클릭 시 이동 링크 |
| `isUse` | `use_yn` | `String` | 사용 여부 (Y/N) |
| `sortNo` | `sort` | `Integer` | 정렬 순서 |

### 2.2. SetupBanner (텍스트 배너)
- **Legacy Table**: `SETUP_MAIN_TEXT_BANNER`
- **Description**: 텍스트 형태의 공지 배너

| Field Name | Column Name | Type | Description |
|---|---|---|---|
| `id` | `no` | `Long` | 고유 번호 |
| `content` | `content` | `String` | 배너 내용 |
| `url` | `url` | `String` | 이동 링크 |
| `position` | `position` | `String` | 위치 코드 |

---

## 3. 구현 전략
- **Legacy 호환성**: 100% 호환을 위해, 테이블을 통합(`Migration`)하기보다는 **각 테이블에 맞는 엔티티를 개별 생성**(`Banner2020`, `Banner2018`)하는 것을 권장합니다.
- **인터페이스 활용**: `Banner`라는 공통 인터페이스를 정의하여 서비스 로직의 중복을 줄이십시오.

