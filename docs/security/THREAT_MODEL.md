# Initial Threat Model — AI Call Assistant

**Status:** Initial threat discovery, not a completed security assessment. Date: 2026-10-11. No implementation authorised.

## 1. System and trust boundaries

Assets include account credentials, phone numbers, caller identity, call-routing configuration, audio, transcripts, summaries, personal context, usage/billing records, connector credentials, provider webhooks and audit logs.

Trust boundaries:
1. User device ↔ public API.
2. Telephony provider ↔ webhook/media ingress.
3. Realtime session worker ↔ speech/model providers.
4. AI model output ↔ policy/tool gateway.
5. AI service ↔ Antena or future domain APIs.
6. Primary storage ↔ background workers, support tools, backups and analytics.
7. User ↔ third-party caller who may not be an account holder.

## 2. Threat scenarios and controls

| ID | Threat | Potential impact | Initial control requirements | Verification |
|---|---|---|---|---|
| THR-001 | Account takeover | Attacker reads call records, changes routing or impersonates user. | Secure authentication/recovery, session revocation, rate limits, alerts for risky changes. | Auth/recovery abuse tests. |
| THR-002 | Insecure direct object reference | User accesses another user's calls, summaries or usage by changing IDs. | Object-level authorization at every query and export boundary. | Cross-tenant negative tests. |
| THR-003 | Spoofed/replayed provider webhook | Fake call session, wrong billing, tool execution or denial of service. | Signature verification, timestamp/replay checks, idempotency keys, provider allowlist and bounded body sizes. | Forged/replayed webhook tests. |
| THR-004 | Media/session mix-up | Audio or transcript associated with the wrong user/call. | Server-generated session IDs, verified call-to-account mapping, explicit lifecycle state machine. | Concurrency and out-of-order event tests. |
| THR-005 | Prompt injection from caller speech | Caller attempts to override assistant policy or extract personal context. | Treat caller input and profile text as untrusted; separate policy from content; no direct model authority over tools. | Adversarial conversation suite. |
| THR-006 | Tool/connector abuse | Model calls unauthorized operation or reaches attacker-controlled endpoint. | Server-side allowlist, typed schemas, scoped authorization, no arbitrary URLs/SQL/scripts, confirmation for consequential actions. | Tool authorization and SSRF tests. |
| THR-007 | Cross-tenant connector access | Hospitality or future domain data leaks across tenants. | Tenant-scoped domain API credentials, resource-level checks and audit. | Tenant-boundary integration tests. |
| THR-008 | Sensitive content in logs/traces | Audio/transcripts exposed through observability or support tools. | No raw content by default; redaction, restricted access, short retention and audit. | Log scanning and access tests. |
| THR-009 | Provider retains or trains on call content unexpectedly | Privacy breach, legal/contractual mismatch. | Review DPA, retention, training, subprocessors and region; use approved settings; document provider deletion. | Contract/configuration review. |
| THR-010 | Excessive retention or failed deletion | User cannot remove sensitive call records. | Data-class-specific lifecycle, deletion jobs, provider deletion and backup schedule. | End-to-end deletion exercise. |
| THR-011 | Call-routing misconfiguration | Important calls are dropped, diverted unexpectedly or cannot be restored. | Explicit activation, test call, verified state, immediate disable instructions, status reconciliation. | Carrier/device recovery tests. |
| THR-012 | Resource exhaustion / cost attack | High bills, unavailable service or queue collapse. | Per-user/global duration, concurrency and spend caps; admission control; bounded retries; abuse detection. | Burst and budget-exhaustion tests. |
| THR-013 | Model hallucination or unsafe commitment | User's reputation, privacy or finances harmed. | Narrow scope, disclosure, uncertainty, confirmation for commitments, refusal/escalation rules. | Scenario-based red-team tests. |
| THR-014 | Caller impersonation or voice-clone abuse | Fraud or deception. | Exclude voice cloning from MVP; do not make identity claims based only on voice; abuse monitoring. | Scope review and abuse tests. |
| THR-015 | Insider/support misuse | Staff access call content without need. | Least privilege, just-in-time access, audited support access, break-glass process and retention limits. | Access review and audit sampling. |
| THR-016 | Secrets leak from client or repository | Provider account compromise and cost abuse. | Server-side secrets, managed secret store, rotation, scanning and least-privilege credentials. | Secret scan and rotation drill. |
| THR-017 | Provider outage / model timeout | Calls go silent or are mishandled. | Deadline budgets, fallback/termination, circuit breakers, graceful degradation and incident runbooks. | Fault-injection tests. |
| THR-018 | Malicious file/content in context or imported contacts | Prompt injection or data exfiltration. | Treat all context as data, sanitize/limit input, no capability grants from imported content. | Adversarial input tests. |

