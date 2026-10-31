# Security Case Study · M1 세션 인증·입력 검증

[English](./m1-session-validation.en.md) · [프로필](../../README.md)

상태: 로컬 보안 통제 구현·검증. 취약점 발견·수정 사례 아님. 검토일 2026-11-01 / 원본 시험 기록 2026-10-28.

## Problem
유효한 직원 세션이 없는 게시판 요청과 잘못된 게시글 입력 거절 필요.

## Environment
개발 PC: Java 21 · Spring Boot 4.1.1 · MySQL 8.0.46 · React. API localhost:8080. M1/M2 서버 배포 검증과 구분.

## My Responsibility
로그인·게시글 API, React 연동, 로컬 테스트 설계·구현. 서버·망 배포는 M1/M2 담당. [개발 커밋](https://github.com/team-blocks-lab/otter-shield/commit/2b4cbd2ddfbdb918657c15532b849e197ea87abe) · [연동 커밋](https://github.com/team-blocks-lab/otter-shield/commit/9c03ee07743d74c16c5686c77cf8e3203dddc486).

## Threat / Risk
미로그인 접근, 타인 글 변경, 잘못된 데이터 저장 가능성. 설계 시 고려한 위험이며 실제 공격 성공을 주장하지 않음.

## Analysis
서버 세션에서 사용자 식별 → 입력 검사 → 게시글 소유권 확인 필요. 화면의 버튼 숨김과 서버의 권한 검사를 별도로 판단.

## Implementation
- AuthController: 로그인 전 기존 세션 폐기, LOGIN_EMPLOYEE_ID 저장, 로그아웃 시 세션 무효화
- LoginInterceptor: /api/post 및 /api/post/**의 세션·직원 존재·최초 설정 상태 확인
- AuthService: BCrypt 비밀번호 비교, 최초 설정 시 새 비밀번호 해시 저장, UTF-8 72바이트 초과 검사
- PostService: 수정·삭제 전 작성자 확인. 단위 테스트 소스에 FORBIDDEN 및 원문 유지·삭제 미호출 검사
- DB 비밀값 환경변수 참조, HttpOnly·SameSite=Lax·세션 30분 설정. 전체 비밀정보 관리·CSRF 방어 완료를 의미하지 않음

## Verification

| 요청·조건 | 기대 | 기존 실제 결과 |
| --- | --- | --- |
| POST /api/auth/login; GET /api/auth/me | 200 | 보고서·캡처 200 |
| POST /api/auth/logout | 204 | 보고서·캡처 204 |
| 로그아웃 후 GET /api/post | 401 | 캡처의 401 직접 확인 |
| 공백 제목 POST /api/post | 400 | 캡처의 400·title 오류 직접 확인 |
| 점심 게시글 익명 등록 | 400 | 보고서·캡처 등록 |
| 다른 직원의 수정·삭제 | 403·데이터 불변 | 구현·단위 테스트 소스 확인 / API 실행 NOT VERIFIED |

기존 개발 PC 실행 기록 검토이며 이번 문서 개편에서 새로 실행한 시험 결과가 아님.

## Evidence
- [테스트 보고서](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/docs/TEST_REPORT.md)
- [401 캡처](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/docs/evidence/08-unauthorized-401.png) / [400 캡처](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/docs/evidence/06-blank-title-400.png)
- [AuthController](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/auth/AuthController.java) / [AuthService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/auth/AuthService.java)
- [Interceptor](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/auth/LoginInterceptor.java) / [WebConfig](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/config/WebConfig.java)
- [PostService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/post/PostService.java) / [단위 테스트 소스](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/test/java/com/otter/intranet/post/PostServiceTest.java)
- [환경 설정](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/resources/application.properties)

## Limitations
타인 요청 403 API 캡처, 서버 재시험, 세션 쿠키·TLS 검사, CSRF 방어, 반복 로그인 공격, 비밀정보 이력 감사 미검증. 테스트 묶음의 성공 화면만으로 현재 개별 테스트 전부의 통과를 확정하지 않음. 공격 전후 비교 증거 없음.

## Next Improvement
로컬 직원 계정 2개로 본인 글 수정 성공 → 타인 수정·삭제 403 → DB 불변 확인. Method·세션 사용자 별칭·작성자·시각·커밋·DB 비교 기록. 비밀번호·쿠키는 가림 처리. 이후 대상 서버에서 401·400·403 및 정상 동작 재시험.
