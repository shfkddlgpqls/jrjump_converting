# 🔧 Admin - CRM Migration Map

## 1. 개요
- **Source Path**: `CRM/admin/` (주의: `admin/` 폴더가 아닌 `CRM/` 내부의 admin 폴더임)
- **Target Path**: `com.hackers.jrjump.domain.admin.controller.CrmAdminController`

## 2. 매핑
| Priority | 기능 | PHP Source | Java Target |
|:---:|---|---|---|
| **P1** | **상담원 관리** | `CRM/admin/manager/list.html` (추정) | `CrmAdminController.managerList()` |
| **P2** | **쿠폰 발급 내역** | `CRM/admin/coupone/use_list.html` | `CrmAdminController.couponHistory()` |
| **P2** | **통계(접속/상담)** | `CRM/admin/stats/` | `CrmAdminController.stats()` |

