<p align="center">
  <img src="./assets/profile-header-ink-coral.svg" alt="EunHye Yoo · Cloud & AI Security" width="100%" />
</p>

<p align="center"><strong>Cloud & AI Security Engineering을 목표로, 코드와 통신 경로에서 보안 통제를 확인하고 검증 기록을 남깁니다.</strong></p>
<p align="center"><a href="./README.en.md">English</a> · <a href="./docs/security-cases/m1-session-validation.md">M1 보안 사례</a> · <a href="./docs/security-cases/m3-playback-control.md">M3 보안 사례</a> · <a href="./docs/cloud-api-security-lab/README.md">심화 Lab 계획</a></p>

개발·인프라를 약 6개월 학습한 IT 경력전환자 유은혜입니다. Java/Spring 애플리케이션 구현과 Linux 네트워크 실습을 바탕으로 **보안 솔루션 구축·기술지원, 클라우드 보안, 웹/API 보안** 직무를 준비하고 있습니다. 장기 목표는 AI Security Architect입니다.

## 01 · Security Focus

- **인증·세션:** 서버 세션 기반 로그인·로그아웃, 미인증 요청 거절 및 HTTP 응답 확인
- **입력·데이터 경계:** 입력 검증과 객체 소유권 검사 코드 분석, 구현된 경로와 미검증 경로 구분
- **네트워크·접근 경로:** Linux 3-Tier, Routing/NAT·DNAT·SSH, 애플리케이션에서 DB까지 계층별 연결 확인

이 포트폴리오의 Verified는 **기존 실행 기록과 코드가 뒷받침하는 범위**입니다. 상용 보안 시스템 운영 경력을 의미하지 않습니다. 문서 검토 기준: 2026-11-01.

## 02 · 직접 구현한 보안 기초

### [M1 · 세션 인증과 잘못된 요청 거절](./docs/security-cases/m1-session-validation.md)

사내 게시판 인증·입력 검사 구현 및 로컬 API 검증. 로그인·세션 조회 `200`, 로그아웃 `204`, 이후 게시글 조회 `401`, 공백 제목·허용되지 않은 익명 등록 `400` 기록.

**내 기여:** 로그인·게시글 API와 React 화면 개발·자체 검증. 타인 글 변경 거절 코드는 있지만 `403` API 시험은 미완료.

[테스트 보고서](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m1-intranet/docs/TEST_REPORT.md) · [401 캡처](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m1-intranet/docs/evidence/08-unauthorized-401.png)

### [M3 · 공개 상태와 로그인에 따른 재생 API 통제](./docs/security-cases/m3-playback-control.md)

OTT 로그인·세션 및 PUBLIC 영상 조회·재생 API 구현. 잘못된 로그인·로그아웃 이후 세션 조회 `401`, PRIVATE 영상 상세·재생 `404` 기록.

**검증 경계:** API의 재생 URL 반환 제한과 실제 MP4 파일 접근통제는 별개. CDN 파일 보호·서버 배포·AI 자막 생성은 미검증.