## 3. Abuse cases to model

- Caller pressures assistant to disclose the user's schedule, address, contacts or personal facts.
- Caller pretends to be a bank, government officer, employer, family member or emergency responder.
- Caller requests a payment, booking, appointment, purchase or commitment.
- User's profile contains malicious instructions copied from an email/webpage.
- An attacker repeatedly calls to exhaust usage quota or cause forwarding fees.
- User loses device and needs to disable routing and revoke sessions.
- Support agent is asked to retrieve call audio without sufficient authority.
- Provider sends duplicate, delayed or forged call events.
- AI summary fabricates a commitment or misses a critical negation.

## 4. Minimum security controls before pilot

- Threat model reviewed against actual architecture and jurisdiction.
- Authentication, object-level authorization and tenant isolation tests.
- Signed provider webhook verification, idempotency and replay defence.
- Server-side policy/tool gateway with explicit scopes.
- Data minimisation, encryption in transit/at rest, secret management and rotation.
- Content-free operational logs by default; audited privileged access.
- Usage/concurrency/spend quotas and abuse response.
- Secure deactivation, account recovery and deletion workflows.
- Provider security/privacy terms reviewed.
- Incident response, provider outage and data deletion runbooks.
- Independent security review appropriate to exposure and data sensitivity.

## 5. Open questions

Exact media transport; identity model; provider webhook signature support; session-store consistency; encryption/key ownership; support access; data residency; deletion guarantees; threat model for app links/deep links; emergency and high-risk call policy; incident notification obligations; security test scope.

## 6. Decision status

This is an initial threat register. It is not a penetration test, legal opinion or completed security review. Update it when architecture, providers, data retention and MVP scope are approved.

## Business phone assistant threat-model extension — 2026-10-13

The business-oriented domain contract adds threat areas to include in the next reviewed threat model: organization membership/role bypass; workflow schema or publication abuse; caller-ID-based disclosure without verification; cross-tenant workflow/action execution; spoofed or incomplete call-observation events; connector write duplication after ambiguous timeout; and misleading dashboard metrics caused by missing events or undefined denominators. See [Business Assistant Domain Contract Draft](../architecture/BUSINESS_ASSISTANT_DOMAIN_CONTRACT_DRAFT.md). This is a desk-only extension, not a completed threat assessment or security test.


## Proposed business requirement threat mapping — 2026-10-15

Map the following threats to the proposed REQ-017–REQ-022 before approving the threat model. This desk review adds traceability only; it is not a completed threat assessment.

| Proposed requirement | Threat areas to verify | Planned evidence |
|---|---|---|
| REQ-017 | Cross-tenant object access, membership/role bypass, stale authorization, support-access misuse | BPA-001/BPA-002; negative authorization matrix and audit review |
| REQ-018 | Malicious workflow configuration, publication privilege abuse, version confusion, prompt injection into configuration | BPA-003/BPA-004/BPA-005/BPA-018; schema abuse fixtures and state-transition review |
| REQ-019 | Caller-ID spoofing, social engineering, account/customer enumeration, verification retry abuse | BPA-006/BPA-007; caller verification abuse cases and non-disclosure tests |
| REQ-020 | Forged/incomplete/replayed provider events, false missed-call claims, misleading status after route failure | BPA-012–BPA-015/BPA-017/BPA-018; provider capability mapping and event reconciliation tests |
| REQ-021 | Unauthorized connector writes, cross-tenant action, duplicate side effects after timeout, false success claim | BPA-009–BPA-011; connector authorization/idempotency/reconciliation tests |
| REQ-022 | Cross-tenant aggregation leakage, misleading denominator, stale or silently corrected metrics | BPA-016; metric dictionary, tenant-scope review and late-event fixtures |

No tests have been run and no provider/integration has been selected. Add these to the reviewed threat model after the first workflow, data classes and connector contract are chosen.
