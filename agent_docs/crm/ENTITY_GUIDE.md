# 📞 CRM Entity Guide (엔티티 설계 가이드)

## 1. 개요
CRM(고객관계관리) 도메인은 상담 이력, SMS/메일 발송, 쿠폰 관리 등을 담당합니다.
주로 `CRM_` 접두어가 붙은 테이블을 사용합니다.

---

## 2. 주요 엔티티 상세

### 2.1. CrmManager (상담원/관리자)
- **Legacy Table**: `CRM_MANAGER`
- **Description**: CRM 시스템 접근 가능한 상담원 정보

| Field Name | Column Name | Type | Constraints | Description |
|---|---|---|---|---|
| `id` | `MG_NO` | `Long` | PK | 관리자 번호 |
| `name` | `MG_NAME` | `String` | | 관리자 이름 |
| `dept` | `MG_DEPT` | `String` | | 부서명 |
| `level` | `MG_LEVEL` | `String` | | 권한 레벨 |

### 2.2. CrmSms (SMS 발송 이력)
- **Legacy Table**: `CRM_SMS`
- **Description**: 고객에게 발송된 SMS 내역

| Field Name | Column Name | Type | Constraints | Description |
|---|---|---|---|---|
| `id` | `SMS_NO` | `Long` | PK | 발송 번호 |
| `sender` | `SMS_SENDER` | `String` | | 발신 번호 |
| `receiver` | `SMS_RECEIVER` | `String` | | 수신 번호 |
| `content` | `SMS_CONTENT` | `String` | TEXT | 내용 (EUC-KR 주의) |
| `regDate` | `SMS_REGDATE` | `LocalDateTime` | | 발송 일시 |
| `result` | `SMS_RESULT` | `String` | | 발송 결과 (성공/실패) |

### 2.3. CrmCounselType (상담 유형)
- **Legacy Table**: `CRM_COU_TYPE`
- **Description**: 상담 분류 코드 (전화상담, 방문상담 등)

| Field Name | Column Name | Type | Constraints | Description |
|---|---|---|---|---|
| `id` | `COU_T_NO` | `Long` | PK | 유형 번호 |
| `name` | `COU_T_NAME` | `String` | | 유형 명칭 |

---

## 3. 연관 관계 및 주의사항

### 3.1. Member 연동
- `CRM_SMS` 등은 회원 테이블(`jrjump_member_table`)과 직접 FK가 맺어져 있지 않을 수 있습니다.
- 보통 `user_id`나 `phone` 번호로 느슨하게 연결됩니다.
- Entity에서 `@ManyToOne`으로 회원을 참조하기보다, 필요 시 Service에서 조회하는 것을 권장합니다.

