# Core Requirements Draft — Personal AI Call Assistant

**Status:** DRAFT. No formal review has started and these requirements are not approved for implementation. IDs, priorities and some acceptance thresholds remain provisional. No code is authorised.

## Requirement lifecycle note

REQ-001–REQ-015 and NFR-001–NFR-010 are stable identifiers within this working draft and are referenced by TRACEABILITY_MATRIX.md. Requirement content, priority, completeness and cross-document traceability remain draft and unapproved. Unresolved targets are tracked in ACCEPTANCE_THRESHOLD_REGISTER.md; candidate values are not approved and must be reviewed before baseline approval.

## REQ-001 — Explicit user activation and routing state
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall require an explicit user action before enabling the selected call-routing path.

Acceptance criteria:
- Given routing is not configured, the dashboard shows an inactive/setup-needed state.
- Given setup is incomplete or cannot be verified, the UI does not claim that the assistant is active.
- Given the user activates routing, the system records the activation action, configuration version, time and resulting verification status.
- Given the user disables routing, the UI reports verified-off or clearly states that deactivation could not be verified and provides the approved recovery instructions.
- Proposed usability target: the user can reach disable/recovery instructions within 2 actions from the primary dashboard (AT-001; owner approval pending).

## REQ-002 — Supported-route eligibility
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall activate only a routing method that is explicitly supported for the user's selected region, operator/plan, SIM configuration and device requirements.

Acceptance criteria:
- Unsupported combinations are identified before activation where information is available.
- The setup flow explains requirements and limitations before the user changes carrier settings.
- A test call must pass defined checks before the route is marked verified.
- Failed verification preserves an honest inactive/degraded status and provides a recovery path.
- The product does not claim unrestricted Android cellular audio capture.

## REQ-003 — Versioned assistant profile and personal context
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall store a validated, versioned profile containing only supported fields and shall keep profile text separate from system policy and permissions.

Acceptance criteria:
- Invalid profile fields are rejected with field-specific errors.
- Each saved version has an owner, version identifier and timestamp.
- A profile change affects only sessions started under the documented version policy; active-session behaviour is explicitly defined.
- Profile text cannot add tools, connectors, arbitrary URLs, SQL or permissions.
- The user can review and delete personal context under the approved retention policy.

## REQ-004 — Caller AI disclosure and bounded conversation
**Priority:** P0 candidate. **Status:** DRAFT.

Before engaging in substantive conversation, the assistant shall deliver the approved caller disclosure for the applicable jurisdiction and follow a bounded conversation policy.

Acceptance criteria:
- The disclosure wording and trigger are versioned and tested against the approved legal/product policy.
- The assistant does not falsely claim to be the account holder or a human.
- Unsupported requests, high-risk decisions and uncertain intent trigger an approved safe response or escalation path.
- Conversation termination and failure states are defined for silence, abusive content, emergency cues and provider errors.
- The system records disclosure outcome metadata without retaining unnecessary raw content.

## REQ-005 — Authenticated and authorised call session lifecycle
**Priority:** P0 candidate. **Status:** DRAFT.

The server shall associate each telephony event and session with a verified provider identity, account, route state and unique call/session identifiers.

Acceptance criteria:
- Invalid webhook signatures are rejected and audited.
- Duplicate events do not create duplicate sessions, billable usage events or side effects.
- Out-of-order connect/disconnect events result in a valid final state.
- Session creation is rejected when routing is inactive, account is suspended or quota/concurrency controls block admission.
- Session lifecycle transitions and timeout handling are specified and tested.

## REQ-006 — Real-time conversation quality and cancellation
**Priority:** P0 candidate. **Status:** DRAFT.

The voice pipeline shall support the approved interaction mode, cancellation, interruption handling and safe termination.

Acceptance criteria:
- End-to-end p50/p95/p99 latency thresholds are approved before release.
- The system handles caller interruption according to the selected provider's verified capabilities.
- Proposed cancellation target: stop downstream generation/playback within 500 ms of accepted cancellation where measurable and supported (AT-004; provider validation and owner approval pending).
- Provider timeout or media loss results in a defined fallback/termination behaviour, not indefinite silence.
- Supported languages and device/carrier combinations are listed from test evidence.

## REQ-007 — User takeover and call control
**Priority:** P0 candidate; feasibility-dependent. **Status:** DRAFT.

If the selected route supports takeover, the system shall allow an authorised user to request it and report the outcome truthfully.

Acceptance criteria:
- The UI exposes takeover only for routes where it has been validated.
- Successful takeover confirms the resulting call state.
- Failed or timed-out takeover presents a clear outcome and safe alternative.
- Repeated taps and duplicate events do not create duplicate transfers.
- If takeover cannot be delivered reliably, the feature is removed from the MVP promise and requirements are updated.

## REQ-008 — Post-call summary and uncertainty
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall produce a summary of the call outcome using only available call data and shall make uncertainty or missing data visible.

Acceptance criteria:
- Summary is linked to the correct user and call/session.
- Processing failure is represented distinctly from an empty summary.
- The summary does not fabricate missing caller identity, commitments or facts.
- The user can mark a summary incorrect and correct supported structured fields.
- Raw transcript/audio is not required to remain stored solely to render a summary after the approved retention period.

## REQ-009 — Usage ledger and cost guardrails
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall meter provider-defined billable usage and enforce account/global cost limits.

