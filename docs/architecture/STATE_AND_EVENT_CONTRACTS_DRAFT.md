# State and Event Contract Draft

**Status:** Conceptual state/event model for discovery; not provider-specific and not approved for implementation.  
**Date:** 2026-10-12.  
**Dependency:** Read with API_CONTRACT_DRAFT.md, DATA_MODEL_DRAFT.md, THREAT_MODEL.md and ARCHITECTURE_CONTRACT_SEMANTIC_REVIEW.md.

This document makes hidden state assumptions explicit. It deliberately avoids asserting that any chosen telephony/provider route supports every state or transition. Before implementation, select and document the supported subset for each actual provider and route.

## 1. Contract invariants

1. Separate the user-visible CallSession from one or more provider/media legs. Do not assume one provider call reference equals one complete user conversation.
2. Every state change has an authoritative source, event timestamp, receive timestamp, correlation ID and idempotency/deduplication rule.
3. Provider event authenticity is necessary but insufficient: validate provider account, route/session mapping, expected transition and current account/route eligibility before side effects.
4. Duplicate events do not duplicate tool actions, user notifications, or billable ledger postings.
5. Out-of-order events must not blindly move a terminal session backwards. Preserve the event for reconciliation and apply an explicit precedence policy.
6. Unknown or conflicting state is visible as unknown/reconciliation-required; never infer success from a request being accepted.
7. State history is auditable without storing raw audio/transcript by default.
8. A route state, call state, deletion state and usage reconciliation state are separate dimensions; one cannot stand in for another.

## 2. Call session and provider-leg lifecycle

### Candidate session states

| State | Meaning | User-facing interpretation |
|---|---|---|
| created | A validated start has been accepted and a session record exists | Setup in progress |
| connecting | The provider/media path is being established, if observable | Connecting; not yet a successful conversation |
| active | The selected route has authoritative evidence that the session is active | Assistant handling is active |
| ending | Termination has been requested but not yet confirmed | Ending; outcome pending |
| ended | An authoritative terminal event or reconciliation confirms normal termination | Call ended |
| failed | The session failed before or during service, with a classified reason | Call could not be handled or ended unexpectedly |
| reconciliation_required | Events conflict, are incomplete, or cannot safely determine state | Status uncertain; show a safe explanation |

These are conceptual states, not a promise that the route exposes every intermediate event. A provider adapter may map a provider's event vocabulary into this model only when the mapping is supported by documentation and test evidence.

### Provider-leg model

Represent each externally meaningful leg separately when the selected route has multiple call legs. A candidate leg record may contain: internal leg ID, session ID, provider and provider-account reference, opaque provider leg reference, leg role, direction, state, start/end timestamps, last authoritative event, and safe failure code. Keep raw provider payloads out of the durable model unless a specific debugging need, access policy and retention rule are approved.

Do not infer caller identity, route success, takeover success or billable duration from a leg's existence alone.

### Event processing rules

| Event class | Validation before side effects | Duplicate/out-of-order handling |
|---|---|---|
| Session/leg started | Signature/authenticity, provider account, expected route mapping, allowed initial state | Deduplicate by provider event identity or approved fallback key; never create a second session for a duplicate |
| Media connected/disconnected | Match leg to session and current state; enforce media deadlines | Preserve timestamps; a late connect cannot revive a confirmed terminal session without reconciliation |
| Takeover/bridge requested | User authorization, route capability, active session, idempotency key | One logical request per key; report requested separately from confirmed outcome |
| Takeover/bridge result | Trusted provider event and matching request/leg | Do not claim success from request acceptance alone; reconcile contradictory results |
| Session/leg ended | Trusted event, mapping, valid terminal transition | Duplicate ends are no-ops for billing/action side effects; retain minimal event evidence |
| Provider error/timeout | Provider-specific mapping and correlation | Classify transient vs terminal only when supported; bounded retries, no duplicate external actions |

### Reconciliation requirements

- Define which source wins when provider events conflict with local timeout/termination decisions.
- Keep occurred_at separate from received_at; do not trust an unvalidated client timestamp.
- Record a safe reason when state is unknown or reconstructed.
- Define how late billable events attach to already-ended sessions.
- Test duplicate starts/ends, missing end events, event replay, clock skew, concurrent callbacks, provider-leg swaps, and termination during takeover.
- The session state machine must not promise an emergency-calling guarantee or any other capability not proven by the chosen route.

## 3. Routing lifecycle

### Candidate route states

| State | Meaning | Required product behavior |
|---|---|---|
| not_configured | No route is configured | Explain setup requirements |
| setup_pending | User requested setup and the workflow has started | Show pending, not active |
| verification_pending | Setup was attempted but end-to-end evidence is incomplete | Do not claim verified service |
| active_verified | Evidence confirms the specific supported route configuration is active | Display verification scope and last checked time |
| degraded | Previously verified route may not be working or provider status is uncertain | Explain uncertainty and present disable/recovery options |
| disable_pending | Disable was requested but not confirmed | Keep warning visible; do not claim disabled |
| disabled_verified | The supported control plane has confirmed assistant handling is disabled | Explain exactly what was disabled |
| restoration_unverified | Assistant handling is disabled or stopped, but restoration of the original carrier/operator behavior is not verified | Give documented manual recovery steps |
| failed | Setup or disable failed with a known failure class | Show safe recovery instructions and support path |

