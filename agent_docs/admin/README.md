# 🔧 Admin Documentation (관리자 가이드)

관리자(Admin) 시스템은 모든 도메인 기능의 집합체입니다.
따라서 단일 문서로 관리하지 않고, **기능별로 분할하여 점진적으로 참조**해야 합니다.

---

## 1. 🤖 Admin 작업 프로토콜 (Workflow)
Admin 작업 시 다음 순서를 반드시 준수하십시오.

1.  **타겟 선정**: 전체를 한 번에 작업하지 말고, `maps/` 폴더 내의 **하나의 맵(Map)**을 선정하여 시작합니다. (예: `maps/ACADEMY.md`)
2.  **엔티티 확인**:
    - Admin은 독립적인 엔티티를 갖지 않고, **각 도메인의 엔티티를 공유**합니다.
    - 예: 학원 관리자 작업 시 `agent_docs/academy/ENTITY_GUIDE.md`를 참조하여 엔티티를 생성/사용합니다.
3.  **구현**: `IMPL_GUIDE.md`의 공통 전략(보안, 레이아웃)을 바탕으로 기능을 구현합니다.

---

## 2. 참조 문서 (Reference)

### 🗺️ Migration Maps (기능별 매핑)
- [Academy (Homepy)](maps/ACADEMY.md): 학원/선생님 관리
- [Banner](maps/BANNER.md): 배너/팝업 관리
- [Board](maps/BOARD.md): 게시판 관리
- [CRM](maps/CRM.md): 고객/상담 관리
- [Member](maps/MEMBER.md): 회원/쿠폰/할인/인증 관리
- [Payment](maps/PAYMENT.md): 결제/매출/정산/환불 관리
- [Common & System](maps/COMMON.md): 시스템 설정, 과정/과목/시즌/반 관리

### ⚙️ Guides
- [Implementation Guide](IMPL_GUIDE.md): Admin 공통 구현 전략 (보안, 권한, 공통 UI)
- [View Mapping Guide](VIEW_MAP.md): PHP View ↔ Thymeleaf 매핑 규칙
- [Analysis Guide](ANALYSIS_GUIDE.md): 소스 분석 가이드
- [Test Guide](TEST_GUIDE.md): 보안 및 컨트롤러 테스트 전략
- [Checklist](CHECKLIST.md): 관리자 기능 검증 리스트

---

## 3. 엔티티 참조 전략 (Entity Strategy)
엔티티 클래스는 **각 도메인 패키지**(`com.hackers.jrjump.domain.*`)에 위치해야 합니다.

- **학원 관리**: `agent_docs/academy/ENTITY_GUIDE.md` 참조
- **CRM 관리**: `agent_docs/crm/ENTITY_GUIDE.md` 참조
- **게시판 관리**: `agent_docs/board/ENTITY_GUIDE.md` 참조
- **배너 관리**: `agent_docs/banner/ENTITY_GUIDE.md` 참조
- **회원 관리**: `agent_docs/member/ENTITY_GUIDE.md` 참조 (예정)
- **결제 관리**: `agent_docs/payment/ENTITY_GUIDE.md` 참조 (예정)
- **강좌 관리**: `agent_docs/lecture/ENTITY_GUIDE.md` 참조 (예정)
