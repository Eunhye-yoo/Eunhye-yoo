# M5 · 개인 담당 범위의 보안 확장 계획

[English](./m5-access-boundaries.en.md) · [프로필](../../README.md)

**Planned / My Design.** 직접 담당하는 캐나다 지사망·AWS를 하나의 접근 경계 보안 사례로 심화하기 위한 설계. 공격·차단·정책 변경 완료 결과 없음. 검토일 2026-11-01.

## Problem

통신 성공만으로 적절한 접근통제를 판단할 수 없음. 캐나다 업무 사용자의 본사 서비스 접근 범위, 시험용 DB·관리 화면 직접 접근 필요성, AWS 관리 주체를 구체적으로 정의할 필요.

## Environment · 현재 기준선

[기존 M5 기술서](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe) · [M5 담당](https://github.com/team-blocks-lab/otter-shield/issues/34) · [AWS 담당](https://github.com/team-blocks-lab/otter-shield/issues/12).

- **기록된 실습:** Sophos UTM의 OPS·CONTENT·MGMT 독립 가상망, PC 5대, Gateway·DNS·TCP 기본 시험. CloudFormation VPC·NAT, EKS 제어 영역 ACTIVE
- **미완료:** 지사 간 VPN 성립, 구역 간 허용·차단 시험, Worker Ready·앱 Pod·ALB·HTTPS·RDS, 보안 변경 전후 비교
- Private Subnet 배치만으로 접근 경계 검증 완료를 주장하지 않음

## My Responsibility

M5 시험 설계, UTM5 정책 범위, 본인 담당 AWS 자원, 증거 수집·분석·재시험. M1 피어·반환 경로·VPN과 M3 격리 시험용 DB는 해당 담당과 협의 필요. 다른 팀원의 Wazuh·M1/M2 정책·M3 클러스터·M4 백업을 개인 성과로 사용하지 않음.

## Threat / Risk

과도한 VPN 대역·허용 규칙, 업무 PC의 불필요한 DB·관리 서비스 접근, EKS 관리 API의 넓은 접근 범위, 과도한 AWS 권한, 공개·광범위 DB 노출 가능성. **점검할 가설이며 확인된 취약점 아님.**

## Analysis · 제안 접근 행렬

정책 적용 전 실제 목적지와 업무 요구 확정.

| 출발지·주체 | 목적지 | 제안 정책 | 검증 조건 |
| --- | --- | --- | --- |
| M5 OPS 시험 PC | 합의한 M1 업무 Web·DNS | 실제 필요한 포트만 허용 | DNS 정상 응답·웹 기능 확인. TCP 연결만으로 완료하지 않음 |
| M5 OPS·CONTENT PC | 가짜 데이터의 격리 Test DB | 기준선 확인 후 직접 접근 거절 | 실제 수신 중인 목적지·클라이언트 거절·해당 정책 로그 |
| M5 OPS·CONTENT PC | UTM 관리 화면 | 명시적 허가 외 거절 | MGMT 정상 대조군·업무 PC 거절 |
| 허용된 M5 관리 주체·출발지 | EKS 관리 API | 출발지·IAM/Kubernetes 권한 최소화 | 허용 주체/출발지 성공·미허용 주체/출발지 실패 |
| AWS 앱 Workload | 시험 DB | 필요한 앱 경로만 허용 | 앱 쿼리 성공·무관한 출발지 거절 |
| 외부·업무 PC | AWS DB | 직접 접근 거절 | 실제 Endpoint 상태·경로 확인. 시험을 위해 공개하지 않음 |

정확한 IP·포트·주체·정책·허용 응답은 확정 전. Any→Any 허용이나 실제 계정 공격 없이 시험 가능.

## Implementation · 앞으로 적용할 순서

### A. 정상 기준선 확보

1. UTM WAN·인터페이스·라우트와 M1 피어 도달성·반환 경로 실측. 라우터 Ping 성공과 VPN 종단 도달 구분
2. VPN SA(터널 협상 상태) 확인 후 합의한 DNS·웹 업무의 필요한 양방향 동작 확인. 비밀값 제거 로그 확보
3. 담당자와 격리된 가짜 데이터 DB 준비. 허용 대조군에서 실제 포트 수신·쿼리 성공 확인
4. 현재 접근부터 시험. 이미 업무 PC 접근이 거절된다면 통제 검증으로 기록. 취약점을 만들기 위해 허용 범위를 넓히지 않음

### B. 본인 범위의 최소 접근 정책

1. UTM5 설정 백업·되돌리기 절차 기록
2. 출발지·목적지·서비스 객체와 정상 업무 허용 정의. 업무 PC의 DB·관리 경로 제한. 규칙 순서·VPN Selector·NAT 동작 확인
3. 한 번에 하나의 변경 적용. 정책 ID·전후 차이·시각·방향 기록
4. 정상 업무·금지 접근·허용 대조군 재시험. Timeout만으로 방화벽 차단 성공이라 판단하지 않음

### C. 같은 검증 방식을 AWS로 확장

1. 현재 자원 상태·소유 범위 확인. 앱→DB 시험 전 노드 Ready·앱·DB 배포 선행
2. 허용 관리 출발지와 IAM 주체 정의. EKS Endpoint 설정과 인증·인가를 분리 점검
3. 최소 권한의 앱→DB Security Group 경로 설계. 기준선 생성을 위해 DB 공개 금지
4. 작은 시험용 IAM Role로 허용 작업·거절 작업 정의. 권한 판정과 감사 이벤트 기록. CloudTrail의 실제 이벤트 수집 여부 확인 후 증거로 사용
5. WAF는 HTTPS 정상화 뒤 선택할 HTTP 필터링 실험. 앱 소유권·DB·망 정책을 대체하지 않음

## Verification · 남길 시험 결과

| 시험 | 정책 적용 후 기대 | 실제 |
| --- | --- | --- |
| 허용된 업무 요청 | 서비스까지 정상 동작 | 미실행 |
| 업무 PC→Test DB 직접 접근 | 의도한 정책에 따른 거절 | 미실행 |
| 허용 대조군→같은 DB | 정상 동작 | 미실행 |
| 업무 PC→UTM 관리 화면 | 거절·허용 관리 경로 유지 | 미실행 |
| 허용/미허용 AWS 주체 | 정의한 허용/거절 | 미실행 |
| 앱→DB / 무관한 출발지 | 허용 / 거절 | 미실행 |
| 되돌리기·정상 동작 복구 | 복구 가능 | 미실행 |

출발지 별칭/IP·목적지/포트·시각/시간대·요청·기대/실제 결과·관련 로그/이벤트/정책 ID·버전/설정 차이 기록. 비밀값·쿠키 가림. 실패 원인을 라우팅·서비스 수신 상태·NAT·서버 로그와 대조한 뒤 보안 통제로 귀속.

## Evidence · 수집 예정

UTM 규칙 전후·일치 로그, VPN SA·업무 요청, Test DB 수신/대조군 쿼리·거절 요청, AWS Endpoint·SG·IAM 설정, 감사 이벤트, 정상 회귀·되돌리기. 실제 결과만 저장하고 완료 후 Case Study에서 연결. GitHub는 구현·핵심 증거, Notion은 상세 설정·명령 기록.

## Limitations

현재 토폴로지에 바로 적용할 명령어를 작성한 문서 아님. 실제 Endpoint·팀 간 경계·권한·현재 설정 확인이 구현 전제. VPN·노드·앱·DB 준비가 선행 과제. 위험 감소 수치·공격 차단 실적 없음.

## Completion Criteria

**내 변경 → 정상 요청 성공 → 금지 요청이 의도한 원인으로 실패 → 일치 로그 → 재시험·복구**를 추적 가능. 여러 미검증 제품 나열보다 직접 담당한 사례 하나의 완결성을 우선.

## Next Improvement

VPN 기준선과 업무 PC→Test DB 정책 사례 1건부터 완성. 이후 AWS IAM 또는 SG 경계에 같은 증명 방식 적용. WAF·컨테이너·AI Gateway·Agent는 [장기 심화 Lab](../cloud-api-security-lab/README.md) 순서로 확장.
