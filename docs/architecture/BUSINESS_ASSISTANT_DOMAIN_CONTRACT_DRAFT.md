# Business Phone Assistant Domain Contract — Draft

**Status:** Conceptual domain contract for discovery only. Not an approved schema, API, workflow DSL, provider contract or implementation authorization.  
**Date:** 2026-10-13.  
**Depends on:** `BUSINESS_PHONE_ASSISTANT_PRODUCT_DIRECTION.md`, `BUSINESS_ASSISTANT_REQUIREMENT_GAP_AUDIT.md`, `API_CONTRACT_DRAFT.md`, `DATA_MODEL_DRAFT.md`, `STATE_AND_EVENT_CONTRACTS_DRAFT.md`, and `THREAT_MODEL.md`.

## 1. Purpose and boundaries

This document provides one consistent vocabulary and a first-pass set of domain boundaries for the business-phone-assistant hypothesis. It is meant to prevent the API, data, UX and evaluation drafts from making incompatible assumptions. It does not select a provider, vertical, ticket system, caller-verification method, hosting model, legal basis or final MVP.

The conceptual path is:

`Organization configuration → validated workflow version → eligible business-number route → observed call/session → bounded workflow execution → optional authorized connector action → authoritative action outcome → business-visible call outcome`.

A missing event or uncertain result must remain unknown; it must not be converted into success or a claim that no call occurred.

## 2. Canonical vocabulary

| Term | Meaning | Boundary |
| --- | --- | --- |
| Account | Authenticated human identity in the control plane | An account may belong to zero, one or multiple organizations; membership grants access. |
| Organization | Business-facing owner of phone routes, workflows, integrations, usage and call records | Tenant is the backend isolation boundary; never trust an organization ID supplied by a client without membership authorization. |
| Organization membership | Relationship between an account and organization, with role and status | Membership is distinct from authentication and must be checked for every organization-scoped operation. |
| Workflow definition | Stable identity for a business-configured inbound call process | Stores no arbitrary executable code, SQL, client-defined connector URL or model-granted permission. |
| Workflow version | Immutable, validated configuration snapshot | A call execution records the exact version used; publishing a newer version does not silently rewrite an active execution. |
| Business number / route | Number and provider route through which callers may reach the assistant | Route activation and workflow publication are separate state dimensions. Route support is evidence-scoped. |
| Call observation | Evidence from a provider/carrier/route source that a call event occurred | Observation coverage is limited to what the source can actually see. No event does not prove no call occurred. |
| Call session | Product-level representation of a conversation, possibly spanning multiple provider legs | Session existence does not prove successful conversation, caller identity or billable duration. |
| Caller reference | Minimal identifier or matched customer reference associated with a call | Caller ID is a match signal, not authentication. Do not expose protected customer information without the workflow's approved verification policy. |
| Workflow execution | One call's execution against one pinned workflow version | Records progress and branch outcomes without treating model text as authoritative external state. |
| Action execution | One requested connector action, with authorization, idempotency and outcome state | A request/timeout is not proof of success. Show success only after authoritative confirmation. |
| Call outcome | Canonical product classification of the observed interaction and its evidence | Outcome categories must retain unknown/unobserved and partial failure states. |
| Usage event | Immutable usage evidence used for metering/reconciliation | Billing units, call-leg inclusion and adjustments remain provider/plan dependent. |

## 3. Organization and authorization boundary

Every organization-scoped resource must be authorized server-side using the authenticated account, active membership, role, resource organization, operation and any resource-specific scope. Random IDs, caller ID, workflow text and model output are not authorization.

Candidate role names for discussion only:
- **Owner:** manage organization, membership, route and billing settings.
- **Admin:** configure/publish workflows and integrations within granted scope.
- **Operator:** review calls and permitted operational outcomes; no implied ability to publish workflows or change billing.
- **Reviewer:** read only explicitly allowed records.
- **Support operator:** separate platform-side support role, least privilege and audited time-bounded access.

Do not finalize these roles until owner workflows, support model and data visibility are reviewed. Invitations, role changes and member removal need auditable, revocable state. A removed or downgraded member must lose access at the server-enforced policy boundary, including exports, search, background jobs and existing sessions as defined by the approved session policy.

## 4. Workflow definition and publication lifecycle

Candidate lifecycle, not yet approved:

`draft → validated → test-ready → published → paused → retired`

This is not necessarily a strictly linear machine. Validation may fail; a published version may be paused; an eligible prior version may be restored only through an explicit, audited operation. The product must define whether a new call can be admitted while a workflow is paused, retired or awaiting provider capability verification.

Minimum contract expectations:
- Workflow blocks are typed, schema-validated and allowlisted.
- A workflow may only refer to server-registered connector operations and approved policy choices.
- The configuration stores prompts/content separately from system policy, organization authorization and connector credentials.
- Validation checks required fields, supported branches, action scopes, timeout/fallback paths and incompatible combinations before publication.
- Each publish creates an immutable version, actor, timestamp, schema version and audit event.
- Each call execution is pinned to one workflow version. Updates do not mutate the active execution's behavior unless an explicit reviewed migration policy says otherwise.
- Test mode uses synthetic fixtures by default and cannot cause real connector side effects unless separately authorized and clearly gated.
- Pause of a workflow is not equivalent to verified disablement of the telephony route.

## 5. Caller matching and verification

Caller-number matching may identify candidate customer records, but is not proof of identity. Each workflow must state whether it:
1. performs general, non-sensitive intake without customer lookup;
2. matches a customer record but does not disclose protected information; or
3. requires a reviewed verification step before any protected disclosure or consequential action.

