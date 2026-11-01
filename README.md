<p align="center">
  <img src="./assets/profile-header-ink-coral.svg" alt="EunHye Yoo · Cloud & AI Security" width="100%" />
</p>

<p align="center"><strong>Cloud & AI Security</strong></p>
<p align="center"><a href="./README.en.md">English</a> · <a href="https://app.notion.com/p/3dd1b198732a8059b1b1f2f410f08dc6">Technical Notes</a></p>

보안 솔루션 구축·기술지원과 클라우드 보안 분야를 준비하는 유은혜입니다. Java/Spring으로 REST API를 구현하고 Linux와 AWS에서 서버·네트워크를 구성하며 서비스의 동작과 접근 경로를 익히고 있습니다.

## Projects

### [OTTer Shield](https://github.com/team-blocks-lab/otter-shield) · 진행 중

OTT 서비스를 위한 하이브리드 인프라 구축·보안 검증 팀 프로젝트. **PM, 애플리케이션 개발, M5 캐나다 지사망·AWS 구성 담당.**

**사내 게시판 · REST API 개발과 검증**

- 로그인·로그아웃, 게시글 CRUD, 이미지 첨부 API 및 React 화면 구현
- Postman으로 요청·응답을 확인하고 MySQL 데이터와 대조하여 저장·수정·삭제 검증
- 서버 세션을 이용한 로그인 처리와 미로그인 접근 차단 확인(`401`), 공백 제목 등 잘못된 입력 거절 확인(`400`)
- BCrypt 비밀번호 처리와 게시글 작성자 확인 로직 구현

[API 테스트 보고서·캡처](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m1-intranet/docs/TEST_REPORT.md) · [소스 코드](https://github.com/team-blocks-lab/otter-shield/tree/main/apps/m1-intranet/backend)

**OTT 서비스 · 회원·영상 API 개발**

회원가입·로그인, 공개 영상 조회와 재생 API 구현. 세션 상태와 영상 공개 여부에 따라 응답을 구분하고 로컬에서 API·React 화면 연동 확인.

[구현·검증 자료](https://github.com/team-blocks-lab/otter-shield/tree/main/apps/m3-ott)

**캐나다 지사망·AWS · 보안 실습 확장**

Sophos UTM과 PC 5대의 기본 통신 구성. AWS CloudFormation으로 VPC·서브넷·NAT 구성, EKS 제어 영역 활성화 확인.

현재 담당 파트의 보안 실습을 확장해 VPN 업무 통신과 DB·관리 서비스의 접근 제한을 검증할 계획입니다. AWS에서는 관리 권한과 앱→DB 접근 경로를 점검할 예정입니다.

[M5 기술 기록](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe) · [보안 확장 계획](./docs/security-plans/m5-access-boundaries.md)

### [Full-Stack Integration Lab](https://github.com/Eunhye-yoo/fullstack-integration-lab)

**Linux 서버를 분리하고 웹 요청부터 DB까지 연결한 개인 실습.**

- React·Spring Boot·MySQL을 각각 Ubuntu VM에 배치
- Linux NAT Router, IP Forwarding, MASQUERADE·DNAT, SSH/SCP 구성
- API 응답·브라우저 화면·DB 데이터를 대조하여 전체 연결 확인
- Gateway·DNS·Proxy·DB 접속 설정을 나누어 연결 오류 점검

[3-Tier 실습·검증](https://github.com/Eunhye-yoo/fullstack-integration-lab/tree/main/02-linux-3tier) · [설정 명령어·문제 해결 기록](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175)

### [EduPOP](https://github.com/Eunhye-yoo/EduPOP)

학원 운영·학습 관리 팀 프로젝트. **반 관리, 강사·학생 배정, 대시보드와 개인 성적표 구현 담당.**

반 생성과 다중 강사·학생 매핑, 중복·정원 검사 구현. 반 상세 조회에서는 로그인 사용자의 소속 학원과 조회 대상의 학원을 비교하도록 처리했습니다. Controller–Service–MyBatis–DB로 이어지는 데이터 흐름을 구성했습니다.

[본인 구현·접근통제 검토](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/access-control-review.md) · [포트폴리오 PDF](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/EduPOP_Portfolio_Eunhye_Yoo.pdf) · [시연 영상](https://youtu.be/mkAcPCD7VOY)

## Skills

### 개발·API 검증

<p>
  <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&amp;logo=openjdk&amp;logoColor=white" alt="Java" height="24" />
  <img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&amp;logo=springboot&amp;logoColor=white" alt="Spring Boot" height="24" />
  <img src="https://img.shields.io/badge/MyBatis-415A77?style=flat-square" alt="MyBatis" height="24" />
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&amp;logo=mysql&amp;logoColor=white" alt="MySQL" height="24" />
  <img src="https://img.shields.io/badge/React-20232A?style=flat-square&amp;logo=react&amp;logoColor=white" alt="React" height="24" />
  <img src="https://img.shields.io/badge/JavaScript-B89B00?style=flat-square&amp;logo=javascript&amp;logoColor=white" alt="JavaScript" height="24" />
  <img src="https://img.shields.io/badge/Postman-FF6C37?style=flat-square&amp;logo=postman&amp;logoColor=white" alt="Postman" height="24" />
</p>

REST API · 세션 인증 · 입력 검증 · Postman 요청·응답 확인 · MySQL 데이터 대조

### 인프라·보안

<p>
  <img src="https://img.shields.io/badge/Linux-1B263B?style=flat-square&amp;logo=linux&amp;logoColor=white" alt="Linux" height="24" />
  <img src="https://img.shields.io/badge/SSH%20%2F%20SCP-415A77?style=flat-square&amp;logo=gnubash&amp;logoColor=white" alt="SSH / SCP" height="24" />
  <img src="https://img.shields.io/badge/Routing%20%2F%20NAT-415A77?style=flat-square" alt="Routing / NAT" height="24" />
  <img src="https://img.shields.io/badge/Sophos%20UTM-1B263B?style=flat-square&amp;logo=sophos&amp;logoColor=white" alt="Sophos UTM" height="24" />
  <img src="https://img.shields.io/badge/AWS-1B263B?style=flat-square&amp;logo=amazonwebservices&amp;logoColor=white" alt="AWS" height="24" />
</p>

- **Linux · SSH:** 원격 서버 접속, 앱·DB 서버 분리, 연결 오류 점검
- **Routing · NAT:** IP Forwarding, MASQUERADE·DNAT, 서버 간 통신 경로 확인
- **Sophos UTM:** OPS·CONTENT·MGMT 구역 분리와 기본 통신 구성
- **AWS:** VPC·서브넷·NAT, EKS 클러스터용 IAM Role 설정

[Cloud & API Security Lab 학습 계획](./docs/cloud-api-security-lab/README.md)

## Certifications

- **네트워크관리사 2급** — 취득
- **정보처리기사** — 필기 합격
- **리눅스마스터 2급** — 1차 합격

## Technical Notes & English

GitHub에는 소스와 API 검증 자료를, [Notion](https://app.notion.com/p/3dd1b198732a8059b1b1f2f410f08dc6)에는 인프라 설정·명령어·문제 해결 과정을 기록합니다.

캐나다 유학·해외생활, 경영학 전공과 영어 교육 경험이 있습니다. 영문 기술문서를 읽고 영어로 소통하는 데 이 경험을 활용하고 있습니다.
