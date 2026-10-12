# UX-to-State Contract Reconciliation

**Review date:** 2026-10-12  
**Status:** Documentation-only reconciliation; not approved for implementation.  
**Inputs:** `UX_SCREEN_INVENTORY.md`, `UX_WIREFLOW_SPEC.md`, `API_CONTRACT_DRAFT.md`, `STATE_AND_EVENT_CONTRACTS_DRAFT.md`, `CORE_REQUIREMENTS_DRAFT.md`, and `ARCHITECTURE_CONTRACT_SEMANTIC_REVIEW.md`.

## Executive result

The UX inventory and wireflows generally use the right safety principles, but some user-facing states are still broader or less precise than the conceptual state contracts. The UI must render the authoritative backend state and its freshness—not infer success from a tap, request acceptance, a permission grant, a timer, or a single provider-leg event.

This reconciliation is a documentation correction guide. It does not establish telephony feasibility, choose a provider, authorize optional features, or approve implementation.

## Required UX/state rules

| Area / screens | Contract-backed rule | Required user-facing distinction | Open dependency |
|---|---|---|---|
| Routing setup and activation — UX-007/008/009/010, flows A/D | Map route state to `not_configured`, `setup_pending`, `verification_pending`, `active_verified`, `degraded`, or `failed` only when the selected route supports that mapping. | A setup request or successful permission grant is not activation. Show “Verifying” until evidence confirms the specific device/operator/plan/route combination; show verification scope and last checked time. | Route/provider contract and controlled route evidence. |
| Disable and normal-call recovery — UX-010/013/021, flow C | Distinguish `disable_pending`, `disabled_verified`, and `restoration_unverified`. Disabling future assistant handling does not necessarily terminate an active call or restore original carrier behavior. | Do not show “Disabled” until assistant handling is authoritatively confirmed off. If carrier restoration is not verified, say “Assistant handling stopped; normal call routing not verified” and provide documented manual recovery steps. Avoid claiming the phone is restored. | Route-specific disable semantics and independent recovery procedure. |
| Live call and provider legs — UX-012/013, flow B | Map one user-visible call to its session and, where applicable, multiple provider/media legs. Keep requested, pending, confirmed, failed and unknown outcomes separate. | “Transfer requested” is not “Transfer complete”; “Connecting” is not “Assistant active.” For conflicting or stale events, show “Status uncertain” or a safe “Needs attention” state rather than regressing to active or implying success. | Provider event mapping, state precedence and route-specific takeover support. |
| Takeover / stop action — UX-013, flow B | Only offer takeover where the selected route is validated; use an idempotent request and wait for authoritative outcome. | After the user taps, show “Requesting takeover.” Show success only after the route confirms it; otherwise explain failure, timeout or unsupported route. Keep active-call termination distinct from disabling future calls. | Route support and takeover/termination tests; REQ-007 remains conditional. |
| Deletion — UX-019, flow F | Map UI progress to `requested`, `authorization_pending`, `in_progress`, `partial`, `primary_removed`, `completed`, or `completed_with_exception` only where the underlying workflow records these states. | “Request received” and “Removed from primary systems” are not “Deleted everywhere.” Show pending targets/exceptions in plain language and do not promise a completion time until an approved policy and provider/backup evidence support it. | Data-class retention policy, provider confirmations, backup expiry, exception policy and deletion SLA. |
| Call detail, summary, transcript/audio — UX-014/015/016, flow C | Treat summary, transcript and audio as distinct artifacts with separate availability, authorization and retention. | Distinguish processing, available, unavailable, expired, deleted and failed-to-process states where supported. A missing transcript does not mean the call failed; a summary inference must be labelled uncertain, not presented as confirmed fact. Never expose transcript/audio controls when the feature gate is off. | Product/privacy/legal gate, provider capability, retention and deletion design. |
| Usage and plan — UX-018, flow E | Distinguish provider-reported usage, internally posted ledger entries, estimates and reconciled billing. Duplicate/late events cannot create duplicate charges; corrections must be auditable. | Label delayed figures as estimates or pending reconciliation. Explain which unit is shown. At quota exhaustion, reflect the previously chosen cap policy; do not silently switch to uncapped paid usage or terminate an active call in an unsafe manner. | Written provider pricing, billable-unit contract, invoice reconciliation and approved quota behavior. |
| Sign-in, recovery and sessions — UX-003/020 | Account/session/recovery operations must be server-authoritative; recovery is rate-limited and non-enumerating; session revocation is not merely client-side logout. | Show recovery requested/pending/success/failure only from authoritative responses. Do not reveal whether an email/phone/account exists. After revocation, stale clients must not continue to imply the session remains valid. | Approved auth/recovery mechanism, session policy, support recovery and abuse tests (REQ-016). |
| Caller disclosure and privacy choices — UX-002/016/019, flow B/F | Account-holder preferences, caller-facing disclosure events, and legal consent/basis are different concepts. | Never imply that enabling a product setting proves a caller was notified or consented. Show disclosure behavior only when it is actually supported by the route and approved policy. | Route-specific disclosure behavior and jurisdiction-specific legal review. |
| Follow-up tasks — UX-017, flow C | A generated suggestion is not a completed external action. Tasks/reminders are user-confirmed; autonomous external actions remain outside the approved MVP boundary. | Use “Suggested” / “Needs your confirmation” until the user confirms. Report reminder delivery separately from task creation; do not claim external action succeeded without an authoritative result. | SCOPE-011 lacks a dedicated requirement; defer from MVP or specify and review a requirement before inclusion. |
| Contacts and call rules — UX-011, flow A/B | The core path must remain usable without contacts permission; call rules are conditional until a dedicated contract exists. | Explain when permission is optional and offer a clear no-contacts path. Never imply that contacts synced or exclusions applied until the applicable state is confirmed. | SCOPE-012 lacks a dedicated requirement; defer from MVP or specify and review a requirement before inclusion. |
| Support and operational incidents — UX-021/022 | Client-visible incident state must reflect a tracked issue/status; telemetry must avoid unnecessary call content. | Distinguish report submitted, under investigation, resolved and awaiting user action only if the support workflow tracks them. Do not ask for raw recordings as a default troubleshooting step. | Support operations, safe logging allowlist, incident ownership and runbooks. |

