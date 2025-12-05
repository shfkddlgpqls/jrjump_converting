# 📋 Board Migration Map

## 1. 개요
- **Domain**: Board (게시판)
- **Description**: 공지사항, Q&A, 자료실 등 게시판 기능
- **Base URL**: `/board` (사용자), `/admin/board` (관리자)

## 2. 소스/타겟 매핑

| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **게시판 설정** | `admin/admin_board_list.php` | `BoardAdminController.configList()` | 게시판 생성/설정 |
| **P1** | **게시글 목록** | `bbs/zboard.php` | `BoardController.list()` | 동적 테이블 조회 |
| **P2** | **게시글 상세** | `bbs/view.php` | `BoardController.detail()` | 조회수 증가 포함 |
| **P3** | **게시글 쓰기** | `bbs/write.php` | `BoardController.write()` | 파일 업로드 포함 |

## 3. 엔티티 (Entity)
`ENTITY_GUIDE.md` 참조.
- `BoardConfig`
- `BoardArticle` (동적 테이블 처리 필요)

