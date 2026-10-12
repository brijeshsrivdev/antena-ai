# Architecture/API/Data/Security Semantic Review

**Review date:** 2026-10-12  
**Status:** Documentation review; findings are not owner-approved architecture decisions.  
**Scope:** Semantic consistency across system architecture options, API contract, data model, core requirements, traceability, capability governance, threat model and data lifecycle.  
**Repository constraint:** Discovery only. No product code, deployment, real-world experiments, provider outreach, interviews or legal opinions are authorised by this review.

## Executive assessment

The draft architecture has sound high-level boundaries: the client is untrusted for permissions, domain systems remain authoritative, tool execution is server-authorised, provider events are verified/idempotent, and raw call content is separated from ordinary telemetry. The main risk is not a missing top-level component; it is that several critical guarantees are stated in prose but are not yet represented as explicit contract states, records or verification obligations.

Two concrete contract gaps have been clarified in the working drafts:
- The API contract now names account-session listing/revocation and account-recovery operations, reflecting REQ-016.
- The data model now distinguishes account sessions and recovery challenges, and separates account-holder consent/choices from caller-facing disclosure events.

These are conceptual corrections only. They do not choose an identity provider, establish lawful caller processing, or approve a schema.

## Findings

| ID | Severity | Finding | Required disposition before baseline approval |
|---|---|---|---|
| SEM-001 | P0 | **Account authentication requirement exceeded its data/API representation.** REQ-016 required recovery and revocation, while the earlier API/data drafts had only a generic identity link and no explicit session/recovery lifecycle. | The API and data drafts now include candidate operations/entities. Still choose the auth mechanism, recovery factors, session policy, support recovery process and abuse limits; verify with negative tests before internal MVP. |
| SEM-002 | P0 | **Account, profile owner and domain tenant are not the same concept.** The data model uses account_id, while future capability policy also speaks of tenant scope. A user may act for a hospitality tenant, but personal-account ownership does not establish business-tenant authority. | Specify principal-to-tenant membership, roles, delegation and revocation only when the future hospitality scope is investigated. Each connector call must derive tenant scope from trusted server-side authorization, never from model output or an arbitrary client field. Keep domain connectors outside the personal-assistant critical path. |
| SEM-003 | P0 | **Account-holder consent/choices and third-party caller notice are easy to conflate.** A user's acceptance of product terms or enabling a route cannot prove that a caller heard a disclosure or that a legal consent condition was met. | Drafts now name a separate CallerDisclosureEvent concept. Define route-specific evidence and caller notice behavior only after route/provider and jurisdiction are known; obtain counsel review. Do not label a disclosure event as consent unless the reviewed policy supports that meaning. |
| SEM-004 | P0 | **Call identity and state transitions remain underspecified.** One user-visible call may include forwarding, provider, bridge and takeover legs; events can be duplicated, delayed or arrive out of order. A single provider_call_ref may not represent all legs. | Define canonical call/session IDs, provider-leg mapping, allowed state transitions, terminal-state precedence, late-event handling and reconciliation. Tests must cover crossed events, duplicate starts/ends, provider/local state disagreement and route deactivation during an active call. |
| SEM-005 | P0 | **Route activation, verification and disable need a precise contract.** “Disable route” could mean the app stopped processing, the provider configuration changed, or carrier forwarding was restored; these are materially different outcomes. | Use explicit states such as requested, pending, verified-active, degraded, disable-requested, disabled-verified, and restoration-unverified only if supported by the selected route. Report what was actually confirmed and provide safe manual recovery instructions when remote verification is impossible. Do not claim automatic restoration without evidence. |
| SEM-006 | P0 | **Deletion completion is a distributed lifecycle, not a single database status.** The API and data model acknowledge providers, exports, caches and backups, but the product's completion semantics and exception handling remain open. | Define per-data-class deletion behavior, provider request/confirmation states, retries, accountable owner, backup expiry, legal exceptions and user-facing completion language before promising an SLA. Distinguish “removed from primary systems” from “all downstream copies confirmed deleted.” |
| SEM-007 | P0 | **Usage ledger idempotency and billing correction are directionally sound but need a canonical event contract.** Provider event IDs may be missing, repeated or revised; usage can arrive after a call is marked terminal. | Specify provider/event-key construction, uniqueness scope, immutable adjustment entries, reconciliation states and the policy for missing/unmatched events. Keep connected minutes distinct from AI-active minutes and provider-billed units. Reconcile against invoices before paid pilot. |
| SEM-008 | P1 | **Authentication/session lifecycle is not yet fully traceable.** The requirements mention revocation, expiration, recovery and risky-event auditing; architecture and test mapping must name the corresponding API/data records and scenarios. | REQ-016 traceability now names AccountSession, RecoveryChallenge, session/recovery operations and AuditEvent. Keep exact protocol and durations open until owner review. |
| SEM-009 | P1 | **Privacy-safe observability is stated but not operationally specified.** “No raw content by default” does not define redaction, correlation, access control or which metadata is safe. | Create a field-level logging allowlist and redaction policy before implementation; test logs/traces for phone numbers, tokens, transcript snippets, profile context and provider payloads. Correlation IDs must not become cross-user lookup authority. |
| SEM-010 | P1 | **Provider callback authentication and authorization must be distinct.** A valid signature proves origin/integrity according to the provider protocol, but does not alone prove that a callback belongs to the expected account, route, session or current state. | Preserve signature/replay checks, then validate provider account, route/session mapping, event type, state transition and idempotency before side effects. Unknown or mismatched events must fail safely and alert without exposing content. |
| SEM-011 | P1 | **Export and support access are high-risk alternate read paths.** Object-level API authorization is insufficient if background exports, support tooling, generated download links or retries bypass it. | Apply the same account/tenant authorization and audit rules to jobs, object storage, exports and support tools. Use short-lived scoped downloads and test revoked access and cross-account identifiers. |
| SEM-012 | P1 | **Recovery and urgent route-disable paths need an independence check.** If account takeover or a lost device prevents login, a dashboard-only disable path may not help the user restore phone behavior. | Compare supported recovery/disable mechanisms after a route is selected. Document limitations and a tested manual carrier/operator fallback; do not promise a recovery channel until validated. |