The verification method, retry limit, fallback and permitted disclosures are open decisions. If verification fails, is unavailable or is ambiguous, protected data/actions remain unavailable. The system must not ask the model to invent a verification result or infer identity from conversational confidence/voice alone. Legal and privacy review is required for the selected deployment jurisdiction and data flow.

## 6. Canonical call observation and outcome model

Keep **source event**, **session state**, **workflow result**, **action result** and **dashboard classification** separate. Candidate business-visible outcomes:

| Outcome | Minimum evidence rule | Must not be conflated with |
| --- | --- | --- |
| Assistant handled | Authoritative evidence of assistant connection plus defined terminal handling result | Call offered, workflow merely started, or ticket action alone |
| Caller abandoned | Evidence of caller disconnect/abandonment before the defined completion point | Provider failure or no observation |
| Missed before assistant connection | Reliable provider/carrier evidence of an offered/incoming call and evidence the assistant did not connect | No call record or a dashboard gap |
| Route/provider failure | Evidence classifies failure in route/provider delivery or connection | Caller abandonment or model failure |
| Assistant/workflow failed | Session was observed and a defined assistant/workflow failure occurred | Unknown status or provider failure |
| Action pending/unknown | Connector action may have occurred but authoritative final result is absent or conflicting | Action failed or succeeded |
| Action confirmed | Authoritative connector result/reference confirms the side effect | Model claim, request accepted, HTTP timeout or locally generated identifier |
| Unobserved/coverage unknown | Source coverage cannot establish whether all relevant calls/events were seen | Zero calls or zero missed calls |

These labels are proposed vocabulary, not final analytics taxonomy. Exact event sources, precedence rules, denominator and retention remain open. Do not advertise “all missed calls captured” until provider/carrier coverage is documented and validated for the selected route.

## 7. Connector action contract

A connector operation must be registered server-side with a typed input/output schema, explicit organization/resource scope, authorization rule, timeout, idempotency behavior, audit fields and authoritative result definition.

Candidate action states:
`not_requested → requested → pending → confirmed | failed | unknown/reconciliation_required`

The exact transition graph depends on the connector. An ambiguous timeout after a write may mean the side effect succeeded. Retry must use a supported idempotency key or query/reconciliation operation; otherwise hold the result as unknown and require a safe recovery path. Do not create a duplicate ticket just to make the UI look complete. Do not present a ticket reference as confirmed unless it is supplied by the trusted system of record.

Ticket/case creation remains a candidate action; no provider or ticket system is selected by this contract.

## 8. Dashboard metrics and evidence provenance

Before a metric is shown to a customer, document:
- definition and event source;
- numerator, denominator and excluded/unknown cases;
- tenant/resource scope and authorization;
- event-time versus receive-time semantics;
- freshness and late-event reconciliation;
- behavior when source coverage is incomplete;
- whether it is observed, estimated or unavailable.

A dashboard must not convert “no event received” into “no call happened.” Unknown and reconciliation-required states should be visible in operational views and excluded or separately represented in success metrics according to a reviewed definition.

## 9. Minimum domain events to evaluate

Candidate event names for discussion, not a required event bus or final schema:

- `organization.membership_changed`
- `workflow.version_validated`, `workflow.version_published`, `workflow.paused`, `workflow.retired`
- `call.observed`, `call.session_started`, `call.session_ended`, `call.outcome_reconciled`
- `workflow.execution_started`, `workflow.execution_completed`, `workflow.execution_failed`
- `caller.verification_requested`, `caller.verification_passed`, `caller.verification_failed`
- `connector.action_requested`, `connector.action_confirmed`, `connector.action_failed`, `connector.action_reconciliation_required`
- `usage.event_recorded`, `usage.adjustment_recorded`

Every accepted event should include an internal event ID, organization scope where known, source/provider identity where relevant, source event ID/idempotency key, occurred-at and received-at times, correlation ID, schema version and minimal safe metadata. Do not store full provider payloads or caller content by default.

## 10. Mapping to existing requirements and scenarios

- **REQ-001/002:** separate workflow publication from route activation and require evidence-scoped route eligibility.
- **REQ-003:** expand or split for typed workflow schema, immutable versions, publication and execution pinning.
- **REQ-004/010:** caller disclosure, caller verification and data-policy decisions must not be inferred from account consent.
- **REQ-005/013/015:** map authoritative call observations and source-specific outcome classification.
- **REQ-011/016:** distinguish account authentication from organization membership, role authorization and caller verification.
- **REQ-012:** require typed allowlisted connector operations and authoritative action confirmation.
- **REQ-008/009:** preserve outcome provenance and usage-event reconciliation.
- **NFR-002/003/004/006/007:** define coverage denominators, workflow outcomes, service boundary, business workload and full variable cost.
- **BPA-001–BPA-018:** remain planned scenarios; this document does not execute or pass them.

See the business assistant coverage gap audit for the recommended requirement revision plan.

## 11. Open decisions and approval gates

1. Initial target segment, geography and one highest-value workflow.
2. Supported business-number route and provider event/media coverage.
3. Organization roles, invitations, member removal and support-access model.
4. Canonical workflow block schema, validation policy and publication/rollback semantics.
5. Caller matching and verification requirements by data/action risk.
6. First trusted connector and authoritative success/reconciliation interface.
7. Call observation coverage, canonical outcomes and dashboard metric definitions.
8. Data classes, retention/deletion targets, notice/consent requirements and qualified legal review.
9. Business workload, peak concurrency, billable unit, comparable provider quotes and pricing.
10. Approved acceptance thresholds, verification evidence and named operational owners.

## 12. Approval status

This is a consistency contract for further discovery. It is not customer validation, a legal opinion, a provider capability statement, a finalized schema, a production design or authorization to implement. Phase 0 remains incomplete; all acceptance scenarios remain NOT RUN.