The exact states and guarantees depend on the route. In particular, disabled_verified must not imply carrier forwarding was restored unless the chosen route actually verifies that condition.

### Route transition rules

- Activation requires explicit user intent and route-specific eligibility checks.
- A test call is evidence for the tested device/operator/plan/route combination only; it is not universal compatibility.
- Route changes and disable requests are audited and idempotent.
- An active call and a routing configuration have separate state; disabling future handling does not necessarily terminate an active call.
- If status cannot be verified, show uncertainty and safe manual steps rather than inventing success.
- Define a recovery route independent enough to help when the primary device/account is unavailable, if the selected product/route can support it.

## 4. Deletion lifecycle

### Candidate states

| State | Meaning |
|---|---|
| requested | User has requested deletion; request identity and scope are recorded |
| authorization_pending | Additional authentication/authorization is needed |
| in_progress | First-party and downstream deletion tasks are running |
| partial | Some targets completed while one or more required targets failed or remain pending |
| primary_removed | The specified primary systems no longer contain the targeted data; downstream work remains |
| completed | All targets required by the approved policy have confirmed completion |
| completed_with_exception | Remaining copies are covered by a documented, reviewed exception with expiry/owner where applicable |
| rejected | Request cannot proceed under the documented policy; safe reason and review path are provided |

### Required semantics

- Define the requested scope precisely: account, profile/version, call metadata, summary, transcript, recording, exports, support data and/or other artifact.
- Track downstream target, attempt count, last result, next retry, responsible owner and safe exception code.
- Do not claim complete deletion when only the primary database row is gone.
- Define how legally required security/financial records are minimized and retained without silently preserving unrelated call content.
- Document backup expiration and vendor/provider deletion behavior before promising an SLA.
- Keep deletion job authorization and status retrieval subject to the same account-level controls as the original data.
- Test retries, partial vendor failure, inaccessible object storage, backup expiration, repeated requests and account deletion while work is pending.

## 5. Usage and billing reconciliation lifecycle

### Candidate event states

| State | Meaning |
|---|---|
| received | An event or usage record arrived but has not been trusted for billing |
| validated | Source, account/session association, units and event identity passed validation |
| posted | A unique ledger entry has been committed |
| reconciliation_pending | Provider invoice/usage statement or related event is still expected |
| adjustment_required | Evidence shows a correction is needed; do not overwrite the original ledger entry |
| reconciled | Internal ledger has been compared against the relevant provider statement and exceptions resolved |
| rejected | Event failed validation and cannot be posted; retain only safe diagnostic metadata |

### Idempotency and adjustment rules

- Define the idempotency key and uniqueness scope per provider, account/route, event type and billing period where appropriate; provider event ID alone may not be globally unique.
- Store provider-reported units and internal normalized units separately with explicit unit names.
- Distinguish connected minutes, AI-active minutes, billable call legs, rounding increments, failed-call charges, transfers and fixed/recurring fees.
- Late corrections are represented as immutable adjustment/reversal entries referencing the original entry, not destructive edits.
- A duplicate callback cannot post duplicate usage or repeat external actions.
- Provider invoice reconciliation is a required control before paid billing claims; internal arithmetic alone is not cost validation.
- Define what happens at quota exhaustion and on ledger/provider disagreement without dropping an active call unsafely.

## 6. Shared event envelope

A candidate normalized event envelope should include:
- internal event ID;
- event type and schema version;
- source/provider identity;
- provider event ID when available;
- account and session references resolved by trusted server-side mapping;
- provider-leg reference when relevant;
- occurred-at and received-at timestamps;
- correlation ID;
- idempotency/deduplication key;
- validation result and safe rejection reason;
- minimal safe metadata;
- processing state and retry/reconciliation reference.

Do not accept account, tenant, session or operation authority solely because a webhook or model payload includes those fields. Resolve and verify them against trusted server-side mappings.

## 7. Required mappings before implementation

| Contract | Requirements / risks | Evidence required |
|---|---|---|
| Call/session lifecycle | REQ-005, REQ-006, REQ-007; THR-003, THR-004, THR-017 | Provider event contract, route mapping, duplicate/out-of-order tests, failure injection |
| Routing lifecycle | REQ-001, REQ-002, REQ-014; THR-011 | Controlled route tests and documented restoration/disable behavior |
| Deletion lifecycle | REQ-010, REQ-013; THR-010; NFR-005 | Data-class retention policy, provider terms, deletion exercise and backup policy |
| Usage lifecycle | REQ-009, REQ-015; THR-012; NFR-007 | Written pricing, sample invoice reconciliation, duplicate/late-event tests and spend-limit behavior |
| Account sessions/recovery | REQ-016; THR-001 | Approved auth design and abuse/revocation tests |

## 8. Open decisions

- Which route/provider events can actually support each candidate state.
- Whether provider-leg identifiers and signed event IDs are stable and unique.
- Event retention and whether any raw payload is needed for dispute resolution.
- Terminal-state precedence and provider/local reconciliation ownership.
- Supported disable and manual restoration semantics.
- Data-class retention, deletion SLA, backup expiry and exception policy.
- Billable units, rounding rules, failed-call/transfer billing and invoice adjustment handling.
- Owners and runbooks for stuck reconciliation, deletion and provider incidents.

## Approval status

No state machine, event schema, deletion SLA, usage unit, provider mapping or recovery guarantee is approved. Use this draft to guide provider questions and later design reviews. It does not authorise provider outreach, test calls, spending, implementation or deployment.
