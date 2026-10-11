# Requirements Index and Specification Standard

Status: initial scaffold. Detailed product requirements are not baselined. Implementation is not authorised.

## Current draft

- [CORE_REQUIREMENTS_DRAFT.md](CORE_REQUIREMENTS_DRAFT.md) contains provisional REQ-001 through REQ-015 and initial non-functional requirement areas. These are drafts with unapproved priorities and some intentionally unresolved thresholds; reconcile IDs and traceability before approval.

## Planned requirement domains
- GOV: governance, approval gates and auditability
- IDN: identity, accounts and recovery
- CFG: assistant profile, instructions, context, forms and versioning
- TEL: telephony, number setup, forwarding and routing failures
- VOX: real-time voice sessions, latency, interruptions, language and fallback
- HIS: call history, transcripts, summaries, search, export and deletion
- DOM: trusted domain connectors, scopes and tenant authorization
- HOS: hospitality profile and Antena API integration
- SEC: security, privacy, consent, retention, isolation and incident response
- BILL: plans, usage metering, limits and payment lifecycle
- UX: navigation, visual states, accessibility and design system
- OPS: observability, SLOs, rate limits, capacity, backup and support
- LEG: jurisdiction-specific legal/compliance release gates

Prefixes are provisional. Never reuse retired IDs.

## Lifecycle
DRAFT → IN_REVIEW → APPROVED → IMPLEMENTED → VERIFIED → RELEASED. Use DEFERRED or RETIRED with rationale. Requirement approval does not independently authorise implementation.

## Required fields
ID/title/status/priority/version; problem and evidence; actors/value; scope/exclusions/assumptions; preconditions and flows; alternate/error/timeout/retry/recovery cases; testable acceptance criteria; non-functional targets; authorization/privacy/consent/audit; API/data dependencies; verification/test strategy; observability/support; links to research, UX, ADRs, risks and roadmap; open questions and owner.

## Acceptance criteria
Use verifiable scenarios. Do not use vague terms such as fast, secure, user-friendly or scalable without measurable thresholds and a verification method.

## Traceability
Every feature traces to a problem or labelled hypothesis → UX journey → requirement → architecture/API/data → verification → milestone/operational owner.