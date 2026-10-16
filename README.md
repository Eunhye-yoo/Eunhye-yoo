<p align="center">
  <img src="./assets/profile-header-ink-coral.svg" alt="EunHye Yoo profile header" width="100%" />
</p>

<p align="center">
  <strong>Connecting requirements, applications, and infrastructure through implementation and verification.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Requirements-FF5D5D?style=flat-square" alt="Requirements" />
  <img src="https://img.shields.io/badge/Applications-0D1B2A?style=flat-square" alt="Applications" />
  <img src="https://img.shields.io/badge/Infrastructure-1B263B?style=flat-square" alt="Infrastructure" />
  <img src="https://img.shields.io/badge/Verification-415A77?style=flat-square" alt="Verification" />
</p>

<p align="center">
  <a href="./README.ko.md">한국어</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Eunhye-yoo/EduPOP">EduPOP</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Eunhye-yoo/fullstack-integration-lab">Full-Stack Lab</a>
  &nbsp;·&nbsp;
  <a href="https://app.notion.com/p/Infrastructure-Lab-3dd1b198732a8059b1b1f2f410f08dc6?source=copy_link">Infrastructure Lab</a>
</p>

---

## 01 · About

I explore how **requirements, application features, data, and server/network environments** fit together in a working system. In EduPOP, I helped define service requirements and implemented class-management and analytics features. In the Full-Stack Integration Lab, I verified React–API–MySQL integration and communication across Linux VMs using routing and NAT.

Before moving into IT, I coordinated instructors, students, schedules, and customer needs in education operations. I bring that perspective to requirement analysis and team projects, documenting what I actually built, configured, and verified.

---

## 02 · Tech Stack

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

Version badges refer to EduPOP. Integration labs and practice projects use their own Java, Spring Boot, and MyBatis starter versions.

### Infrastructure & Network
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![VMware](https://img.shields.io/badge/VMware-607078?style=flat-square)
![Routing/NAT](https://img.shields.io/badge/Routing%20%2F%20NAT-415A77?style=flat-square)
![SSH/SCP](https://img.shields.io/badge/SSH%20%2F%20SCP-475569?style=flat-square)

**Configuration labs:** [Linux 3-Tier (React / Spring Boot / MySQL)](https://github.com/Eunhye-yoo/fullstack-integration-lab/tree/main/02-linux-3tier) · AWS EC2/VPC/ALB (Linux httpd, Windows IIS, Bastion Host)

**Currently studying:** Docker · LLM / Generative AI applications

### Tools
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![IntelliJ IDEA](https://img.shields.io/badge/IntelliJ%20IDEA-000000?style=flat-square&logo=intellijidea&logoColor=white)

---

## 03 · Selected Work

### [EduPOP](https://github.com/Eunhye-yoo/EduPOP)

> **An education platform that connects academy operations and test results to the next learning cycle**

`Java` `Spring Boot` `MyBatis` `MySQL`

- **Problem & requirement definition** — Proposed the original concept and translated academy-operation and learning needs into core service flows and feature scope
- **Class management implementation** — Implemented class creation and updates, student/multi-instructor assignment, duplicate and capacity checks, and status-based class closure
- **Pre-Class Dashboard** — Built class/student performance summaries and weak-area signals to support a three-minute pre-class review goal
- **Student Performance Report** — Implemented score trends and strength/weakness analysis, with analytics logic reused in monthly reporting code

> **Scope note:** Three minutes is a design goal, not a measured result. Assignment/access checks differ by path, and the parent-facing report share link is unfinished.

[Project README](https://github.com/Eunhye-yoo/EduPOP) · [Planning & Implementation Portfolio (PDF · Korean)](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/EduPOP_Portfolio_Eunhye_Yoo.pdf) · [Demo Video](https://youtu.be/mkAcPCD7VOY)

### [Full-Stack Integration Lab](https://github.com/Eunhye-yoo/fullstack-integration-lab)

> **Hands-on integration labs connecting frontend, backend, database, Linux servers, and network paths**

`React` `Spring Boot` `MyBatis` `MySQL` `Linux` `Routing/NAT`

- **Application integration** — Verified React → Vite Proxy → Spring Boot → MyBatis → MySQL CRUD flow and corrected environment-specific datasource/API configuration
- **Linux 3-Tier environment** — Separated React, Spring Boot, and MySQL across Ubuntu VMs with static IPs and remote database access
- **Network extension** — Added a Linux NAT Router, IPv4 forwarding, MASQUERADE, SSH/SCP, and DNAT port forwarding, then verified the full Windows → Router → React → Spring Boot → MySQL path

- **Express API** — Added Express source and verified query, path, and JSON body handling with GET/POST/PUT/DELETE responses. PUT/DELETE are learning examples without database persistence.

[Repository](https://github.com/Eunhye-yoo/fullstack-integration-lab) · [Detailed Infrastructure Lab](https://app.notion.com/p/Infrastructure-Lab-3dd1b198732a8059b1b1f2f410f08dc6?source=copy_link)

---

## 04 · Practice & Study

| Repository | Focus |
| --- | --- |
| [Spring Boot Practice](https://github.com/Eunhye-yoo/springBoot_practice) | Spring MVC · Thymeleaf · Interceptor/AOP · JPA · QueryDSL |
| [React Practice](https://github.com/Eunhye-yoo/react_practice) | JavaScript · Components · Hooks · Router · State |
| [Servlet Practice](https://github.com/Eunhye-yoo/servlet_practice) | Servlet · JSP · JDBC · Session · Request flow |
| [Study Log](https://github.com/Eunhye-yoo/study_log) | Network · Routing · Server · IT fundamentals |

---

## 05 · Certifications

- **Network Administrator Level 2 (Korea)** — Certified
- **Engineer Information Processing (Korea)** — Written exam passed
- **Linux Master Level 2 (Korea)** — Written exam passed

---

## 06 · Infrastructure Lab

Documentation covers **Linux 3-Tier · Network · Server** configuration, integration, verification, and troubleshooting. Separate hands-on AWS practice includes **EC2, VPC, ALB, and Bastion Host**. I am currently studying **LLM / Generative AI and Docker**.

[GitHub Full-Stack Integration Lab](https://github.com/Eunhye-yoo/fullstack-integration-lab) · [Notion Infrastructure Lab](https://app.notion.com/p/Infrastructure-Lab-3dd1b198732a8059b1b1f2f410f08dc6?source=copy_link)
