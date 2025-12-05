# 🔧 Admin - Member Migration Map

## 1. 개요
- **Domain**: Member (회원 관리)
- **Source Path**: `admin/Lecture/` (주의: Lecture 폴더 내에 회원 기능이 혼재됨)
- **Target Controller**: `MemberAdminController`, `CouponAdminController`, `CertAdminController`

---

## 2. 소스/타겟 매핑

### 2-1. 회원 기본 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **회원 목록** | `admin/Lecture/MemberList.php` | `MemberAdminController.list()` | 검색 조건 다수 |
| **P1** | **회원 목록 엑셀** | `admin/Lecture/MemberListExcel.php` | `MemberAdminController.listExcel()` | |
| **P1** | **회원 상세** | `admin/Lecture/MemberInfo.php` | `MemberAdminController.detail()` | |
| **P1** | **회원 수정** | `admin/Lecture/MemberInfoUpd.php` | `MemberAdminController.update()` | |
| **P2** | **회원 등록** | `admin/Lecture/MemberRegist.php`, `MemberWrite.php` | `MemberAdminController.register()` | |
| **P2** | **회원 ID 중복체크** | `admin/Lecture/MemberCheckId.php` | `MemberAdminController.checkId()` | AJAX |
| **P3** | **회원 탈퇴/삭제** | `admin/Lecture/MemberDel.php` | `MemberAdminController.delete()` | |
| **P3** | **회원 관계 설정** | `admin/Lecture/MemberRelation.php`, `MemberRelationChange.php` | `MemberAdminController.relation()` | 가족/연계 회원 |

### 2-2. 수강 관리 (회원별)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **회원 수강 등록** | `admin/Lecture/MemberLectureWrite.php` | `MemberAdminController.registerLecture()` | 복잡한 로직 |
| **P1** | **회원 수강 등록(신규)** | `admin/Lecture/MemberLectureWrite_NEW.php` | `MemberAdminController.registerLectureNew()` | |
| **P2** | **회원 수강 추가** | `admin/Lecture/MemberLectureWriteAdd.php` | `MemberAdminController.addLecture()` | |
| **P2** | **회원 결제 내역** | `admin/Lecture/MemberPay.php` | `MemberAdminController.paymentHistory()` | |
| **P2** | **회원 결제 내역 엑셀** | `admin/Lecture/MemberPayExcel.php` | `MemberAdminController.paymentHistoryExcel()` | |
| **P2** | **시즌별 회원 목록** | `admin/Lecture/SeasonMemberList.php` | `MemberAdminController.seasonList()` | 연도별 버전 다수 |

### 2-3. 쿠폰 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **쿠폰 발급 내역** | `admin/Lecture/MemberCoupon.php` | `CouponAdminController.list()` | |
| **P1** | **쿠폰 등록** | `admin/Lecture/MemberCouponWrite.php`, `MemberCouponRegist.php` | `CouponAdminController.register()` | |
| **P2** | **쿠폰 생성** | `admin/Lecture/MemberCouponCreate.php` | `CouponAdminController.create()` | 대량 생성 |
| **P2** | **생성된 쿠폰 목록** | `admin/Lecture/MemberCouponCreated.php` | `CouponAdminController.createdList()` | |
| **P2** | **생성된 쿠폰 엑셀** | `admin/Lecture/MemberCouponCreatedXls.php` | `CouponAdminController.createdExcel()` | |
| **P2** | **쿠폰 티켓 추가** | `admin/Lecture/MemberCouponAddTicket.php` | `CouponAdminController.addTicket()` | |

### 2-4. 할인(DC) 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **할인 목록** | `admin/Lecture/MemberDc.php` | `DiscountAdminController.list()` | |
| **P2** | **할인 등록/수정** | `admin/Lecture/MemberDcWrite.php`, `MemberDcModify.php`, `MemberDcRegist.php` | `DiscountAdminController.save()` | |
| **P2** | **할인 복사** | `admin/Lecture/MemberDcCopy.php` | `DiscountAdminController.copy()` | |
| **P2** | **할인 타이틀 관리** | `admin/Lecture/MemberDcTitle.php`, `MemberDcTitleWrite.php` | `DiscountAdminController.titleList()` | |

### 2-5. 자격증/인증 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **인증 회원 목록** | `admin/Lecture/MemberCert.php` | `CertAdminController.list()` | |
| **P2** | **인증 등록/수정** | `admin/Lecture/MemberCertWrite.php`, `MemberCertModify.php`, `MemberCertRegist.php` | `CertAdminController.save()` | |
| **P2** | **인증 심사** | `admin/Lecture/MemberCertSimsa.php` | `CertAdminController.review()` | |
| **P2** | **인증 유형 관리** | `admin/Lecture/MemberCertType.php` | `CertAdminController.typeList()` | |
| **P3** | **인증 승인/거부** | `admin/Lecture/MemberCertOk.php`, `MemberCertNo.php` | `CertAdminController.approve()` | |

### 2-6. 기타 회원 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **캐시 관리** | `admin/Lecture/MemberCash.php` | `MemberAdminController.cashList()` | 포인트/캐시 |
| **P2** | **수강료 관리** | `admin/Lecture/MemberFee.php`, `MemberFeeModify.php` | `MemberAdminController.feeList()` | |
| **P2** | **무료교재 수정** | `admin/Lecture/MemberFreeBookModify.php` | `MemberAdminController.updateFreeBook()` | |
| **P3** | **회원쉽 리셋** | `admin/Lecture/MemberShipReset.php` | `MemberAdminController.resetMembership()` | |
| **P3** | **회원 시즌ID 관리** | `admin/Lecture/MemberSeasid.php` | `MemberAdminController.seasonId()` | |
| **P3** | **상담 등록** | `admin/Lecture/MemberConsultReg.php` | `MemberAdminController.registerConsult()` | CRM 연계 |
| **P3** | **댓글 승인** | `admin/Lecture/MemberCommentOk.php` | `MemberAdminController.approveComment()` | |
| **P3** | **선결제 회원** | `admin/Lecture/PrepayMember.php` | `MemberAdminController.prepayList()` | |

---

## 3. 핵심 엔티티 참조
- `Member` → `agent_docs/member/ENTITY_GUIDE.md` (예정)
- `Coupon` → `agent_docs/event/ENTITY_GUIDE.md` (예정)
- `MemberCert` → `agent_docs/member/ENTITY_GUIDE.md` (예정)
- `MemberDiscount` → `agent_docs/payment/ENTITY_GUIDE.md` (예정)

## 4. 주의사항
- `admin/Lecture/` 폴더에 회원, 결제, 강좌 기능이 혼재됨 (레거시 구조)
- Member 관련 파일만 70개 이상 → 단계별 구현 필수
- 쿠폰/할인 로직은 결제(Payment)와 강하게 연결됨
- 시즌별 회원 목록은 연도별로 파일이 분리되어 있음 (통합 필요)

