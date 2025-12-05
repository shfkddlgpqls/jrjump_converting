# 📋 Board Test Guide (게시판 테스트 가이드)

## 1. Test Strategy
게시판 도메인은 **동적 테이블 쿼리**와 **파일 처리** 검증이 핵심입니다.

### 1.1. Repository Test (Dynamic Query)
- **Table Injection**: `QueryDSL` 또는 `Native Query` 사용 시, 테이블명 치환(`zetyx_board_{id}`)이 SQL Injection 없이 올바르게 수행되는지 검증.
- **Pagination**: 레거시 페이징(`page`, `limit`) 로직이 Spring `Pageable`과 정확히 매핑되는지 확인.

### 1.2. Service Logic Test
- **Secret Post**: 비밀글(`is_secret`) 조회 시 권한 체크 로직 검증.
- **File Attachment**: 업로드된 파일 경로가 레거시 규칙(`/files/board/...`)을 준수하는지 확인.

## 2. Key Scenarios
- **댓글 계층 구조**: 계층형 댓글(답글)의 정렬 순서(`ref`, `step`)가 PHP와 동일하게 유지되는지 검증.
- **조회수 증가**: 게시글 조회 시 조회수(`hit`) 증가 로직 검증.

