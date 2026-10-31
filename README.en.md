<p align="center">
  <img src="./assets/profile-header-ink-coral.svg" alt="EunHye Yoo · Cloud & AI Security" width="100%" />
</p>

<p align="center"><strong>Working toward Cloud & AI Security Engineering through code, network paths, and evidence of security controls.</strong></p>
<p align="center"><a href="./README.md">한국어</a> · <a href="./docs/security-cases/m1-session-validation.en.md">M1 case</a> · <a href="./docs/security-cases/m3-playback-control.en.md">M3 case</a> · <a href="./docs/cloud-api-security-lab/README.en.md">Advanced lab plan</a></p>

I am EunHye Yoo, transitioning into IT after approximately six months of development and infrastructure study. I am preparing for **security solution implementation/support, cloud security, and web/API security** roles, drawing on Java/Spring development and Linux networking labs. My long-term goal is AI Security Architect.

## 01 · Security Focus

- **Authentication and sessions:** Server-side login/logout, rejection of unauthenticated requests, and HTTP response checks
- **Input and data boundaries:** Input validation and object-ownership code review, distinguishing implementation from untested paths
- **Network and access paths:** Linux 3-Tier, routing/NAT, DNAT, SSH, and layer-by-layer application-to-database connectivity checks

Verified means **supported by existing execution records and code**. It does not imply commercial security operations experience. Documentation review: 2026-11-01.

## 02 · Implemented Security Foundations

### [M1 · Session authentication and invalid-request rejection](./docs/security-cases/m1-session-validation.en.md)

Implemented intranet authentication/input checks and tested APIs locally. Evidence records login/session lookup `200`, logout `204`, subsequent post lookup `401`, and blank-title/disallowed anonymous submissions `400`.

**My contribution:** Login/post APIs, React UI, and local validation. Cross-user mutation checks exist in code; the `403` API test remains incomplete.

[Test report](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m1-intranet/docs/TEST_REPORT.md) · [401 capture](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m1-intranet/docs/evidence/08-unauthorized-401.png)

### [M3 · Login and publication-state checks for playback APIs](./docs/security-cases/m3-playback-control.en.md)

Implemented OTT login/sessions and PUBLIC video lookup/playback APIs. Evidence records `401` for invalid login and session lookup after logout, and `404` for PRIVATE video details/playback.

**Boundary:** Restricting playback URL responses does not protect the MP4 itself. CDN file protection, server deployment, and AI subtitle generation remain unverified.

[Evidence index](https://github.com/team-blocks-lab/otter-shield/blob/main/apps/m3-ott/docs/evidence/README.md) · [Implementation commit](https://github.com/team-blocks-lab/otter-shield/commit/d3772bc550681d1f05f5a7f31b86f6a3f9cfc9b7)

## 03 · Next Security Focus

**Develop a deeper personal case around M5 VPN and AWS access boundaries.** First resolve remaining connectivity/deployment checks, then compare permitted business requests with DB/management requests that should be denied under the same conditions.

[Personal security experiment plan](./docs/security-plans/m5-access-boundaries.en.md) — threats, ownership, access matrix, before/after tests, evidence, and completion criteria. **Planned, not a completed achievement.**

## 04 · Projects

### [OTTer Shield](https://github.com/team-blocks-lab/otter-shield) · Primary / In progress

Five-person OTT infrastructure and security-validation project.

- **My responsibility:** PM scheduling/issues, M1 intranet and M3 OTT development/local tests, M5 Canada branch network and AWS configuration
- **Hands-on records:** Sophos UTM/five-PC basic connectivity, AWS CloudFormation VPC/NAT setup, EKS control plane ACTIVE
- **Individual boundary:** Other members’ network security, deployment, monitoring, and backup outcomes are excluded from my achievements
- **Remaining:** Established VPN/round-trip traffic, EKS Ready nodes/application deployment, RDS/ALB/HTTPS, and post-remediation retests

[M5 technical notes](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe) · [Contribution/evidence inventory](./docs/portfolio-audit.md)

### [Full-Stack Integration Lab](https://github.com/Eunhye-yoo/fullstack-integration-lab) · Infrastructure foundation

Separated React, Spring Boot, and MySQL into Ubuntu VMs. Configured Linux NAT routing, IP forwarding, MASQUERADE, DNAT, and SSH/SCP; compared API, DB, and browser results. **A lab for understanding connectivity and access paths**, not an attack-blocking or firewall-hardening achievement.

[3-Tier implementation/evidence](https://github.com/Eunhye-yoo/fullstack-integration-lab/tree/main/02-linux-3tier) · [Commands/troubleshooting](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175)

### [EduPOP](https://github.com/Eunhye-yoo/EduPOP) · Supporting application project

Implemented class creation, multi-instructor/student mapping, academy-ownership checks on class detail views, input/duplicate/capacity validation, dashboards, and student reports. **Ownership checks are not uniform across mutation/assignment paths.** Spring Security, OAuth, and shared login are team features.

[Code-based contribution/limitations](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/access-control-review.en.md) · [Existing portfolio PDF, Korean](https://github.com/Eunhye-yoo/EduPOP/blob/main/docs/EduPOP_Portfolio_Eunhye_Yoo.pdf) · [Demo](https://youtu.be/mkAcPCD7VOY)

## 05 · Core Skills

- **Verified · Execution evidence:** Java/Spring session/input-check APIs, Postman HTTP responses, React/API/MySQL integration — M1/M3 cases and 3-Tier evidence above
- **Hands-on · Configuration:** Linux, SSH/SCP, routing/NAT, DNAT, Sophos basic network, AWS VPC/NAT/CloudFormation/EKS control plane — separate from verified node/application operations
- **Learning:** Web/API authentication/authorization, cloud access boundaries, LLM API integration
- **Planned:** Cloudflare WAF/Tunnel → AWS IAM/WAF/CloudTrail security experiments → Docker image/secret review → AI Gateway or LiteLLM → agent tool permissions/guardrails

Java, Spring Boot, JPA/MyBatis, MySQL, and React support these implementations; they do not establish security-product proficiency. [Lab design and completion criteria](./docs/cloud-api-security-lab/README.en.md)

## 06 · Certifications

- **Certified:** Network Administrator Level 2, Korea
- **Exam stages passed:** Engineer Information Processing written exam / Linux Master Level 2 first-stage exam
- **Long-term options, not earned:** CISSP, AWS Security – Specialty, AWS Solutions Architect – Professional. CISSP experience eligibility remains unconfirmed

## 07 · Technical Documentation

**GitHub:** Source, APIs, and application evidence. **Notion:** Environments, configuration commands, networks, and troubleshooting.

[Infrastructure Lab](https://app.notion.com/p/3dd1b198732a8059b1b1f2f410f08dc6) · [Linux 3-Tier](https://app.notion.com/p/3ed1b198732a815091d2e0030512f175) · [OTTer M5](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe)

Foundational study: [Spring Boot](https://github.com/Eunhye-yoo/springBoot_practice) · [React](https://github.com/Eunhye-yoo/react_practice) · [Servlet](https://github.com/Eunhye-yoo/servlet_practice) · [Study Log](https://github.com/Eunhye-yoo/study_log). Coursework and unfinished missions are separated from featured security work.

## 08 · English Communication

Study and life in Canada, a commerce degree, and English-teaching experience provide a background for reading English technical documentation and communicating in English. I aim to apply this to global collaboration and English technical support; I have no overseas technical-support or AWS ticket-handling work experience.