[검증 목록](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m3-ott/docs/evidence/README.md) · [구현 커밋](https://github.com/team-blocks-lab/otter-shield/commit/d3772bc550681d1f05f5a7f31b86f6a3f9cfc9b7)

## 03 · 앞으로 집중할 보안 과제

**M5의 VPN·AWS 접근 경계를 직접 설계·시험하는 사례로 심화할 계획입니다.** 현재 남아 있는 연결·배포 검증부터 완료한 뒤, 허용된 업무 요청과 거절해야 할 DB·관리 요청을 같은 조건에서 비교합니다.

[개인 보안 실습 상세 계획](./docs/security-plans/m5-access-boundaries.md) — 위협·담당 범위·접근 행렬·변경 전후 시험·증거·완료 기준. **Planned이며 완료 실적 아님.**

## 04 · Projects

### [OTTer Shield](https://github.com/team-blocks-lab/otter-shield) · 주력 / 진행 중

5인 팀의 OTT 환경 구축·보안 검증 프로젝트.

- **직접 담당:** PM 일정·Issue 조율, M1 게시판·M3 OTT 앱 개발·로컬 검증, M5 캐나다 지사망·AWS 구성
- **실습 기록:** Sophos UTM·PC 5대 기본 통신, AWS CloudFormation VPC·NAT 구성, EKS 제어 영역 ACTIVE 기록
- **개인 범위 경계:** 다른 팀원의 망 보안·서버 배포·관제·백업 성과는 개인 실적에서 제외
- **남은 범위:** VPN 성립·왕복 통신, EKS 노드 Ready·앱 배포, RDS·ALB·HTTPS 및 보안 개선 후 재시험

[M5 기술 기록](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe) · [개인 기여·근거 목록](./docs/portfolio-audit.md)

### [Full-Stack Integration Lab](https://github.com/Eunhye-yoo/fullstack-integration-lab) · 인프라 기초

React–Spring Boot–MySQL을 Ubuntu VM으로 분리. Linux NAT Router·IP Forwarding·MASQUERADE·DNAT와 SSH/SCP 구성, API·DB·브라우저 결과 대조. **서버 간 통신과 접근 경로를 이해하기 위한 실습**이며 공격 차단·방화벽 강화 성과로 해석하지 않습니다.

[3-Tier 구현·검증](https://github.com/Eunhye-yoo/fullstack-integration-lab/tree/main/02-linux-3tier) · [명령어·장애 분석](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175)

### [EduPOP](https://github.com/Eunhye-yoo/EduPOP) · 애플리케이션 보조 프로젝트

반 생성, 다중 강사·학생 매핑, 반 상세 조회의 학원 소유권 확인, 입력·중복·정원 검사와 대시보드·개인 성적표 구현. **수정·배정 등 모든 경로에 동일한 소유권 검사가 적용된 것은 아닙니다.** Spring Security·OAuth·공통 로그인은 팀 기능으로 구분합니다.

[코드 기준 기여·한계](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/access-control-review.md) · [기존 포트폴리오 PDF](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/EduPOP_Portfolio_Eunhye_Yoo.pdf) · [시연](https://youtu.be/mkAcPCD7VOY)

## 05 · Core Skills

- **Verified · 실행 증거:** Java/Spring 세션·입력 검사 API, Postman HTTP 응답, React/API/MySQL 연결 — 위 M1·M3 사례와 3-Tier Evidence
- **Hands-on · 구성 경험:** Linux·SSH/SCP·Routing/NAT·DNAT, Sophos 기본망, AWS VPC·NAT·CloudFormation·EKS 제어 영역 — 노드·앱 운영 검증과 구분
- **Learning · 학습 중:** 웹/API 인증·인가(사용자와 허용 작업 확인), 클라우드 접근 경계, LLM API 연동
- **Planned · 구현 예정:** Cloudflare WAF·Tunnel → AWS IAM·WAF·CloudTrail 보안 실험 → Docker 이미지·비밀정보 점검 → AI Gateway 또는 LiteLLM → Agent 도구 권한·Guardrails

Java·Spring Boot·JPA/MyBatis·MySQL·React는 구현 기반 기술입니다. 제품별 보안 숙련도를 의미하지 않습니다. [심화 Lab 설계·완료 기준](./docs/cloud-api-security-lab/README.md)

## 06 · Certifications

- **취득:** 네트워크관리사 2급
- **시험 단계 합격:** 정보처리기사 필기 / 리눅스마스터 2급 1차
- **장기 검토 목표·미취득:** CISSP, AWS Security – Specialty, AWS Solutions Architect – Professional. CISSP 경력 인정 여부 미확정

## 07 · Technical Documentation

**GitHub:** 소스·API·애플리케이션 검증 Evidence. **Notion:** 환경·설정 명령어·네트워크·Troubleshooting.

[Infrastructure Lab](https://app.notion.com/p/3dd1b198732a8059b1b1f2f410f08dc6) · [Linux 3-Tier](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175) · [OTTer M5](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe)

기초 학습 저장소: [Spring Boot](https://github.com/Eunhye-yoo/springBoot_practice) · [React](https://github.com/Eunhye-yoo/react_practice) · [Servlet](https://github.com/Eunhye-yoo/servlet_practice) · [Study Log](https://github.com/Eunhye-yoo/study_log). 수업 예제·미완성 미션은 대표 보안 실적과 구분합니다.

## 08 · English Communication

캐나다 유학·해외생활과 경영학 전공, 영어 교육 경험을 바탕으로 영문 기술문서 이해와 영어 의사소통에 활용 가능한 배경 보유. 글로벌 협업·영문 기술지원 직무에 연결하고자 하며, 해외 기술지원·AWS 티켓 처리 경력은 없습니다.
