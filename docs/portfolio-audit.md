# Portfolio Evidence Audit · 2026-11-01

보안 중심 문서 개편의 근거·변경 범위. [Profile KR](../README.md) · [Profile EN](../README.en.md)

## 검토 기준 / Review Basis

실제 소스·등록 캡처·보고서·Issue·경로별 Git 이력·연결 Notion 대조. 앱·DB·클라우드에 새 요청을 실행한 감사 아님. 작성자·담당 기록은 기여 근거이며 런타임 성공 증거와 구분.

Static code, registered evidence, reports, issues, path-specific Git history, and linked Notion notes were compared. No application, database, or cloud runtime was retested.

| 대상 / Item | 개인 기여 근거 / Attribution | 확인 범위 / Scope |
| --- | --- | --- |
| OTTer M1 | [2b4cbd2](https://github.com/team-blocks-lab/otter-shield/commit/2b4cbd2ddfbdb918657c15532b849e197ea87abe), [9c03ee0](https://github.com/team-blocks-lab/otter-shield/commit/9c03ee07743d74c16c5686c77cf8e3203dddc486), [Issue 8](https://github.com/team-blocks-lab/otter-shield/issues/8) | 인증·입력·작성자 검사 소스, TEST_REPORT, 401·공백 제목 400 캡처 직접 확인. API 403 미검증 |
| OTTer M3 | [d3772bc](https://github.com/team-blocks-lab/otter-shield/commit/d3772bc550681d1f05f5a7f31b86f6a3f9cfc9b7), [PR 42](https://github.com/team-blocks-lab/otter-shield/pull/42) | 인증·영상·재생 소스, Evidence 목록, PRIVATE 재생 본문 404 직접 확인. 미디어 원본 차단 미검증 |
| M5·PM | [WBS](https://github.com/team-blocks-lab/otter-shield/blob/main/WBS.md), [Issue 34](https://github.com/team-blocks-lab/otter-shield/issues/34), [Issue 12](https://github.com/team-blocks-lab/otter-shield/issues/12), [Notion](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe) | UTM·PC 5대 기본 통신, VPC/NAT 스택·EKS ACTIVE 기록. VPN·노드 Ready·RDS·ALB 미검증 |
| EduPOP | [반 생성](https://github.com/Eunhye-yoo/EduPOP/commit/f7b5083a10cd2ef95925ed4b2f19118004e1d031), [매핑](https://github.com/Eunhye-yoo/EduPOP/commit/ab91c0b9e85dfa215b5cb67489bcb500d51f7317) | Controller·Service·DTO·SQL·SecurityConfig 대조. 학원 소유권 검사가 경로별 상이 |
| Full-Stack Lab | [3-Tier](https://github.com/Eunhye-yoo/fullstack-integration-lab/tree/main/02-linux-3tier), [Notion](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175) | 네트워크·프록시·DB 경로·명령·장애 기록 대조. 방화벽 비활성화 실습 조건 보존 |

Notion M5는 상단 요약의 EKS 생성 중 표기와 본문의 후속 ACTIVE 기록이 달라, 본문 최종 상세 기록을 채택. 노드 조회 '데이터 사용 불가'와 Pod 미배포 상태는 유지. 원본 캡처 전부의 시각 검수나 현재 AWS 상태 조회는 수행하지 않음.

M5's detailed later ACTIVE record takes precedence over its older summary. Node readiness and pod deployment remain unverified. Not all source screenshots or live AWS resources were inspected.

## 제외한 주장 / Excluded Claims

- 상용 보안 운영·글로벌 AWS 티켓 처리 경력 / Commercial security operations or global AWS support work
- 팀 전체 인프라·DR·Wazuh 성과의 개인 귀속 / Personal ownership of all team infrastructure, DR, or Wazuh work
- M1 API 403 성공, 모든 EduPOP 객체 인가 완료 / Verified M1 API 403 or complete EduPOP object authorization
- VPN·EKS 앱·RDS·CDN 보호·AI 자막 생성 완료 / Completed VPN, EKS apps, RDS, media protection, or AI subtitle generation
- WAF·LiteLLM·Agent Security 숙련, CISSP/AWS 고급 자격 취득 / Product proficiency or unearned advanced certifications

## 변경 파일·이유 / Changes and Rationale

- Profile README.md / README.en.md: 보안 방향·증거 우선, 기술 상태 4단계, 자격·영어 배경 구분
- assets/profile-header-ink-coral.svg: 기존 디자인·색상 보존, 문구만 변경
- docs/security-cases/: M1·M3 개인 사례 2건, 한영 동일 검증 경계
- docs/cloud-api-security-lab/: 신규 심화 포트폴리오 설계·단계별 검증 기준
- EduPOP README 2종·docs/access-control-review 2종: 개인/팀 기여와 객체 접근 검사 한계 명시
- Full-Stack README 2종: 인프라 기초와 보안 강화 실적 구분
- OTTer 팀 저장소: 읽기만 수행, README·다른 팀원 자료·소스 변경 없음

## 기타 개인 저장소 / Other Personal Repositories

study_log, springBoot_practice, react_practice, servlet_practice의 README 검토. 수업·미완성 코드를 대표 보안 실적으로 승격하지 않음. public-apis-4Kr는 외부 API 목록 성격으로 대표 선정 제외. business-data-lab은 목록의 size 0으로 표시되며 공개 대표 프로젝트로 사용하지 않음. 기타 저장소 전체 소스 감사는 범위 밖.

## 검증 한계 / Review Limits

문서의 상태·링크 대상·이미지 경로·Markdown 구조 점검 대상. 소스 변경·빌드·런타임 재검증 없음. 공개 프로필 UI의 bio·핀 설정은 API 도구로 변경하지 않음. 한영 README의 프로젝트·응답 코드·한계·자격 상태를 맞춤.

후속 우선순위: M1 두 사용자 403 + DB 불변 → M3 HTTP 상태줄·MP4 직접 접근 → M5 VPN·AWS 경계의 정상/거절 시험.

## 최신 방향 반영 / Updated Focus

팀원의 보안 성과 대신 본인 M5 접근 경계를 심화. [개인 확장 계획](./security-plans/m5-access-boundaries.md) / [English plan](./security-plans/m5-access-boundaries.en.md). 기존 앱 사례는 직접 구현한 기초로 유지하고 앞으로의 정책·검증은 Planned로 구분.
