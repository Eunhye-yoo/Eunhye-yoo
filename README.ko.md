<p align="center">
  <img src="./assets/profile-header-ink-coral.svg" alt="EunHye Yoo profile header" width="100%" />
</p>

<p align="center">
  <strong>요구사항부터 애플리케이션과 인프라까지, 직접 구현·구성하고 검증한 내용을 기록합니다.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Requirements-FF5D5D?style=flat-square" alt="Requirements" />
  <img src="https://img.shields.io/badge/Applications-0D1B2A?style=flat-square" alt="Applications" />
  <img src="https://img.shields.io/badge/Infrastructure-1B263B?style=flat-square" alt="Infrastructure" />
  <img src="https://img.shields.io/badge/Verification-415A77?style=flat-square" alt="Verification" />
</p>

<p align="center">
  <a href="./README.md">English</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/team-blocks-lab/otter-shield">OTTer Shield · 진행 중</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Eunhye-yoo/EduPOP">EduPOP</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Eunhye-yoo/fullstack-integration-lab">Full-Stack Lab</a>
  &nbsp;·&nbsp;
  <a href="https://app.notion.com/p/Infrastructure-Lab-3dd1b198732a8059b1b1f2f410f08dc6?source=copy_link">Infrastructure Lab</a>
</p>

---

## 01 · About

**요구사항, 애플리케이션, 데이터, 서버·네트워크 환경**이 하나의 시스템으로 연결되는 과정을 실습하고 있습니다. EduPOP에서는 서비스 요구사항을 구체화하고 반 관리·분석 기능을 구현했으며, Full-Stack Integration Lab에서는 React–API–MySQL 연동과 Linux VM 간 Routing/NAT 통신을 검증했습니다.

IT 분야로 전환하기 전에는 교육 현장에서 강사·학생·일정·고객 요구를 조율했습니다. 이러한 경험을 요구사항 분석과 프로젝트 협업에 활용하며, 직접 구현·구성하고 검증한 내용을 중심으로 기록합니다.

---

## 02 · Selected Work

### [OTTer Shield · 한국·캐나다 OTT 인프라·보안 컨설팅](https://github.com/team-blocks-lab/otter-shield) · 진행 중

> **Team Blocks가 NetBlocks의 역할로 OTTer의 한국·캐나다 하이브리드 인프라 구축과 보안 개선을 계획하는 5인 팀 프로젝트**

- **현재 단계 — 2026.10:** 기획·설계 준비. 계획서·역할 안내·WBS·초기 작업 Issue를 마련했으며, 실제 구축·보안 검증은 착수 전입니다.
- **담당 역할:** PM으로 일정·범위·협업 조율, 캐나다망·VPN 및 OTT·AI 애플리케이션 개발 담당. 서비스 인프라·배포는 다른 팀원이 담당합니다.
- **검증 계획:** 5개 보안 시나리오의 개선 전후 비교와 정상 서비스·앱 복구·DB 복원 확인.

