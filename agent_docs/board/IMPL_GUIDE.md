# 📋 Board Implementation Guide

## 1. 동적 테이블 전략 (Dynamic Table Strategy)
- **JdbcTemplate 사용**: 게시판 ID(`free`, `notice`)에 따라 테이블명이 바뀌므로, JPA Entity보다는 `JdbcTemplate`을 사용하여 쿼리를 동적으로 생성하는 것이 유리합니다.
- **SQL 예시**:
  ```java
  String sql = "SELECT * FROM zetyx_board_" + boardId + " WHERE ...";
  ```

## 2. 데이터 처리
- **Unix Timestamp**: 작성일이 `int(11)` Unix Time인 경우, `Instant.ofEpochSecond()`로 변환하여 처리합니다.
- **계층형 게시판**: 답글(Reply) 기능을 위해 `headnum`, `step` 컬럼의 정렬 로직을 원본과 동일하게 구현해야 합니다.

