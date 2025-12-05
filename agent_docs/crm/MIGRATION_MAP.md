# 📞 CRM Migration Map

## 1. 개요
- **Domain**: CRM (고객관계관리)
- **Description**: 상담 이력, SMS/메일 발송, 쿠폰 관리
- **Base URL**: `/admin/crm` (관리자), `/api/v1/crm` (API)

## 2. 소스/타겟 매핑

| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **SMS 발송(팝업)** | `CRM/popup/sms_send.html` | `CrmController.sendSms()` | `CRM_SMS` 테이블 |
| **P1** | **상담원 목록** | `CRM/admin/coupone/use_list.html` (참조) | `CrmAdminController.managerList()` | `CRM_MANAGER` |
| **P2** | **메일 발송** | `CRM/popup/mail_send.html` | `CrmController.sendMail()` | `CRM_MAIL` |
| **P3** | **쿠폰 관리** | `CRM/admin/coupone/index.html` | `CrmAdminController.couponList()` | `CRM_CP_LIST` |

## 3. 엔티티 (Entity)
`ENTITY_GUIDE.md` 참조.
- `CrmSms`, `CrmMail`
- `CrmManager`, `CrmCoupon`

