# 🔧 Admin - Board Migration Map

## 1. 개요
- **Source Path**: `admin/admin_board_list.php` 외
- **Target Path**: `com.hackers.jrjump.domain.admin.controller.BoardAdminController`

## 2. 매핑
| Priority | 기능 | PHP Source | Java Target |
|:---:|---|---|---|
| **P1** | **게시판 생성/관리** | `admin/admin_board_list.php` | `BoardAdminController.list()` |
| **P2** | **게시판 권한 설정** | `admin/admin_exec_board.php` | `BoardAdminController.grant()` |

