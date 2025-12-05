# 🔧 Admin - Payment Migration Map

## 1. 개요
- **Domain**: Payment (결제, 매출, 정산, 카드사)
- **Source Path**: `admin/Lecture/`
- **Target Controller**: `PaymentAdminController`, `SalesAdminController`, `ReceiptAdminController`

---

## 2. 소스/타겟 매핑

### 2-1. 수강 접수 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **수강 접수 현황** | `admin/Lecture/ReceiptList.php` | `ReceiptAdminController.list()` | 다양한 검색 조건 |
| **P1** | **접수 현황 엑셀** | `admin/Lecture/ReceiptListExcel.php` | `ReceiptAdminController.listExcel()` | |
| **P1** | **접수 현황 SMS** | `admin/Lecture/ReceiptListSms.php` | `ReceiptAdminController.sendSms()` | SMS 발송 |
| **P2** | **접수 삭제** | `admin/Lecture/ReceiptDel.php` | `ReceiptAdminController.delete()` | |

### 2-2. 결제 내역 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **오늘 결제 목록** | `admin/Lecture/TodayPayList.php` | `PaymentAdminController.todayList()` | |
| **P1** | **결제 결과 조회** | `admin/Lecture/PayResult.php` | `PaymentAdminController.result()` | |
| **P1** | **결제 결과 처리** | `admin/Lecture/PayResultAction.php` | `PaymentAdminController.resultAction()` | |
| **P2** | **수강 취소** | `admin/Lecture/LectureReceiptCancel.php` | `PaymentAdminController.cancelReceipt()` | |

### 2-3. 환불 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **환불 등록** | `admin/Lecture/LectureRefundRegist.php` | `RefundAdminController.register()` | |
| **P1** | **환불 등록 (PG)** | `admin/Lecture/LectureRefundRegist_PG.php` | `RefundAdminController.registerPG()` | PG사 연동 |
| **P2** | **환불 처리** | `admin/Lecture/_LectureRefund.php` | `RefundAdminController.process()` | 내부 처리 |
| **P2** | **환불 요청** | `admin/Lecture/_LectureRefundRequest.php` | `RefundAdminController.request()` | |

### 2-4. 강좌 변경/수정
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **강좌 이력** | `admin/Lecture/LectureHistory.php` | `LectureAdminController.history()` | |
| **P2** | **강좌 목록** | `admin/Lecture/LectureList.php` | `LectureAdminController.list()` | |
| **P2** | **강좌 수정** | `admin/Lecture/LectureModify.php` | `LectureAdminController.modify()` | |
| **P2** | **강좌 수정 등록** | `admin/Lecture/LectureModifyRegist.php` | `LectureAdminController.modifyRegist()` | |
| **P2** | **반 변경 등록** | `admin/Lecture/ClassChangeRegist.php` | `LectureAdminController.classChange()` | |
| **P2** | **온라인 강좌 수정** | `admin/Lecture/LectureOnlineMod.php` | `LectureAdminController.modifyOnline()` | |
| **P2** | **강좌 등록** | `admin/Lecture/LectureRegist.php`, `LectureWrite.php` | `LectureAdminController.register()` | |

### 2-5. 매출/정산 (Sales)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P1** | **일별 매출 집계** | `admin/Lecture/DailyReport.php` | `SalesAdminController.dailyReport()` | **복잡한 쿼리** |
| **P1** | **일별 매출 (계산Ver)** | `admin/Lecture/DailyReportCalcVer.php` | `SalesAdminController.dailyReportCalc()` | |
| **P1** | **일별 매출 엑셀** | `admin/Lecture/DailyReport_Excel.php`, `DailyReportCalcVer_Excel.php` | `SalesAdminController.dailyReportExcel()` | |
| **P2** | **월별 매출 집계** | `admin/Lecture/Sales.php` | `SalesAdminController.monthlyReport()` | |
| **P2** | **일별 매출 상세** | `admin/Lecture/_SalesDay.php` | `SalesAdminController.salesDay()` | |
| **P2** | **월별 매출 상세** | `admin/Lecture/_SalesMonth.php` | `SalesAdminController.salesMonth()` | |
| **P2** | **PG사 리포트** | `admin/Lecture/DacomReport.php` | `SalesAdminController.pgReport()` | 다날(Dacom) |
| **P2** | **PG사 리포트(시험)** | `admin/Lecture/DacomReportExam.php` | `SalesAdminController.pgReportExam()` | |

### 2-6. 카드사/은행 관리
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P2** | **카드사 목록** | `admin/Lecture/CardList.php` | `CardAdminController.list()` | |
| **P2** | **카드사 목록 엑셀** | `admin/Lecture/CardListExcel.php` | `CardAdminController.listExcel()` | |
| **P2** | **카드사 수수료 관리** | `admin/Lecture/CardCompanyCommission.php` | `CardAdminController.commissionList()` | |
| **P3** | **은행 목록** | `admin/Lecture/BankList.php` | `BankAdminController.list()` | |

### 2-7. 마켓 시트 (Market Sheet)
| Priority | 기능 | PHP Source | Java Target | 비고 |
|:---:|---|---|---|---|
| **P3** | **마켓 시트** | `admin/Lecture/Market_sheet.php` | `MarketAdminController.sheet()` | |
| **P3** | **마켓 시트 회원** | `admin/Lecture/Market_sheet_member.php` | `MarketAdminController.memberSheet()` | |
| **P3** | **마켓 시트 매출** | `admin/Lecture/Market_sheet_sales_process.php` | `MarketAdminController.salesProcess()` | |
| **P3** | **마켓 시트 환불** | `admin/Lecture/Market_sheet_refund_process.php` | `MarketAdminController.refundProcess()` | |
| **P3** | **마켓 시트 시즌** | `admin/Lecture/Market_sheet_seasid.php` | `MarketAdminController.seasonSheet()` | |

---

## 3. 핵심 엔티티 참조
- `Payment` → `agent_docs/payment/ENTITY_GUIDE.md` (예정)
- `Receipt` → `agent_docs/payment/ENTITY_GUIDE.md` (예정)
- `Refund` → `agent_docs/payment/ENTITY_GUIDE.md` (예정)
- `CardCompany` → `agent_docs/payment/ENTITY_GUIDE.md` (예정)
- `Bank` → `agent_docs/payment/ENTITY_GUIDE.md` (예정)

## 4. 주의사항
- **DailyReport**: 매출 집계 쿼리가 매우 복잡함. 원본 쿼리 분석 필수
- **PG 연동**: `dacom/` 폴더의 LG U+ 연동 로직과 함께 분석 필요
- **Market Sheet**: 레거시 정산 시스템. 현재 사용 여부 확인 필요
- **환불 PG vs 일반**: PG사 환불과 수기 환불 로직이 분리됨
- 결제 관련 파일 35개 이상 → 단계별 구현 필수

