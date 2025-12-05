# JRJump Spring Migration Project

## Project Overview

**WHAT**: PHP 기반 교육 플랫폼(인강/학원/모바일)을 Java Spring Boot로 마이그레이션하는 프로젝트

**WHY**: 레거시 PHP 코드를 현대적인 Java Spring 아키텍처로 전환하여 유지보수성, 확장성, 성능 개선

**HOW**: 모듈 단위로 순차적 마이그레이션 (Backend 우선 → View 후속)

## Technology Stack

### Current (PHP Legacy)
- **PHP 5.4.16** + ionCube (2013년 버전, 보안 지원 종료)
- MySQL Database (EUC-KR charset)
- jQuery / jQuery Mobile 1.2.0
- File-based routing
- 파일 인코딩: EUC-KR

### Target (Java Spring)
- Java 17+ / Spring Boot 3.x
- Spring Data JPA (ORM)
- Spring Security
- Thymeleaf (View - 후순위)

## Project Structure

### Source Repositories
| Repository | Platform | URL Pattern |
|------------|----------|-------------|
| jrjumpi_new | 인강 (Online) | `{domain}/` |
| jrjump | 학원 (Academy) | `{domain}/regi` |
| jrjump-m | 모바일 (Mobile) | `{domain}/m` |

### Spring Module Structure
```
src/main/java/com/jrjump/
├── common/          # 공통 모듈 (유틸, 설정)
├── config/          # Spring 설정
├── platform/        # 플랫폼 구분 (online/academy/mobile)
├── auth/            # 인증/회원 모듈
├── payment/         # 결제 모듈
├── lecture/         # 강의/학습 모듈
├── board/           # 게시판 모듈
├── admin/           # 관리자 모듈
└── event/           # 이벤트 모듈
```

## Key Principles

### Platform Routing
- URL prefix로 플랫폼 구분 (`/`, `/regi`, `/m`)
- 반응형 웹 X → 플랫폼별 별도 뷰 템플릿
- 공통 비즈니스 로직은 Service 계층에서 공유

### Database & ORM
- Spring Data JPA 사용 (필수)
- 필요한 DB 스키마만 Entity로 매핑
- 기존 테이블 구조 최대한 유지

### Migration Priority
1. 인증/회원 모듈 (Auth)
2. 결제 모듈 (Payment)
3. 강의/학습 모듈 (Lecture)
4. 게시판 모듈 (Board)
5. 이벤트 모듈 (Event)
6. 관리자 모듈 (Admin)
7. View 템플릿 (최후순위)

## Working Guidelines

### Before Starting Any Module
1. PHP 소스 코드 분석 완료
2. 관련 DB 스키마 파악
3. 스킬 파일(`.claude/skills/`) 확인

### 개발 순서 (각 모듈별 적용)
```
1. Domain/Entity        → DB 테이블 매핑, 연관관계 설정
       ↓
2. Repository           → JPA Repository 인터페이스
       ↓
3. Service              → 비즈니스 로직 구현
       ↓
4. Controller           → API 엔드포인트 정의
       ↓
5. DTO                  → 요청/응답 객체 정의
       ↓
6. View/Template        → Thymeleaf 템플릿 (최후순위)
       ↓
7. Exception Handler    → 예외 처리 및 에러 응답
       ↓
8. Configuration        → 보안, 설정 등
```

### Coding Standards
- RESTful API 설계
- Service 계층에서 비즈니스 로직 처리
- Repository 패턴 사용
- DTO/Entity 분리

### File References
- 스킬 파일: `.claude/skills/`
- 마이그레이션 진행 상황: `.claude/MIGRATION_TASKS.md`
- 모듈별 상세: `docs/migration/`

## Quick Commands

```bash
# 빌드
./gradlew build

# 테스트
./gradlew test

# 실행
./gradlew bootRun
```

## Important Notes

- pom.xml 사용 금지 (기존 소스 참조용이므로)
- Gradle 빌드 시스템 사용
- View 작업은 모든 Backend 완료 후 진행

### Encoding 주의사항 (중요!)
- **기존 PHP 파일 인코딩: EUC-KR**
- **DB 테이블 Charset: EUC-KR**
- DB 연결 시 반드시 EUC-KR 인코딩 설정 필요
- Spring 프로젝트 소스코드는 UTF-8, DB 통신은 EUC-KR

```yaml
# application.yml - DB 연결 설정 (EUC-KR)
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/jrjump?useUnicode=true&characterEncoding=EUC-KR&useSSL=false&serverTimezone=Asia/Seoul
    hikari:
      connection-init-sql: SET NAMES euckr

  # HTTP 요청/응답은 UTF-8 유지
  http:
    encoding:
      charset: UTF-8
      enabled: true
      force: true
```

#### 인코딩 처리 전략
1. **DB 레이어**: EUC-KR로 통신 (기존 데이터 호환)
2. **애플리케이션 레이어**: UTF-8 (Java 내부)
3. **HTTP 레이어**: UTF-8 (클라이언트 통신)

#### JPA Entity 설정
```java
// 필요시 컬럼별 인코딩 주의
@Column(name = "member_name", columnDefinition = "varchar(100) CHARACTER SET euckr")
private String name;
```

#### 향후 고려사항
- 장기적으로 DB를 UTF-8로 마이그레이션 검토
- 신규 테이블은 UTF-8로 생성 권장