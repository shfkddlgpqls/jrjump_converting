# 📞 CRM Test Guide (CRM 테스트 가이드)

## 1. Test Strategy
CRM 도메인은 **외부 시스템 연동(SMS, Mail)**과 **이력 로깅**의 안전성 검증이 핵심입니다.

### 1.1. External Service Mocking
- **Mocking**: SMS/Mail 발송 테스트 시, **절대로 실제 발송이 일어나지 않도록** Mock 객체(`@MockBean`)를 사용해야 합니다.
- **Validation**: 발송 요청 파라미터(수신번호, 내용, 발신자)가 레거시 스펙(`__sendSMS`)과 일치하는지 검증.

### 1.2. Logging Test
- **Log Table**: 발송 시도 후 `LOG_SMS`, `CRM_MAIL_LOG` 테이블에 이력이 정확히 적재되는지 검증.

## 2. Key Scenarios
- **개인정보 마스킹**: 로그 저장 시 주민번호, 상세 주소 등 민감 정보가 마스킹 처리되는지(또는 레거시 정책을 따르는지) 확인.
- **발송 실패 처리**: 외부 API 연동 실패 시 예외가 전파되지 않고(Fail-safe) 에러 로그가 남는지 확인.