## Shared presentation rules

1. **Render state, not assumptions.** Every critical status needs an authoritative source, freshness indicator or stale/unknown fallback, and a safe next action.
2. **Separate request from outcome.** A successful HTTP response or accepted command may mean only that work was queued.
3. **Never collapse independent dimensions.** Route state, active-call state, artifact availability, deletion progress and usage reconciliation must not share one ambiguous “active/complete” flag.
4. **Handle stale/conflicting events conservatively.** Keep the last confirmed state and show that it may be stale, or use a reconciliation-required state; never infer success from event order alone.
5. **Make irreversible/high-impact actions explicit.** Confirm consequential deletion and account/security changes as required by the approved policy; make urgent disable easy to find.
6. **Keep sensitive content out of notifications by default.** Lock-screen previews should not reveal caller details, summaries or transcript fragments unless a separate user choice and safe platform behavior are approved.
7. **Keep conditional features visibly gated.** Transcript/audio, contact-based rules, takeover, reminders and future hospitality tools must not appear as universally available features.
8. **Use plain-language errors with safe recovery.** Never expose provider tokens, raw webhook payloads, stack traces or other users' data.

## Copy/state anti-patterns to prohibit

| Do not say/show | Unless the contract proves | Safer interim wording |
|---|---|---|
| “Assistant is active” immediately after setup | The selected route is verified active | “Setup saved — verifying route” |
| “Your phone is back to normal” after disable request | Normal carrier/operator routing was verified | “Assistant handling disable requested; normal routing not yet verified” |
| “Transfer complete” after request acceptance | Takeover/bridge result is confirmed | “Transfer requested” |
| “Deleted everywhere” after primary DB removal | All required targets are confirmed or a reviewed exception applies | “Deletion in progress” / “Primary copy removed; other copies pending” |
| “Recording/transcript available” based on a generic call record | Artifact exists, is retained and caller/account access is authorized | “Transcript unavailable” / omit the control |
| “You spent ₹X” from estimated provider events | Metric and billing source are reconciled to the defined unit | “Estimated usage; provider reconciliation pending” |
| “Reminder sent” when a task was merely generated | Reminder delivery has authoritative confirmation | “Suggested follow-up — confirm to create” |
| “Caller consent recorded” from an account setting | The approved route-specific caller evidence supports that exact meaning | “Your preference saved”; do not make a caller-consent claim |

## Verification scenarios to carry into the later test plan

- Setup permission granted but route verification fails or times out.
- Route status becomes stale during a provider outage.
- Disable request is accepted but provider/carrier state remains unknown.
- Disable is confirmed while an active call leg remains connected.
- Takeover request times out, then a late success/failure event arrives.
- Duplicate or out-of-order start/end callbacks arrive around a terminal state.
- Deletion completes in primary storage while a provider target fails; a retry later succeeds.
- A summary is available but transcript/audio is disabled, expired or deleted.
- A usage event arrives after call termination, is duplicated, or is later corrected by the provider invoice.
- Session is revoked while an export/download or stale client session is in progress.
- Recovery attempts probe account existence or replay a previously used challenge.
- Contact permission is denied and the user still needs a viable core path.

These are required scenarios for future verification planning, not tests performed in this review.

## Disposition and remaining blockers

- **Documentation alignment:** UX should use the lifecycle vocabulary and anti-patterns above; revise final wireflows only after the MVP feature gates and provider mappings are decided.
- **External evidence blocked:** supported routes, takeover, caller disclosure, provider deletion, billable units, invoice reconciliation and route restoration.
- **Owner/policy decisions open:** auth mechanism and recovery, retention and deletion exceptions, quota exhaustion behavior, optional recording/transcript, support operations and feature scope.
- **Requirement gap:** follow-up tasks/reminders (SCOPE-011) and caller/contact allowlist/denylist (SCOPE-012) need a dedicated requirement or explicit MVP deferral.
- **No release readiness conclusion:** the draft UX is not approved, Phase 0 remains incomplete, and implementation is not authorised.

## Approval status

This reconciliation is a desk review only. It authorizes no interviews, provider outreach, live route tests, spending, legal conclusions, implementation or deployment.
