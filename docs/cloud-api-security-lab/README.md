# Cloud & API Security Architecture Lab

[English](./README.en.md) · [프로필](../../README.md)

**Planned · 설계 단계.** 하나의 개인 심화 Lab을 단계적으로 확장하기 위한 계획. 실행 인프라·성공 테스트·보안 제품 연동 결과 없음. 검토일 2026-11-01.

## 범위·아키텍처 상태

| 표시 | 의미·현재 상태 |
| --- | --- |
| Reference Architecture | 외부 공식 참고 구조는 출처 표시. 현재 외부 아키텍처 도면 복제 없음 |
| My Design | 아래 단계별 직접 설계안. 벤더 공식 구조 아님 |
| Implemented Scope | 이 설계 문서만 작성. 실행 구성 없음 |
| Verified Scope | 신규 Lab 검증 없음. 기존 OTTer 사례는 별도 이전 작업 |
| Not Implemented | WAF·Tunnel, AWS 보안 실험, 컨테이너·진단, AI Gateway, Agent 통제 |

## My Design · 제안하는 통제 경계

1. **사용자 경계:** 시험 사용자 A/B·관리자, 소유자가 있는 API 객체, 감사 이벤트 ID
2. **웹 진입점:** Cloudflare WAF·Tunnel 후보 경로. WAF는 선택한 HTTP 요청 필터링 담당. 사용자 인증·소유권은 앱에서 유지
3. **클라우드 경계:** 별도 AWS 단계에서 ALB·WAF, 비공개 앱·DB 경로, 최소 권한 IAM·CloudTrail 실험. 대안 실험 경로이며 모든 제품을 한 경로에 넣는 구조 아님
4. **실행 환경:** 재현 가능한 이미지, 런타임 비밀값 주입, 빌드 비밀값 분리, 취약점 분류·개선
5. **AI 요청:** Cloudflare AI Gateway **또는** LiteLLM 하나부터 선택. 키·모델 권한, 요청 예산, 민감값 제거 로그
6. **Agent 도구:** 허용된 모의 도구, 서버의 사용자·권한 검사, 상태 변경 도구 승인, 프롬프트 인젝션·무권한 요청 시험

## 단계별 완료 기준

| 순서 | 구현할 내용 | Verified 전 필요한 증거 |
| --- | --- | --- |
| 01 웹/API | 세션·인증, 객체 소유권·역할, 입력 검사 | A/B 요청, 정의한 200·401·403·400의 기대·실제 결과, 거절 시 DB 불변, HTTP 로그 |
| 02 Cloudflare | WAF 규칙·Tunnel, 원본 우회 검토 | 같은 정상·거절 요청의 규칙 전후 결과, 이벤트 ID, 원본 직접 요청, 정상 API 회귀 확인 |
| 03 AWS | IAM·VPC·WAF·CloudTrail | 허용·거절 IAM 작업, DB 허용·차단 경로, WAF·CloudTrail 이벤트, 광범위 권한 부여와 구분 |
| 04 Docker | 이미지·비밀정보·취약점 관리 | 이미지 digest, 진단 도구·버전·시각, 분류·개선·재진단, 비밀값 없는 이미지·이력 검사 |
| 05 AI Gateway | 하나 선택, 키·모델·예산 정책 | 정상·거절 요청, 설정 임계값과 실제 집행 비교, 민감 프롬프트 원문 공개 제외 |
| 06 Agent | 도구 권한·Guardrails | 읽기·쓰기 도구 분리, 무권한 실행 거절, 정상 흐름, 프롬프트 인젝션 잔여 한계 |

한 단계 구현·재시험 후 다음 단계 확장. 기존 M1/M3 통제는 참고 입력이며 이 신규 Lab 01~06 구현 증거로 전용하지 않음.

## 구현 시 만들 저장소 구조

- README.md / README.en.md — 개요·현재 범위
- docs/architecture/ — 출처 있는 참고 자료·My Design·설계 결정
- docs/cases/ — Problem → Environment → My Responsibility → Threat/Risk → Analysis → Implementation → Verification → Evidence → Limitations → Next Improvement
- app/ — 최소 시험 API. 팀 앱 로직 변경 불필요
- infra/cloudflare/, infra/aws/, containers/ — 실제 사용 시 설정 추가
- tests/ — 재현 요청·검사·가짜 시험 데이터
- evidence/phase-01/ ~ phase-06/ — 실제 실행만 저장. 성공 예시를 결과처럼 생성 금지

위 경로는 예정 구조이며 기존 파일 링크 아님. 구현 착수 시 별도 개인 저장소로 분리 가능.

## 증거 기록 규칙

커밋·환경/버전·UTC 시각·명령/요청·기대·실제 결과·민감값 제거 출력·되돌리기/정리 기록. 정상·거절 요청을 함께 수집하고 필요한 DB·로그 대조 포함. 실패·미실행 검사도 유지. 세션 쿠키·API 키·PSK·계정 비밀값·개인정보 공개 금지. 비용·기능 사용권·현재 API 문법·정리는 실제 착수 시 재확인.

## 공식 참고 자료

2026-11-01 공식 문서 확인. 참고 문서가 이 설계안의 적합성을 인증하는 것은 아님.

- [Cloudflare WAF](https://developers.cloudflare.com/waf/)
- [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/)
- [AWS Well-Architected Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html)
- [Docker Build secrets](https://docs.docker.com/build/building/secrets/)
- [Cloudflare AI Gateway](https://developers.cloudflare.com/ai-gateway/)
- [LiteLLM Proxy Quick Start](https://docs.litellm.ai/docs/proxy/quick_start)

## 첫 작업

로컬 Phase 01부터 시작. 객체 소유자·사용자 2명과 허용·거절 작업 정의 후 실제 HTTP·DB 결과 수집. 이번 포트폴리오 개편으로 유료 클라우드 자원 생성 없음.
