# M5 · Personal Security Extension Plan

[한국어](./m5-access-boundaries.md) · [Profile](../../README.en.md)

**Planned / My Design.** Extend my Canada branch and AWS responsibilities into one access-boundary security case. No completed attack, block, or policy-change result is claimed. Reviewed 2026-11-01.

## Problem

Connectivity alone does not establish appropriate access. Define which Canada office users may reach business services, whether they may reach a test DB or management interface, and who may administer AWS resources.

## Environment · Current Baseline

[Existing M5 notes](https://app.notion.com/p/3ff1b198732a81c19379cd1f5730afbe), [M5 assignment](https://github.com/team-blocks-lab/otter-shield/issues/34), [AWS assignment](https://github.com/team-blocks-lab/otter-shield/issues/12).

- Recorded hands-on: Sophos UTM with separate OPS/CONTENT/MGMT virtual networks, five PCs, basic gateway/DNS/TCP checks; CloudFormation VPC/NAT; EKS control plane ACTIVE.
- Not yet established: working inter-site VPN, permitted/denied inter-zone tests, Ready workers, application pods, ALB/HTTPS/RDS, or a before/after security comparison.
- Private subnet placement alone is not evidence of a tested security boundary.

## My Responsibility

M5 test design, UTM5 policy scope, AWS resources under my assignment, evidence collection, interpretation, and retest. M1 peer routing/VPN and M3 isolated test-DB endpoint require coordination. Other members’ Wazuh, M1/M2 policies, M3 cluster, or M4 backup work is not my personal result.

## Threat / Risk

Over-broad VPN selectors/rules; office PCs reaching unnecessary database/admin services; broad EKS management access; excessive AWS identity permissions; public or broad DB exposure. These are hypotheses to inspect, not confirmed vulnerabilities.

## Analysis · Proposed Access Matrix

Confirm actual endpoints and business requirements before applying policies.

| Source / identity | Destination | Proposed policy | Test requirement |
| --- | --- | --- | --- |
| M5 OPS test PC | Agreed M1 business web/DNS | Allow only confirmed ports | Valid DNS answer + web function, not TCP alone |
| M5 OPS/CONTENT PC | Isolated fake test DB | Deny direct DB access after baseline | Known listening endpoint; denied client + matching policy log |
| M5 OPS/CONTENT PC | UTM management | Deny unless explicitly authorized | Authorized MGMT control succeeds; office attempt denied |
| Approved M5 management identity/source | EKS management API | Narrow source and IAM/Kubernetes permission | Allowed identity/source succeeds; unapproved identity/source fails |
| AWS application workload | Test DB | Allow required app path only | App query succeeds; unrelated source denied |
| External/office client | AWS DB | Deny direct access | Known endpoint state and path checked; no public exposure added for testing |

Exact addresses, ports, identities, policies, and acceptable responses remain to be confirmed. No Any→Any or real credential attack is needed.

## Implementation · Ordered Work, Not Yet Applied

### A. Establish a Reliable Baseline

1. Record actual UTM WAN/interface routes, M1 peer reachability and return routes. Prior ping success to a router does not establish VPN peer reachability.
2. Establish VPN SA and verify agreed DNS/web functions in both required directions. Save relevant logs with secrets removed.
3. Prepare an isolated fake-data DB endpoint with the owner. Verify it is listening from an authorized control source.
4. Inspect existing access first. If office DB access is already denied, document a verified control; do not manufacture a vulnerability by widening access.

### B. Add Minimum-Access Policies in My Scope

1. Back up UTM5 configuration and record a rollback plan.
2. Define source/destination/service objects and explicit business allows; constrain office DB/admin paths. Confirm rule order and VPN selector/NAT behavior.
3. Make one change at a time. Record before/after policy identifiers, time, and direction.
4. Retest normal work, prohibited access, and an authorized control source. A timeout alone is not proof of firewall blocking.

### C. Extend the Same Method to AWS

1. Confirm live resource state and ownership first. Ready nodes and app/DB deployment are prerequisites for workload-to-DB tests.
2. Document approved admin source and IAM identity; inspect EKS endpoint configuration and authentication/authorization separately.
3. Design app-to-DB security-group paths with least privilege. Do not expose a DB publicly to create a baseline.
4. Use a small test IAM role with a defined permitted operation and denied operation. Record permission decisions and relevant audit events; verify event availability before claiming CloudTrail coverage.
5. WAF is a later optional HTTP-filtering experiment after HTTPS works; it does not replace app ownership checks or DB/network policy.

## Verification · Required Record

| Test | Expected after policy | Actual |
| --- | --- | --- |
| Approved office business request | Works end to end | NOT EXECUTED |
| Office direct test-DB request | Denied with attributable policy evidence | NOT EXECUTED |
| Approved control source to same DB | Works | NOT EXECUTED |
| Office UTM admin request | Denied, approved management remains usable | NOT EXECUTED |
| Approved/unapproved AWS identity | Defined allow/deny | NOT EXECUTED |
| App-to-DB / unrelated source | Allow / deny | NOT EXECUTED |
| Rollback and restored normal operation | Recoverable | NOT EXECUTED |

Capture source alias/IP, destination/port, timestamp/timezone, request, expected/actual result, relevant log/event/policy ID, and version/config diff. Secrets and cookies must be redacted. Correlate failures with routing, listener state, NAT, and server logs before attributing them to a security control.

## Evidence · To Collect

UTM rule diffs and log matches; VPN SA and business requests; fake DB listening/control query and rejected request; AWS endpoint/SG/IAM configuration; audit event; normal regression and rollback. Store actual results only, linked from a completed case study. GitHub holds concise implementation/evidence; Notion holds detailed configuration commands.

## Limitations

This document contains no policy commands ready for the current topology. Endpoint state, cross-team boundaries, permissions, and live settings must be verified before implementation. VPN establishment, EKS node/application readiness, and DB provisioning remain dependencies. No risk reduction or blocked attack is measured yet.

## Completion Criteria

A reviewer can trace **my change → normal request succeeds → prohibited request fails for the intended reason → matching logs → retest/rollback**. At least one complete personally owned case is more valuable than listing several untested products.

## Next Improvement

First finish VPN baseline and one office-to-test-DB policy case. Then apply the same proof method to an AWS IAM or SG boundary. WAF, container security, AI gateway, and agent controls follow the [longer-term lab](../cloud-api-security-lab/README.en.md), one phase at a time.
