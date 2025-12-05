# 🌐 Common Enum Strategy (공통 코드 관리 전략)

이 문서는 PHP 레거시 코드의 하드코딩된 값(매직 넘버/스트링)을 Java Enum으로 변환하는 정책 가이드입니다.

---

## 1. 변환 정책 (Policy)

### 1.1. 매직 넘버/스트링 제거
- PHP의 `1`, `Y`, `eng` 등 의미가 불분명한 값은 반드시 **Java Enum**으로 정의하여 사용한다.
- **Boolean 대체**: `Y`/`N` 값은 `boolean` 필드보다는 `YnType` 등의 Enum 사용을 권장한다. (확장성 고려)

### 1.2. JPA AttributeConverter 필수 사용
- DB에는 레거시 값(`1`, `eng`)을 그대로 저장하고, Entity에서는 Enum 객체로 다뤄야 한다.
- 모든 Enum은 JPA `AttributeConverter`를 구현하여 `autoApply = true`로 설정한다.
- **절대 Entity 필드에 String 타입으로 레거시 코드를 직접 매핑하지 않는다.**

---

## 2. 적용 대상 (Candidates)

아카데미 도메인에서 우선 적용해야 할 항목들입니다.

| 도메인 | 컬럼명 | 설명 | 예시 값 | Java Enum 명 |
|---|---|---|---|---|
| Common | `is_use`, `main_status` | 사용여부 | `Y`, `N` | `YnType` |
| Academy | `course_type` | 강좌 구분 | `eng`, `jap`... | `CourseType` |
| Academy | `vod_type` | 영상 타입 | `youtube`, `jw` | `VodType` |
| Member | `level` | 회원 등급 | `1`, `2`, `9` | `MemberLevel` |
