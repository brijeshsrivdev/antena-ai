# Architecture Principles

Status: PROPOSED guardrails, not a final architecture decision.

## System boundaries
- Mobile client handles user interaction and local presentation; it is not trusted to grant tool permissions.
- Dedicated AI API owns identity integration, profile/configuration versions, session orchestration, policy enforcement, usage metering and provider abstraction.
- Telephony/media, speech recognition, model inference and speech synthesis are replaceable adapters behind explicit contracts where technically feasible.
- Domain systems remain authoritative for domain data and actions.
- Hospitality integration uses authenticated, tenant-scoped Antena backend APIs only. No direct database access from the AI service.
- Future legal/advocate systems must be separate trusted integrations and are not launch dependencies.

## Security principles
- Server-side allowlisted connector registry; no arbitrary client-provided connector URLs, SQL, scripts or tool definitions.
- Authorize each operation against user, tenant, profile, resource and requested action; validate schema and enforce least privilege.
- Personal context is untrusted content and must not grant capabilities or override policy.
- Require explicit consent/notice flows for call routing, recording and transcript handling as determined by jurisdictional research.
- Define retention, deletion, export, encryption, secrets management, audit, abuse limits and incident response before release.
- Redact sensitive values from logs; separate operational metadata from call content where possible.

## Reliability and scale
- Define latency budgets per stage and measure end-to-end p50/p95/p99.
- Model registered, monthly active, concurrent and peak call-arrival load separately.
- Use timeouts, bounded retries, idempotency, backpressure, quotas and graceful fallback.
- Design for provider outages and call-transfer failures; preserve understandable user-visible status.
- Establish SLOs, dashboards, alerts, backup/restore tests and support procedures.

## Dependency selection
Evaluate licence and commercial compatibility, maintenance, security history, deployment complexity, region support, data terms, performance, ecosystem and exit cost. Prefer replaceable interfaces where portability is meaningful; preserve necessary real-time capabilities. Benchmark end-to-end quality and total cost, not isolated STT/TTS list prices.

## Domain integration
Profiles are configuration, not security boundaries. Each connector declares operations, scopes, schemas, idempotency and audit requirements. Hospitality uses supported Antena APIs with tenant-scoped credentials, never direct database access. Legal/advocate integrations are deferred pending workflow and legal research. Personal context must not change tool permissions.

## Open decisions
Telephony/routing; media gateway; speech/model providers and fallbacks; retention defaults; authentication/tenant model; deployment topology; target regions and SLOs; libraries/licences; connector contract; API versioning and final ADRs.