## Cross-document contract alignment

| Concern | Current draft alignment | Still open |
|---|---|---|
| Authentication/recovery | REQ-016; API account/session and recovery operations; AuthIdentity, AccountSession, RecoveryChallenge; AuditEvent | Provider, factor, session duration, recovery support and test thresholds |
| User/account versus tenant | Capability governance says server-side tenant isolation; API and data model use account ownership | Membership/delegation model and hospitality authorization matrix |
| Caller disclosure versus account consent | ConsentRecord described as account-holder choice; CallerDisclosureEvent introduced as separate concept | Route-specific event meaning, notice content, lawful basis and retention |
| Call/provider event lifecycle | CallSession, CallEvent, webhook signature/replay/idempotency rules exist | Provider-leg model, event ordering, terminal precedence and route-specific state machine |
| Usage and billing | UsageEvent has idempotency/reconciliation; requirements require limits | Canonical billable event schema, late adjustments and invoice reconciliation |
| Deletion | API request workflow and lifecycle states are represented | Data-class retention, downstream confirmations, backup expiry, exception policy and SLA |
| Tool governance | Capability allowlist, typed schemas, server-side authorization, confirmation and audit are described | Concrete operation inventory and tenant/scope matrix; future Antena capability audit |
| Telemetry | Content-free logs by default and observability requirement are present | Field allowlist, redaction tests, retention, privileged access and alert ownership |

## Follow-up artifact

Added [STATE_AND_EVENT_CONTRACTS_DRAFT.md](../architecture/STATE_AND_EVENT_CONTRACTS_DRAFT.md) to make call/session, routing, deletion and usage-reconciliation states explicit. Its states are conceptual and provider-neutral; route-specific transitions, retention SLAs and billable units remain unapproved.

## Recommended order for remaining desk-only work

1. Resolve the semantic contract items that can be clarified without route/provider decisions: account-versus-tenant vocabulary, call/session/provider-leg glossary, event idempotency key scope, and the distinction between disclosure and consent.
2. Map each P0 requirement to an explicit API operation, data record/state, threat/privacy control, failure scenario, and verification artifact; leave unavailable route-specific mappings visibly blocked.
3. Define state diagrams and event tables as draft artifacts for call lifecycle, routing lifecycle, deletion lifecycle and usage reconciliation. Do not select provider-specific transitions without evidence.
4. Reconcile API/data-model contracts with UX claims so the UI never promises verified route state, deletion completion, transcript availability or successful takeover without authoritative state.
5. Re-run identifier/reference, table-shape and local-link checks after edits.
6. Present unresolved owner decisions and external-evidence blockers; do not convert this review into architecture approval.


## P0 requirement coverage conclusion

| Coverage group | Requirements | Current conclusion |
|---|---|---|
| Partial contract coverage | REQ-001, REQ-003, REQ-005, REQ-008, REQ-009, REQ-011, REQ-014, REQ-015, REQ-016 | Draft API/data/state references exist, but at least one key design, evidence or verification item remains open. |
| External-evidence or review blocked | REQ-002, REQ-004, REQ-006, REQ-010 | Route/provider capability, legal review, performance evidence or deletion/retention policy is still needed. |
| Conditional | REQ-007 | Do not promise takeover unless the selected route supports it and tests verify the outcome. |

Cross-cutting verification must include duplicate and out-of-order provider events, verified-vs-requested route state, partial downstream deletion, usage/invoice mismatches, cross-account export access, recovery replay, and privacy-sensitive log leakage. The traceability matrix records current risk and verification references; this coverage conclusion does not make any requirement release-ready.

## Explicit non-findings

- This review does not establish Android cellular-audio capture or forwarding feasibility.
- It does not establish Google Play policy eligibility for any proposed route.
- It does not provide legal advice or determine caller-consent requirements.
- It does not validate provider security, retention, pricing, performance or deletion.
- It does not approve an authentication provider, database schema, API endpoint, retention period, SLO or MVP feature.
- It does not authorize interviews, provider outreach, test calls, spending, implementation or deployment.

## Exit status

**Semantic review: findings documented; baseline not ready for approval.** SEM-001 has been partially corrected in the draft contract vocabulary. SEM-002 through SEM-007 and the P1 items remain open, dependent on further documentation, owner choices or external evidence. Phase 0 remains incomplete and implementation remains unauthorized.
