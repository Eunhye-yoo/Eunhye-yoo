# Security Case Study · M3 Playback API Boundary

[한국어](./m3-playback-control.md) · [Profile](../../README.en.md)

Status: local control implementation/validation; no discovered-and-fixed vulnerability claim. Reviewed 2026-11-01.

## Problem
Video details and playback information must follow publication state and session identity.

## Environment
Developer PC: Java 21, Spring Boot 4.1.2, MySQL 8.0.46, React 19.3.0. Backend default 8081; UI/proxy observed at localhost:5175.

## My Responsibility
OTT authentication, video/playback APIs, React integration, and local tests. M3 owner handles service network/server deployment. [Implementation commit](https://github.com/team-blocks-lab/otter-shield/commit/d3772bc550681d1f05f5a7f31b86f6a3f9cfc9b7).

## Threat / Risk
Direct ID requests could reveal PRIVATE video information; a playback API without session checks could return URLs to unauthenticated callers. Direct media-file access is a separate risk.

## Analysis
Authentication identifies the member. Publication-state checks constrain the requested object. Neither guarantees access control at the media origin/CDN.

## Implementation
AuthController replaces old sessions at login and invalidates them at logout. AuthService hashes passwords with BCrypt and rechecks that session members exist. VideoService queries PUBLIC videos; PlaybackService checks the member, then queries the requested PUBLIC video before returning URLs. Missing/private videos share a 404 response.

## Verification

| Condition | Expected | Existing result |
| --- | --- | --- |
| Invalid credentials | 401 | Registered capture |
| Session lookup after logout | 401 | Registered capture |
| PRIVATE detail/playback | 404 | Captures registered; playback response body visually reviewed |
| Invalid pagination | 400 | Registered capture |
| Unauthenticated playback | 401 | Developer record only; separate capture absent |
| Direct MP4 URL without session | Policy-specific denial | NOT VERIFIED |

The playback screenshot shows status 404 in the JSON body; it does not expose the HTTP status line. Existing records were reviewed; APIs were not rerun here.

## Evidence
- [Evidence index](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/README.md)
- [Invalid login](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/07-login-invalid-401.png) / [session after logout](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/09-session-after-logout-401.png)
- [PRIVATE detail](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/13-private-detail-404.png) / [PRIVATE playback](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/docs/evidence/14-private-playback-404.png)
- [AuthService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/auth/AuthService.java) / [VideoService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/video/VideoService.java)
- [PlaybackService](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/video/PlaybackService.java) / [VideoController](https://github.com/team-blocks-lab/otter-shield/blob/c7228831689e4052cfc3b2f45eca8ee073c53dbc/apps/m3-ott/backend/src/main/java/com/otter/ott/video/VideoController.java)

## Limitations
No proof of direct MP4/CDN protection, full role/subscription authorization, shared sessions across pods, server deployment, or AI-generated subtitles. Configuration placeholders do not establish a complete secret lifecycle.

## Next Improvement
Capture HTTP status lines for authenticated/unauthenticated × PUBLIC/PRIVATE/missing video requests. Compare API responses with direct origin/CDN requests. Select media-origin and expiring-URL controls only after defining the playback requirement, then test normal playback and bypass attempts.