[팀 저장소](https://github.com/team-blocks-lab/otter-shield) · [프로젝트 계획서](https://github.com/team-blocks-lab/otter-shield/blob/main/plans/project-plan-v0.3.pdf) · [개인 담당 범위](https://github.com/team-blocks-lab/otter-shield/blob/main/design/network-guides/m5-canada-cloud.md)

### [EduPOP](https://github.com/Eunhye-yoo/EduPOP)

> **학원 운영과 시험 결과를 다음 수업·학습 사이클로 연결하는 교육 플랫폼**

`Java` `Spring Boot` `MyBatis` `MySQL`

- **문제·요구사항 정의** — 초기 아이디어를 제안하고 학원 운영 및 학습상의 요구를 서비스 흐름과 핵심 기능으로 구체화
- **반 운영 기능 구현** — 반 생성·수정, 수강생·다중 강사 배정, 중복·정원 검증, 반 상태를 통한 종강 처리
- **수업 전 대시보드** — 반·학생별 성취도와 취약 영역 신호를 제공해 ‘수업 전 3분 확인’이라는 사용 목표를 지원
- **개인 성적표** — 성적 추이와 강점·취약 영역을 시각화하고, 분석 로직을 월간 성적표 코드에서 재사용

> **구현 범위:** ‘3분’은 측정 결과가 아닌 사용 목표입니다. 배정·접근 검증은 경로마다 차이가 있고, 학부모용 성적표 공유 링크는 미완성입니다.

[프로젝트 README](https://github.com/Eunhye-yoo/EduPOP) · [서비스 기획·구현 포트폴리오 (PDF · 17쪽)](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/EduPOP_Portfolio_Eunhye_Yoo.pdf) · [Demo Video](https://youtu.be/mkAcPCD7VOY)

### [Full-Stack Integration Lab](https://github.com/Eunhye-yoo/fullstack-integration-lab)

> **Frontend · Backend · Database · Linux Server · Network 경로를 연결하는 통합 실습**

`React` `Spring Boot` `MyBatis` `MySQL` `Linux` `Routing/NAT`

- **Application Integration** — React → Vite Proxy → Spring Boot → MyBatis → MySQL CRUD 흐름 검증 및 환경별 Datasource/API 설정 수정
- **Linux 3-Tier** — React · Spring Boot · MySQL을 Ubuntu VM으로 분리하고 Static IP 및 Remote DB Access 구성
- **Network Extension** — Linux NAT Router, IPv4 Forwarding, MASQUERADE, SSH/SCP, DNAT Port Forwarding 구성 후 Windows → Router → React → Spring Boot → MySQL 전체 경로 검증

- **Express API** — 업로드한 Express 소스에서 Query·Path·JSON Body 처리와 GET/POST/PUT/DELETE 응답 흐름 확인. PUT/DELETE는 DB 미연동 학습용 응답.

[GitHub Repository](https://github.com/Eunhye-yoo/fullstack-integration-lab) · [3-Tier 구축 상세 기록 (Notion)](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175) · [Infrastructure Lab 목록](https://app.notion.com/p/Infrastructure-Lab-3dd1b198732a8059b1b1f2f410f08dc6?source=copy_link)

---

## 03 · Tech Stack

### Application & Data
![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1.0-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring MVC](https://img.shields.io/badge/Spring%20MVC-6DB33F?style=flat-square&logo=spring&logoColor=white)
![MyBatis](https://img.shields.io/badge/MyBatis%20Starter-4.0.1-000000?style=flat-square)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-005F0F?style=flat-square&logo=thymeleaf&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white)

![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)

버전 배지는 EduPOP 기준. 통합 Lab과 학습 예제의 Java·Spring Boot·MyBatis Starter 버전은 각 저장소 설정을 기준으로 확인합니다.

### Infrastructure & Network
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![VMware](https://img.shields.io/badge/VMware-607078?style=flat-square)
![Routing/NAT](https://img.shields.io/badge/Routing%20%2F%20NAT-415A77?style=flat-square)
![SSH/SCP](https://img.shields.io/badge/SSH%20%2F%20SCP-475569?style=flat-square)

**인프라 구축 기록:** [Linux 3-Tier + NAT Router (Notion)](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175) — VM 구성, Network/Routing/NAT, 명령어, 검증 및 Troubleshooting

**애플리케이션 검증:** [3-Tier 연동 및 CRUD (GitHub)](https://github.com/Eunhye-yoo/fullstack-integration-lab/tree/main/02-linux-3tier)

**별도 AWS 실습:** EC2/VPC/ALB (Linux httpd, Windows IIS, Bastion Host)

**현재 학습 중:** Docker · LLM/생성형 AI 활용

### Tools
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![IntelliJ IDEA](https://img.shields.io/badge/IntelliJ%20IDEA-000000?style=flat-square&logo=intellijidea&logoColor=white)

---

## 04 · Practice & Study

| Repository | 학습·실습 내용 |
| --- | --- |
| [Spring Boot Practice](https://github.com/Eunhye-yoo/springBoot_practice) | Spring MVC · Thymeleaf · Interceptor/AOP · JPA · QueryDSL |
| [React Practice](https://github.com/Eunhye-yoo/react_practice) | JavaScript · 컴포넌트 · Hooks · Router · 상태 관리 |
| [Servlet Practice](https://github.com/Eunhye-yoo/servlet_practice) | Servlet · JSP · JDBC · Session · 요청 흐름 |
| [Study Log](https://github.com/Eunhye-yoo/study_log) | Network · Routing · Server · IT 기초 |

---

## 05 · Certifications

- **네트워크관리사 2급** — 취득
- **정보처리기사** — 필기 합격
- **리눅스마스터 2급** — 필기 합격

