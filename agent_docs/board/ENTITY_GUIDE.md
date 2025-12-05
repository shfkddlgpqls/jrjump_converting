# 📋 Board Entity Guide (게시판 엔티티 가이드)

## 1. 개요
게시판 시스템은 제로보드(Zetyx) 또는 커스텀 게시판 구조를 따르고 있으며, 게시판 ID별로 테이블이 분리되는 구조(`zetyx_board_free` 등)일 가능성이 높습니다.
JPA 매핑 시 **동적 테이블 전략** 또는 **통합 테이블 전략**이 필요합니다.

## 2. 주요 엔티티

### 2.1. BoardConfig (게시판 설정)
- **Legacy Table**: `zetyx_admin_table` (추정) 또는 `BOARD_ADMIN`
- **Description**: 게시판별 설정 정보 (이름, 권한, 스킨 등)

| Field Name | Column Name | Type | Description |
|---|---|---|---|
| `id` | `no` | `Long` | 게시판 고유 번호 |
| `boardId` | `name` | `String` | 게시판 ID (예: `notice`, `qna`) |
| `title` | `subject` | `String` | 게시판 제목 |
| `readLevel` | `grant_view` | `Integer` | 읽기 권한 레벨 |
| `writeLevel` | `grant_write` | `Integer` | 쓰기 권한 레벨 |

### 2.2. BoardArticle (게시글)
- **Legacy Table**: `zetyx_board_{id}` (동적 테이블)
- **Strategy**:
    - **Option A (JPA)**: 각 게시판별로 Entity를 따로 만듭니다. (`NoticeArticle`, `QnaArticle`)
    - **Option B (JdbcTemplate)**: 동적 쿼리로 처리합니다. (Admin 조회용)
    - **Option C (Union View)**: DB에 View를 생성하여 매핑합니다.

**추천 전략**: Admin에서는 **Option B (JdbcTemplate)**가 유리합니다. (게시판 생성 시마다 Entity를 만들 수 없으므로)

| Field Name | Column Name | Type | Description |
|---|---|---|---|
| `id` | `no` | `Long` | 게시글 번호 |
| `headId` | `headnum` | `Long` | 계층형 게시판 헤드 번호 |
| `author` | `name` | `String` | 작성자 이름 |
| `subject` | `subject` | `String` | 제목 |
| `content` | `memo` | `TEXT` | 내용 |
| `regDate` | `reg_date` | `Integer` | 작성일 (Unix Timestamp) |

---

## 3. 주의사항
- **Unix Timestamp**: 게시판 작성일이 `DATETIME`이 아니라 `INT`(Unix Time)로 저장되는 경우가 많으니 변환(`Instant` 사용)에 주의하십시오.
- **동적 테이블**: 게시판 ID에 따라 테이블명이 바뀌는 구조이므로, `@Table(name="...")`로 고정하기 어렵습니다.

