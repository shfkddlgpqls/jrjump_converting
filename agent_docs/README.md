# 📚 Agent Documentation (도메인별 개발 가이드)

이 디렉토리는 각 도메인별 상세 개발 가이드 문서를 포함하고 있습니다.

---

## 🤖 Agent 작업 프로토콜 (Workflow)
Agent는 반드시 아래 **순서대로(Step-by-Step)** 작업을 진행해야 하며, 각 단계 완료 후 사용자의 **승인(Confirm)**을 받아야 합니다.

1.  **🕵️‍♀️ 1단계: 분석 (Analysis)**
    - 참조: `ANALYSIS_GUIDE.md`, `MIGRATION_MAP.md`
    - 목표: 원본 PHP 소스를 읽고 비즈니스 로직과 쿼리를 파악한다.
2.  **🏗️ 2단계: 설계 (Entity)**
    - 참조: `ENTITY_GUIDE.md`, `MIGRATION_MAP.md`
    - 목표: 분석된 내용을 바탕으로 JPA Entity 클래스를 생성한다.
3.  **⚙️ 3단계: 구현 (Implementation)**
    - 참조: `IMPL_GUIDE.md`
    - 목표: Service, Repository, Controller 코드를 구현한다.
4.  **✅ 4단계: 검증 (Test)**
    - 참조: `TEST_GUIDE.md`, `CHECKLIST.md`
    - 목표: JUnit 테스트를 작성하고 체크리스트를 검증한다.

---

## 🌐 Common (공통)
- [Enum Guide](common/ENUM_GUIDE.md): PHP 하드코딩 값을 Java Enum으로 변환하는 전략
- [Entity Relationship](common/ENTITY_RELATION.md): 도메인 간/내부 엔티티 관계 설정 원칙 (중요)
- [API Standard](common/API_STANDARD.md): API 공통 응답 포맷 및 예외 처리 규격

## 🔧 Admin (관리자)
- [Index & Protocol](admin/README.md): Admin 작업 시작 전 필독
- [Implementation Guide](admin/IMPL_GUIDE.md): Admin 공통 구현 전략
- [Analysis Guide](admin/ANALYSIS_GUIDE.md): Admin 소스 분석 가이드
- [Checklist](admin/CHECKLIST.md): 관리자 기능 검증 리스트
- [Academy Map](admin/maps/ACADEMY.md): 학원 관리
- [Banner Map](admin/maps/BANNER.md): 배너 관리
- [Board Map](admin/maps/BOARD.md): 게시판 관리

## 🏫 Academy (학원)
1. **[Analysis Guide](academy/ANALYSIS_GUIDE.md)**: 원본 PHP 소스 분석 방법 & 체크포인트
2. **[Migration Map](academy/MIGRATION_MAP.md)**: PHP 소스 ↔ Java 타겟 매핑 정보
3. **[Entity Guide](academy/ENTITY_GUIDE.md)**: DB 테이블 구조 및 엔티티 설계 명세
4. **[Implementation Guide](academy/IMPL_GUIDE.md)**: 서비스/컨트롤러 구현 핵심 전략
5. **[Test Guide](academy/TEST_GUIDE.md)**: JUnit5 테스트 코드 작성 가이드
6. **[Checklist](academy/CHECKLIST.md)**: 구현 완료 여부 검증 리스트

## 📞 CRM (고객관리)
- [Entity Guide](crm/ENTITY_GUIDE.md): CRM 테이블 및 엔티티 설계
- [Analysis Guide](crm/ANALYSIS_GUIDE.md): 소스 분석 가이드
- [Migration Map](crm/MIGRATION_MAP.md): 매핑 정보
- [Implementation Guide](crm/IMPL_GUIDE.md): 구현 가이드
- [Checklist](crm/CHECKLIST.md): 검증 체크리스트

## 📋 Board (게시판)
- [Entity Guide](board/ENTITY_GUIDE.md): 게시판 구조 및 동적 테이블 전략
- [Analysis Guide](board/ANALYSIS_GUIDE.md): 소스 분석 가이드
- [Migration Map](board/MIGRATION_MAP.md): 매핑 정보
- [Implementation Guide](board/IMPL_GUIDE.md): 구현 가이드
- [Checklist](board/CHECKLIST.md): 검증 체크리스트

## 🎨 Banner (배너)
- [Entity Guide](banner/ENTITY_GUIDE.md): 배너 테이블 및 파편화 대응 전략
- [Analysis Guide](banner/ANALYSIS_GUIDE.md): 소스 분석 가이드
- [Migration Map](banner/MIGRATION_MAP.md): 매핑 정보
- [Implementation Guide](banner/IMPL_GUIDE.md): 구현 가이드
- [Checklist](banner/CHECKLIST.md): 검증 체크리스트

## 👤 Member (회원)
- *작성 예정*

## 🎓 Lecture (강좌)
- *작성 예정*

## 💳 Payment (결제)
- *작성 예정*

---
> **Note**: 모든 가이드 문서는 **HumanLayer**의 `Less is More` 및 `Progressive Disclosure` 원칙을 준수합니다.
