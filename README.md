# EunHye Yoo

**서비스의 요구를 기능으로 구체화하고, 데이터·API·서버 흐름까지 연결해 이해하는 개발자**

사용자의 업무 흐름을 관찰하고 필요한 기능을 구조화하는 데 익숙합니다. 교육 현장에서 사람과 업무를 조율해 온 경험을 바탕으로, IT 프로젝트에서도 **기획 → 데이터 구조 → API → 서버 로직 → 실제 기능**이 어떻게 연결되는지 이해하며 개발하고 있습니다.

Java·Spring Boot·MyBatis·MySQL을 기반으로 웹 애플리케이션을 개발하고 있으며, Linux·Docker·네트워크·서버 환경도 함께 학습하고 있습니다.

> **관심 분야**  기술 중심 서비스/IT 기획 · Java/Spring 기반 웹 개발 · 서비스와 기술을 함께 이해하는 역할

---

## 01 · About

- 사용자의 요구를 기능과 데이터 흐름으로 구체화
- 화면에서 끝나지 않고 API·Service·DB까지 연결해 구조 파악
- 기존 기능의 재사용과 기능 간 데이터 흐름을 고려한 설계
- AI를 활용해 프로젝트 구조를 정리하되, 실제 코드와 DB를 직접 확인해 교차 검증

---

## 02 · Tech Stack

### Languages
![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square)

### Backend & Web
![Servlet](https://img.shields.io/badge/Servlet-000000?style=flat-square)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1.0-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring MVC](https://img.shields.io/badge/Spring%20MVC-6DB33F?style=flat-square&logo=spring&logoColor=white)
![MyBatis](https://img.shields.io/badge/MyBatis-4.0.1-000000?style=flat-square)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)

### Frontend & Data Visualization
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-005F0F?style=flat-square&logo=thymeleaf&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white)

### Database & Tools
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![IntelliJ IDEA](https://img.shields.io/badge/IntelliJ%20IDEA-000000?style=flat-square&logo=intellijidea&logoColor=white)

### Learning
Linux · Docker · Network & Server · REST API · Web Architecture · Cloud Infrastructure basics · React

---

## 03 · Selected Project

### EduPOP

**시험 결과를 다음 수업과 학습으로 연결하는 교육 플랫폼**

Java · Spring Boot · MyBatis · MySQL 기반 팀 프로젝트

**아이디어 제안 · 서비스 기획 · 핵심 기능 설계 및 구현**

- **3분 수업 보완 대시보드**
  - 반 평균과 전체 평균 비교
  - 반 전체 취약 유형 분석
  - 학생별 오답률·취약 유형 확인
  - 학생 상태를 위험 신호로 시각화하여 다음 수업의 보완 포인트 제공

- **개인 성적 분석**
  - 영역별 성취도와 추이 분석
  - 강점/취약 영역 시각화
  - 분석 결과를 다른 팀원의 월간 학생 리포트에서도 재사용할 수 있도록 내부 API/메서드 구조 구성

- **반 생성 및 학생·교사 배정**
  - 반 생성 및 정보 관리
  - 복수 교사 배정
  - 학생 배정·변경
  - 중복 배정 방지 및 과거 데이터 보호를 고려한 상태 관리

- 프로젝트 전체 흐름을 이해하기 위해 다른 팀원의 기능과 코드도 함께 확인하고, 발표 과정에서 서비스의 데이터 흐름을 설명

[EduPOP Repository](https://github.com/Eunhye-yoo/EduPOP) · [Demo Video](https://youtu.be/mkAcPCD7VOY)

---

## 04 · How I Work

### 기능을 구현하기 전에 데이터 흐름부터 확인합니다.

요구사항을 기능 단위로 나눈 뒤, 실제 코드와 DB 구조를 확인하면서 다음 흐름을 따라갑니다.

**화면 → Controller → Service → Mapper/Repository → DB → 응답**

AI를 활용해 ERD·Class Diagram·코드 흐름을 정리할 때도 제안 내용을 그대로 사용하지 않고 실제 코드와 DB를 다시 확인합니다.

### 한 기능만이 아니라 연결된 기능까지 확인합니다.

EduPOP에서는 개인 성적 분석 데이터를 특정 화면에서만 사용하는 대신, 다른 팀원의 월간 학생 리포트에서도 활용할 수 있도록 내부 API/메서드 구조를 구성했습니다.

기능을 추가할 때도 **중복 구현을 줄이고 기존 데이터를 다른 기능에서 어떻게 재사용할 수 있는지** 함께 확인하는 편입니다.

---

## 05 · Certifications

- **네트워크관리사 2급** — 취득
- **정보처리기사** — 필기 합격
- **Linux Master 2급** — 필기 합격

---

## 06 · Portfolio & Study

### Portfolio
EduPOP 프로젝트의 서비스 기획, 기능 설계, 데이터 흐름, 구현 내용을 정리했습니다.

- [EduPOP Repository](https://github.com/Eunhye-yoo/EduPOP)
- [EduPOP Demo Video](https://youtu.be/mkAcPCD7VOY)

### Infrastructure Lab
Linux · Network · Server · Docker 중심의 인프라 실습 및 기술 학습 기록

[Infrastructure Lab](https://app.notion.com/p/Infrastructure-Lab-3dd1b198732a8059b1b1f2f410f08dc6?source=copy_link)

---

## 07 · Direction

개발 기술을 이해하면서 서비스의 요구사항을 구조화하고, 실제 구현과 연결할 수 있는 역량을 쌓고 있습니다.

**기술과 서비스 흐름을 함께 이해하는 역할**을 목표로 하며, Java/Spring 기반 웹 개발 경험을 바탕으로 기술 중심의 서비스·IT 기획 영역까지 역량을 확장하고 있습니다.