Acceptance criteria:
- Each billable event has a unique idempotency key, source provider event, account/session association, units and timestamp.
- Duplicate callbacks cannot double-charge.
- The UI labels the metric used (e.g. connected minutes) and the update delay.
- Users receive warnings at approved thresholds and the system applies the documented behaviour at plan exhaustion.
- Global and per-account spend/concurrency limits are enforced server-side.
- Billing reconciliation can compare provider usage to the internal ledger.

## REQ-010 — Privacy notice, consent and retention controls
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall apply the approved data-processing notice, consent and retention policy to each data category.

Acceptance criteria:
- The user sees the relevant notice before activating routing and before enabling optional recording/transcript features.
- The policy records notice version, consent state, timestamp and withdrawal event where applicable.
- Audio, transcript, summary, profile context and operational logs have separate retention rules.
- Deletion requests expose pending/completed status and are reconciled with provider deletion and backup schedules.
- Logs do not include raw audio/transcript by default.
- Launch cannot proceed until jurisdiction-specific legal review approves the notice and processing design.

## REQ-011 — Tenant and profile isolation
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall enforce object-level access controls for profiles, calls, summaries, usage, exports and tools.

Acceptance criteria:
- A user cannot read or mutate another user's records by changing identifiers.
- Cross-tenant isolation tests cover normal API, search, export, background jobs and provider callbacks.
- Every tool invocation is authorised server-side for the user, profile, tenant, resource and action.
- Profile text cannot grant a new permission.
- Access denials are logged without leaking sensitive record contents.

## REQ-012 — Trusted domain connector boundary
**Priority:** P1 / future profile. **Status:** DRAFT.

The AI service shall invoke only server-configured, allowlisted domain operations. Future hospitality actions shall use authenticated Antena backend APIs.

Acceptance criteria:
- Clients cannot register arbitrary connector URLs, SQL or executable tool definitions.
- Each operation has a typed schema, explicit scopes, timeout, idempotency and audit policy.
- Antena remains authoritative for hospitality business data and rules.
- Connector credentials are stored server-side and scoped to the required tenant/resources.
- Advocate/legal integrations are not enabled by this requirement and need separate discovery and approval.

## REQ-013 — Call history, transcript and recording controls
**Priority:** P1 candidate; data retention and cost dependent. **Status:** DRAFT.

The system shall expose only the call records and media permitted by the approved plan and privacy configuration.

Acceptance criteria:
- The UI distinguishes summary, transcript and recording availability.
- Unavailable, expired, deleted and failed-to-process records have distinct states.
- Access is authenticated and audited.
- Retention expiry removes or restricts the applicable artifact according to policy.
- Audio playback and transcript access are not enabled until the corresponding legal and product decision is approved.

## REQ-014 — Support, incident and urgent disable
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall provide an accessible way to report harmful handling, troubleshoot routing and disable the assistant.

Acceptance criteria:
- A user can reach the urgent disable instructions from the primary dashboard.
- Reports capture call/session IDs and issue categories without requiring the user to upload raw call content.
- Critical incidents trigger the documented escalation and containment process.
- Support tooling uses least privilege and is audited.
- Users can understand whether an issue is being investigated, resolved or awaiting their action.

## REQ-015 — Operational observability and recovery
**Priority:** P0 candidate. **Status:** DRAFT.

The system shall emit structured operational telemetry sufficient to diagnose call-routing, media, model, billing and deletion failures without unnecessarily logging call content.

Acceptance criteria:
- Metrics distinguish routing failures, provider failures, model timeouts, session termination, transfer outcomes and billing reconciliation.
- p50/p95/p99 latency and success-rate dashboards are defined for each critical stage.
- Alerts have a named owner and runbook.
- Retry policies are bounded and idempotent.
- Recovery, provider outage and deletion-job failures are tested before production.

## Non-functional requirements to baseline

| ID | Requirement area | Target to decide | Verification |
|---|---|---|---|
| NFR-001 | End-to-end response latency | p95/p99 target after benchmark | Realistic end-to-end test |
| NFR-002 | Call routing success | Threshold per supported carrier/route | Repeated carrier/device matrix |
| NFR-003 | Conversation completion | Threshold and safe-failure behaviour | Pilot telemetry |
| NFR-004 | Availability | SLO and maintenance policy | Synthetic monitoring and incident history |
| NFR-005 | Privacy/deletion | Data-specific retention and deletion SLA | Automated and provider-side deletion tests |
| NFR-006 | Capacity | Peak concurrent sessions and calls/second | Load, burst and soak tests |
| NFR-007 | Cost | Maximum variable cost per active user/minute | Provider invoice reconciliation |
| NFR-008 | Accessibility | Target standard and supported screen-reader flows | Accessibility audit |
| NFR-009 | Recovery | RTO/RPO for critical control-plane data | Restore and incident exercise |
| NFR-010 | Security | Threat-model controls and verification scope | Automated tests and independent review |

## Traceability and status

These draft requirements need trace links to customer evidence, UX screens, architecture components, privacy risks, provider capability and test cases. Numeric targets and evidence gaps are tracked in ACCEPTANCE_THRESHOLD_REGISTER.md. Do not mark APPROVED or implement until the owner reviews the complete baseline and explicitly authorises implementation.