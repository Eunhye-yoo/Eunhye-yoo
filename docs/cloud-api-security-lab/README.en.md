# Cloud & API Security Architecture Lab

[한국어](./README.md) · [Profile](../../README.en.md)

**Planned · Design only.** A single progressive personal lab, not a deployed system. No runtime infrastructure, successful tests, or working security product integrations are claimed here. Review: 2026-11-01.

## Scope and Architecture Status

| Label | Meaning / current state |
| --- | --- |
| Reference Architecture | External official architectures, explicitly attributed; no external diagram copied here |
| My Design | Proposed staged design below, authored for this lab; not an official vendor architecture |
| Implemented Scope | This design document only; runtime implementation absent |
| Verified Scope | None for this new lab; existing OTTer cases are separate prior work |
| Not Implemented | WAF/Tunnel, AWS security experiments, containers/scanning, AI gateway, agent controls |

## My Design · Proposed Boundaries

1. Identity: test users A/B and an administrator; owned API objects and audit event IDs.
2. Edge: Cloudflare WAF/Tunnel candidate path to a test application. WAF handles selected HTTP filtering; application identity/ownership remain enforced by the app.
3. Cloud: separate AWS phase using ALB/WAF, private application/DB paths, scoped IAM, and CloudTrail. This is an alternative experiment path; not every product is required in one chain.
4. Workload: reproducible container image, runtime secret injection, build-secret separation, vulnerability triage.
5. AI: select Cloudflare AI Gateway **or** LiteLLM first; scoped credentials, request budgets, and redacted logs.
6. Agent: allowlisted mock tools, server-enforced identity/scope, approval for state-changing tools, negative tests for prompt injection and unauthorized actions.

## Ordered Milestones

| Phase | Work | Evidence required before Verified |
| --- | --- | --- |
| 01 Web/API | Session/authentication, ownership/role checks, input checks | A/B requests; expected and actual 200/401/403/400 as specified; DB unchanged on rejection; HTTP logs |
| 02 Cloudflare | WAF rule and Tunnel; origin bypass analysis | Same allowed/denied requests before/after rule; event ID; direct-origin attempt; normal API regression |
| 03 AWS | IAM/VPC/WAF/CloudTrail | Allowed/denied IAM operations; permitted/blocked DB paths; WAF event; CloudTrail event; no broad wildcard permission claim |
| 04 Docker | Image build, secrets, vulnerability management | Image digest; scanner/version/time; triage/remediation/re-scan; image/history review without secrets |
| 05 AI gateway | Choose one gateway; scoped key/model/budget policies | Allowed/denied calls; configured thresholds vs actual enforcement; no raw sensitive prompts in published logs |
| 06 Agent | Tool permissions and guardrails | Read-only/write-tool separation; denied unauthorized action; normal allowed flow; residual prompt-injection limits |

Complete and retest each phase before expanding scope. Existing M1/M3 controls are reference inputs, not evidence that phases 01–06 have been implemented.

## Repository Structure to Create During Implementation

- README.md / README.en.md — overview and current scope
- docs/architecture/ — attributed references, My Design, decision records
- docs/cases/ — Problem → Environment → My Responsibility → Threat/Risk → Analysis → Implementation → Verification → Evidence → Limitations → Next Improvement
- app/ — minimal test API; no changes to team application logic required
- infra/cloudflare/, infra/aws/, containers/ — actual configuration added when used
- tests/ — reproducible requests/assertions and controlled fake fixtures
- evidence/phase-01/ through phase-06/ — only actual executions, never generated success placeholders

These are planned directories, not links to existing files. A standalone personal repository can host this structure when implementation starts.

## Evidence Rules

Each execution records commit, environment/version, UTC timestamp, command/request, expected result, actual result, redacted output, and rollback/cleanup. Include both normal and rejected requests and DB/log comparison where relevant. A failed/untested check remains visible. Do not publish session cookies, API keys, PSKs, account credentials, or personal data. Costs, feature entitlement, current API syntax, and cleanup must be checked at implementation time.

## Official References

Official documentation reviewed 2026-11-01; references do not certify this proposed design.

- [Cloudflare WAF](https://developers.cloudflare.com/waf/)
- [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/)
- [AWS Well-Architected Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html)
- [Docker build secrets](https://docs.docker.com/build/building/secrets/)
- [Cloudflare AI Gateway](https://developers.cloudflare.com/ai-gateway/)
- [LiteLLM proxy quick start](https://docs.litellm.ai/docs/proxy/quick_start)

## Next Action

Start locally with phase 01: define an object owner and two users, specify normal and forbidden operations, then capture actual HTTP/DB results. No paid cloud resources were created for this portfolio update.
