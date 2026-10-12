# Data Inventory and Lifecycle — Draft

**Status:** Draft for privacy/architecture review. Not a final retention policy. Date: 2026-10-11.

## 1. Data classes

| Data class | Examples | Purpose | Sensitivity / risk | Initial lifecycle direction |
|---|---|---|---|---|
| Account identifiers | Internal user ID, login identifier, auth subject | Authentication, account support | High | Keep only while account is active and required for security/legal purposes; define post-deletion schedule. |
| Contact/caller metadata | Caller number, display name, contact mapping, call timestamps | Call context and history | High | Minimise; avoid full contact import unless justified; separate raw number from analytics IDs where possible. |
| Routing configuration | Operator/SIM choice, forwarding status, setup verification | Call delivery and troubleshooting | High | Keep only required status/history; protect from unauthorized changes. |
| Assistant profile | Name, language, tone, boundaries, custom context | Personalise responses | High; may contain sensitive facts | Structured fields, versioned; user edit/delete; avoid unnecessary sensitive details. |
| Live audio/media | Incoming/outgoing audio frames or provider media stream | Realtime conversation | Very high | Do not persist by default unless a reviewed feature requires it; secure transient processing. |
| Recording | Full call audio | Playback/evidence if enabled | Very high | Separate explicit decision/notice; shortest justified retention; provider deletion must be verified. |
| Transcript | Spoken words and speaker turns | Live transcript, summary, search | Very high | Optional feature; separate retention/access control from summary; avoid logging content. |
| Summary and extracted intent | Call reason, promises, callback needs | User understanding and follow-up | High | Store only if useful; flag uncertainty; allow correction and deletion. |
| Suggested tasks/reminders | Callback reminder, appointment note | User-controlled follow-up | High | User confirms before consequential external actions; define expiration and deletion. |
| Usage/billing ledger | Billable minutes, provider event IDs, plan usage | Billing, fraud prevention, cost control | Medium/high | Keep minimal auditable records per applicable financial/legal retention; no transcript in ledger. |
| Consent and notice records | Notice version, activation, feature consent, withdrawal | Demonstrate choices and manage processing | High | Retain the minimum record needed for accountability under counsel-approved policy. |
| Security/audit events | Login, route change, export, deletion, admin access | Security and incident response | High | Content-free metadata where possible; access-controlled, bounded retention. |
| Operational telemetry | Latency, provider errors, concurrency, cost | Reliability and observability | Medium/high | Avoid caller numbers/raw content; aggregate or pseudonymise; short retention unless justified. |
| Support records | Issue category, call/session ID, user correspondence | Troubleshooting and safety | High | Limit access; do not request raw call content by default; define closure/retention. |
| Domain connector data (future) | Antena API response subset | Hospitality operation | High | Retrieve minimum fields per action; do not duplicate domain source of truth; no direct DB access. |

## 2. Lifecycle states

For each stored artifact, define: created → active use → retention/expiry pending → deletion requested → deletion in progress → deleted from primary systems → provider deletion confirmed or exception recorded → backup expiration complete according to policy.

Do not represent deletion as complete merely because a UI row disappeared. Define what deletion means for primary databases, object storage, search indexes, caches, analytics, vendor systems and backups.

## 3. Data-flow inventory required before approval

For every data class, record:
- collection source and trigger;
- whether it is required or optional;
- purpose and applicable notice/consent;
- systems and subprocessors that receive it;
- data location and cross-border transfer;
- access roles and authorization checks;
- encryption and key ownership;
- retention period and deletion mechanism;
- backup and disaster-recovery lifecycle;
- export/access/correction workflow where applicable;
- logging/analytics exposure;
- breach/incident response owner;
- legal basis and counsel review status.

## 4. Minimisation defaults to consider

- Do not store raw audio unless the user enables a reviewed feature and the legal basis/notice is settled.
- Do not store full transcripts just because a summary is generated.
- Do not send the user's entire profile or contact book to every model/provider; pass only the minimum context needed for the current call.
- Keep operational metrics free of raw audio, transcripts and unnecessary phone numbers.
- Use a stable internal identifier for analytics and avoid placing caller phone numbers in metric labels.
- Keep billing events separate from conversation content.
- Keep domain API responses transient where possible and store only user-requested outcomes.
- Never use personal call content for model training by default without a separate, informed and legally reviewed opt-in.

## 5. Retention policy is an open decision

No specific duration is set here. Durations must reflect product value, provider capabilities, legal requirements, user control and cost. Define separate values for raw media, transcript, summary, profile context, usage/billing, consent and security logs. Include a deletion SLA and verified exception handling.

## 6. Sources to align with

- MeitY Digital Personal Data Protection Rules 2025: https://www.meity.gov.in/documents/act-and-policies/digital-personal-data-protection-rules-2025-gDOxUjMtQWa?pageTitle=Digital-Personal-Data-Protection-Rules-2025
- Android and Google Play permissions guidance: https://developer.android.com/guide/topics/permissions/default-handlers
- Provider privacy policies, data processing terms and deletion documentation must be reviewed once providers are shortlisted.

## 7. Decision status

This document proposes data classes and lifecycle controls only. It does not approve retention durations, provider data terms, recording defaults or a legal basis.

## 8. Deletion-target reconciliation — 2026-10-12

The shared target-by-data-class checklist and candidate request/target outcome semantics are recorded in [Deletion and Verification Reconciliation](../governance/DELETION_AND_VERIFICATION_RECONCILIATION.md). Use it to enumerate actual first-party, provider, derived-copy and backup destinations once the deployed architecture is selected.

For each destination, record **present**, **not present with evidence**, or **unknown**. Unknown destinations block a full-deletion claim. A parent `DeletionRequest` is not complete merely because the primary row is gone; each required `DeletionTarget` must have a confirmed outcome or a separately approved exception. The candidate target states in the reconciliation document are proposals, not approved enum values.

No data-class retention duration, deletion SLA, backup expiry or legal exception is approved by this addition.
