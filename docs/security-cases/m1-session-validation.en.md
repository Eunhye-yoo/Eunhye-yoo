# Security Case Study · M1 Session & Input Validation

[한국어](./m1-session-validation.md) · [Profile](../../README.en.md)

Status: local control implementation/validation; not a discovered-and-fixed vulnerability. Review: 2026-11-01. Original test record: 2026-10-28.

## Problem
The intranet must reject requests without a valid employee session and prevent invalid post submissions.

## Environment
Developer PC: Java 21, Spring Boot 4.1.1, MySQL 8.0.46, React. API base: localhost:8080. M1/M2 deployment is separate.

## My Responsibility
Designed/implemented login and post APIs, React integration, and local tests. M1/M2 owners handle server/network deployment. [Development commit](https://github.com/team-blocks-lab/otter-shield/commit/2b4cbd2ddfbdb918657c15532b849e197ea87abe), [integration commit](https://github.com/team-blocks-lab/otter-shield/commit/9c03ee07743d74c16c5686c77cf8e3203dddc486).

## Threat / Risk
Unauthenticated access, cross-user mutations, and invalid data. These are design risks; no exploitation is claimed.

## Analysis
The server must determine identity from its session, validate inputs, and separately check post ownership. Hiding UI controls alone is insufficient.

## Implementation
- AuthController invalidates an old session at login, stores LOGIN_EMPLOYEE_ID, and invalidates the session at logout.
- LoginInterceptor checks session identity, employee existence, and first-login completion for /api/post and /api/post/**.
- AuthService uses BCrypt matching; initial setup hashes the new password and rejects inputs over 72 UTF-8 bytes.
- PostService checks author identity before update/delete. Unit test source asserts FORBIDDEN and unchanged content/no delete call.
- DB credentials are environment placeholders; HttpOnly, SameSite=Lax, and 30-minute session timeout are configured. This does not prove complete secret management or CSRF protection.

## Verification

| Request/condition | Expected | Existing result |
| --- | --- | --- |
| POST /api/auth/login; GET /api/auth/me | 200 | 200, report/captures |
| POST /api/auth/logout | 204 | 204, report/capture |
| GET /api/post after logout | 401 | 401, capture visually reviewed |
| POST /api/post with blank title | 400 | 400 with title field error, capture visually reviewed |
| Anonymous lunch post | 400 | 400, report/capture registered |
| Another employee updates/deletes | 403, no data change | Code/unit-test source reviewed; API execution NOT VERIFIED |

These are existing developer records, not a new execution in this documentation review.

## Evidence
- [Test report](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/docs/TEST_REPORT.md)
- [401 capture](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/docs/evidence/08-unauthorized-401.png) / [400 capture](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/docs/evidence/06-blank-title-400.png)
- [AuthController](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/auth/AuthController.java) / [AuthService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/auth/AuthService.java)
- [Interceptor](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/auth/LoginInterceptor.java) / [WebConfig](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/config/WebConfig.java)
- [PostService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/java/com/otter/intranet/post/PostService.java) / [unit-test source](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/test/java/com/otter/intranet/post/PostServiceTest.java)
- [Configuration](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m1-intranet/backend/src/main/resources/application.properties)

## Limitations
No cross-user 403 API capture, deployed-server retest, session-cookie/TLS inspection, CSRF verification, brute-force test, or secret-history audit. A suite-success screenshot alone does not establish that every current test passed. No before/after attack evidence.

## Next Improvement
Use two local test employees: prove own-post update succeeds, other-user update/delete returns 403, and DB content is unchanged. Record method, session identity alias, post owner, timestamp, commit, and DB comparison with credentials/cookies redacted. Then repeat 401/400/403 and normal operations on the target server.
