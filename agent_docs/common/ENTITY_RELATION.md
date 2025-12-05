# 🔗 Entity Relationship Strategy (엔티티 관계 전략)

## 1. 도메인 간 결합 (Cross-Domain)
MSA 전환 및 모듈 독립성을 위해 **타 도메인 엔티티 직접 참조(`@ManyToOne`)를 엄격히 금지**합니다.
- **Policy**: 오직 **Logical ID**(`Long memberId` 등)만 저장합니다.
- **Reason**: 레거시 DB의 강한 결합을 끊고, 향후 서비스 분리를 용이하게 하기 위함입니다.

## 2. 도메인 내 결합 (Inner-Domain)
같은 도메인 패키지 내(`AcademySeason` ↔ `AcademyCalendar`)에서는 **JPA 연관관계 사용을 권장**합니다.

## 3. Fetch 전략 & N+1
- **Default**: 모든 연관관계는 `FetchType.LAZY`를 기본으로 합니다.
- **Optimization**: `QueryDSL`의 `fetchJoin()`을 사용하여 N+1 문제를 해결합니다.

## 4. Legacy Constraints
- **No Foreign Key**: 레거시 DB에는 물리적 FK가 거의 없습니다.
- **Action**: JPA Entity에서 `@JoinColumn` 사용 시 `foreignKey = @ForeignKey(ConstraintMode.NO_CONSTRAINT)` 옵션을 필수로 적용하여 DDL 자동 생성 시 오류를 방지합니다.
