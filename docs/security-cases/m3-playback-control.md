# Security Case Study · M3 재생 API의 접근 경계

[English](./m3-playback-control.en.md) · [프로필](../../README.md)

상태: 로컬 보안 통제 구현·검증. 취약점 발견·수정 사례 아님. 검토일 2026-11-01.

## Problem
영상 공개 상태와 로그인 사용자에 따른 상세·재생 정보 제공 제한 필요.

## Environment
개발 PC: Java 21 · Spring Boot 4.1.2 · MySQL 8.0.46 · React 19.3.0. Backend 기본 8081 / 캡처의 UI·Proxy localhost:5175.

## My Responsibility
OTT 인증·영상·재생 API, React 연동, 로컬 테스트 구현. 서비스망·서버 배포는 M3 담당. [구현 커밋](https://github.com/team-blocks-lab/otter-shield/commit/d3772bc550681d1f05f5a7f31b86f6a3f9cfc9b7).

## Threat / Risk
영상 ID 직접 요청을 통한 PRIVATE 정보 조회, 미인증 사용자에게 재생 URL 반환 가능성. 미디어 파일 직접 접근은 별도 위험.

## Analysis
인증은 회원 식별, 공개 상태 확인은 요청 객체의 조회 범위 제한. 두 검사만으로 미디어 원본·CDN 접근통제까지 보장하지 않음.

## Implementation
AuthController에서 로그인 시 기존 세션 교체·로그아웃 시 무효화. AuthService에서 BCrypt 해시 저장·세션 회원의 DB 존재 확인. VideoService에서 PUBLIC만 조회. PlaybackService에서 회원 확인 후 PUBLIC 영상을 조회하고 URL 반환. 비공개·없는 영상은 404 응답으로 통일.

## Verification

| 조건 | 기대 | 기존 실제 결과 |
| --- | --- | --- |
| 잘못된 로그인 | 401 | 캡처 등록 |
| 로그아웃 후 세션 조회 | 401 | 캡처 등록 |
| PRIVATE 상세·재생 | 404 | 캡처 등록 / 재생 응답 본문 직접 확인 |
| 잘못된 페이지 요청 | 400 | 캡처 등록 |
| 미로그인 재생 | 401 | 개발 기록 있음 / 별도 캡처 없음 |
| 세션 없이 MP4 직접 요청 | 정책에 따른 거절 | NOT VERIFIED |

재생 캡처는 JSON 본문의 status 404를 보여주며 HTTP 상태줄은 표시하지 않음. 이번 검토는 기존 기록 대조이며 API 재실행 아님.

## Evidence
- [검증 목록](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/README.md)
- [로그인 오류](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/07-login-invalid-401.png) / [로그아웃 후 세션](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/09-session-after-logout-401.png)
- [PRIVATE 상세](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/13-private-detail-404.png) / [PRIVATE 재생](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/14-private-playback-404.png)
- [AuthService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/auth/AuthService.java) / [VideoService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/video/VideoService.java)
- [PlaybackService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/video/PlaybackService.java) / [VideoController](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/video/VideoController.java)

## Limitations
실제 MP4·CDN 접근통제, 역할·구독 권한 전체, 다중 Pod 세션, 서버 배포, AI 자막 생성 미검증. 환경변수 참조만으로 비밀정보 수명주기 관리 완료를 주장하지 않음.

## Next Improvement
로그인·미로그인 × PUBLIC·PRIVATE·없는 영상의 요청별 HTTP 상태줄 확보. API와 원본·CDN 직접 요청 결과 비교. 재생 요구사항에 맞춰 원본 보호·만료 URL 통제를 선정한 뒤 정상 재생과 우회 요청을 함께 시험.
