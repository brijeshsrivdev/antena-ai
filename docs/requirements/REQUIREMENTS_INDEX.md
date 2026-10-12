# Requirements Index and Specification Standard

Status: initial scaffold. Detailed product requirements are not baselined. Implementation is not authorised.

## Current draft

- [CORE_REQUIREMENTS_DRAFT.md](CORE_REQUIREMENTS_DRAFT.md) contains draft REQ-001 through REQ-015 and NFR-001 through NFR-010. IDs are stable within this working draft and used by the traceability matrix; requirement content, priorities, thresholds and full cross-document traceability remain unapproved and must be reviewed before baseline approval.

- [TRACEABILITY_MATRIX.md](TRACEABILITY_MATRIX.md) maps the draft requirements to UX, architecture, risks and verification; mappings are manual and known evidence/coverage gaps remain.

- [Expanded traceability](TRACEABILITY_MATRIX.md) now includes proposed evidence states and exit gates for REQ-001–REQ-015 and NFR-001–NFR-010.
- [MVP scope and feature gates](../discovery/MVP_SCOPE_AND_FEATURE_GATES.md) separates core candidates, conditional capabilities and deferred scope. Nothing in it is approved.
- [Acceptance threshold register](ACCEPTANCE_THRESHOLD_REGISTER.md) records measurable candidate thresholds, evidence requirements and unresolved placeholders. All values remain proposed or open pending explicit owner review.

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