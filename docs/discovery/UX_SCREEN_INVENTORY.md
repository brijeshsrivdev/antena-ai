# UX Screen Inventory and Journey Requirements

**Status:** Draft discovery artifact. No visual design is approved; no implementation is authorised. The inventory originated from the personal-assistant hypothesis. For the primary business assistant, web/dashboard versus mobile form factor remains undecided; Android-first is not an accepted default.

## 1. UX principles to validate

- Make the call-routing state unmistakable: Off, Setup needed, Testing, Active, Degraded or Failed.
- Treat activation and deactivation as high-risk actions; explain consequences and offer a clear recovery path.
- Explain what the assistant can say/do, what it cannot do and when a caller will hear AI disclosure.
- Make privacy controls understandable: audio, transcripts, summaries, retention and deletion are distinct.
- Do not promise support for a carrier, SIM, language or takeover flow until verified.
- Make variable usage visible before it creates a surprise bill.
- Show uncertainty in summaries and let users correct inaccurate details.
- Avoid showing private call content on a locked screen by default.
- Support accessible typography, contrast, screen readers, large touch targets and language clarity.

## 2. Screen inventory

| Screen ID | Screen / state | Main user goal | Required states / edge cases |
|---|---|---|---|
| UX-001 | Welcome / value proposition | Understand what the assistant does and its limits. | Loading, offline, supported-region notice, unsupported-device/route notice. |
| UX-002 | Trust and privacy explanation | Understand routing, AI disclosure, data use and controls. | Notice version, links to full terms/privacy, consent withdrawal. |
| UX-003 | Sign-up / sign-in | Securely access account. | Invalid input, OTP delay/expiry, rate limit, account recovery, network failure. |
| UX-004 | Profile setup | Define name, language and speaking style. | Unsupported language, invalid values, preview failure, save/retry. |
| UX-005 | Personal context form | Add useful facts, preferences and boundaries. | Empty/partial form, sensitive data warning, save/version history, delete/edit. |
| UX-006 | Assistant permissions / system role | Grant only necessary OS permissions. | Denied, permanently denied, ineligible role, OS version mismatch, recovery to settings. |
| UX-007 | Routing method selection | Choose a supported route for device/carrier. | Unsupported operator, dual-SIM ambiguity, no valid route, VoIP alternative if offered. |
| UX-008 | Forwarding setup guide | Configure the carrier route. | Per-carrier instructions, copy action, failed USSD/MMI, carrier rejection, cancel. |
| UX-009 | Test call and verification | Confirm that the route works before activation. | Success, no answer, wrong destination, caller ID mismatch, timeout, retry, support escalation. |
| UX-010 | Assistant status dashboard | Know whether calls are handled. | Off, setup needed, active, degraded, failed, provider outage, status stale. |
| UX-011 | Caller handling preferences | Define allowed/blocked categories and personal boundaries. | No contacts permission, duplicate contacts, sync error, fallback policy. |
| UX-012 | Live call event/status | Understand what is happening during an eligible call. | Connecting, AI active, transfer requested, user takeover, provider failure, disconnect. |
| UX-013 | Takeover / stop controls | Reclaim control or stop assistant. | Transfer unsupported, delay, failure, accidental tap, confirmation where needed. |
| UX-014 | Call history | Find prior handled calls. | Empty, loading, pagination, search no result, deleted record, access denied. |
| UX-015 | Call detail / summary | Understand caller intent and outcome. | Low-confidence summary, missing transcript, processing failed, user correction. |
| UX-016 | Transcript / audio playback | Review call details where enabled. | No recording, consent state, playback error, restricted content, retention expiry. |
| UX-017 | Follow-up tasks | Review and confirm suggested next steps. | Duplicate task, failed reminder, unsupported external action, user edit/cancel. |
| UX-018 | Usage / plan / billing | Understand consumption and limits. | Meter delay, limit warning, payment failure, plan expired, dispute/refund path. |
| UX-019 | Privacy and data controls | Manage recording, retention, export and deletion. | Pending deletion, provider deletion failure, export expiry, re-authentication. |
| UX-020 | Account and security | Manage sessions, devices and recovery. | New device, session revocation, suspicious login, lost device. |
| UX-021 | Help / support / report issue | Recover from routing or AI mistakes. | Urgent disable path, ticket status, abuse report, provider incident. |
| UX-022 | Notifications and permission status | Understand setup and usage events. | Notification denied, stale state, duplicate alert, private lock-screen content. |

| UX-023 | Organization creation / join / membership | Create or join the correct business workspace and understand access. | Invitation expired, wrong organization, no active membership, revoked membership, duplicate invite, account belongs to multiple organizations. |
| UX-024 | Team roles and access | Understand and manage who may view calls, publish workflows, configure routes, manage integrations, export data or change billing. | Least-privilege role, unauthorized action, role downgrade/removal, stale session, audit history, support access. |
| UX-025 | Workflow list / builder / validation | Configure an inbound workflow using only supported blocks. | Empty draft, invalid fields, unsupported block, unauthorized action, validation failure, synthetic-test failure, no external side effect in test mode. |
| UX-026 | Workflow version / publish / pause / retire | Review changes and control which workflow version handles new calls. | Draft versus published, pending publication, rejected version, rollback policy, active-call version pinned, workflow pause distinct from route disable. |
| UX-027 | Business-number route setup and status | Understand route eligibility and whether the route is active, degraded or unverified. | Provider/number unsupported, route test failed, event coverage unknown, disable requested/pending/confirmed/unverified, normal-call recovery. |
| UX-028 | Business call inbox and filters | Find calls needing review without overstating what the system observed. | Assistant-handled, caller-abandoned, missed-before-connection, route/provider failure, unknown/conflicting event, unobserved coverage limitation, stale data. |
| UX-029 | Business call detail / workflow result | Understand what happened, which workflow version ran and which facts remain uncertain. | Missing events, low-confidence extraction, wrong/multiple customer matches, caller verification failed, partial workflow, summary unavailable, tenant access denied. |
| UX-030 | Connector setup and action reconciliation | Understand which approved business integration is connected and whether an action actually succeeded. | No connector selected, insufficient scope, credential expiry, denied operation, pending/unknown write, duplicate prevention, authoritative success/failure, disconnect/reconcile. |
| UX-031 | Business overview and metric definitions | Understand service health, call outcomes, workflow results and usage. | Metric source/freshness, denominator/exclusions, unknown events, late correction, zero-data state, provider outage separated from assistant outcome. |
| UX-032 | Caller verification branch (conversation state) | Complete an approved verification step before protected disclosure or action. | Zero/one/multiple customer matches, verification unavailable/failed/abandoned/disputed, retry limit, safe fallback, no protected-data leakage. |
| UX-033 | Workflow action result / ticket reference | Review a confirmed external action or resolve an ambiguous outcome. | Action not requested/denied/pending/confirmed/failed/unknown; do not show a ticket reference before authoritative confirmation. |

## 3. Critical user flows

### A. First-time activation
Welcome → trust/privacy explanation → sign-in → profile/context → permission eligibility → routing method → setup guide → test call → verified status → explicit activation.

Activation must not be inferred from opening the app or granting a permission. If route verification fails, clearly show that the service is not active and explain how to restore normal calling.

### B. Call handling
Eligible incoming call → route/connection → caller AI disclosure → policy-bounded conversation → optional user takeover/end → call termination → summary/records → usage update.

Failure branches must include no audio, caller ID unavailable, model timeout, provider outage, silence, abusive caller, emergency cue, transfer failure and concurrent call capacity exhaustion. Each branch needs a defined response and audit event.

### C. Deactivation and recovery
Dashboard → disable assistant → deactivate/restore forwarding instructions or supported network control → test normal call → show verified off status. If deactivation cannot be confirmed automatically, say so explicitly and provide carrier-specific steps and support.

### D. Deletion
Privacy settings → choose data categories → explain effects → re-authenticate if needed → confirm → show pending/completed status → verify deletion across first-party and provider systems under documented retention/backup schedules.

## 4. Visual design work required later

Before implementation, create:
- Information architecture and navigation map.
- Low-fidelity wireframes for each P0 journey.
- High-fidelity screens for onboarding, routing status, live call state, summary, usage and privacy.
- Design tokens, typography, spacing, colour/contrast and components.
- Content guidelines for caller disclosure, errors, uncertainty and safety.
- Responsive/accessibility rules and reduced-motion behaviour.
- Testable visual acceptance criteria and annotated failure states.

## 5. UX validation plan

Conduct moderated walkthroughs with target-segment participants after problem interviews. Ask users to explain the routing state, find the disable control, describe what gets recorded, interpret a low-confidence summary and understand minute limits. Track completion, misinterpretation, time-to-complete, confidence and points of hesitation.

No user testing is claimed to have occurred. All screens and flows are provisional until validated with customers and the selected telephony architecture.
## Scope boundary against the proposed MVP

This inventory covers candidate screens and states across the product, not a commitment to include every screen in the first release. Align with MVP_SCOPE_AND_FEATURE_GATES.md and PRODUCT_SCOPE_AND_FEATURE_CATALOG.md:
- UX-011 (caller handling preferences/contact access) is conditional/P1. The initial experience must work without contact-book permission unless research demonstrates a need and the permission/policy review approves it.
- UX-016 (transcript/audio playback) is off by default and excluded unless a separate product, privacy, legal and cost decision approves it. Its presence here only describes the state model if enabled later.
- UX-017 follow-up tasks must remain user-confirmed; do not imply autonomous external actions.
- UX-012/UX-013 live call/takeover states are route-dependent and must not be shown as available until the exact route supports them.

Before baseline approval, mark each screen as MVP, conditional, deferred or excluded in the versioned MVP list. No screen in this inventory independently authorises a feature.

## Business phone assistant screen-scope reconciliation — 2026-10-13

The existing inventory is largely personal-assistant-oriented. Before a baseline is approved, add/review business journeys for organization creation/membership and roles, phone-number/route setup, workflow list/builder/validation/test/publish/version history, call inbox/detail with outcome provenance, connector setup and action reconciliation, and organization usage/metric definitions. These are candidates, not automatically MVP screens. Workflow pause must not be represented as route disable; “missed call” and “ticket created” must only be shown when their evidence contracts support those claims. See [Business Assistant Domain Contract Draft](../architecture/BUSINESS_ASSISTANT_DOMAIN_CONTRACT_DRAFT.md).


## Business assistant wireflow reference — 2026-10-13

See [Business Assistant UX Wireflows Draft](BUSINESS_ASSISTANT_UX_WIREFLOWS_DRAFT.md) for business-admin onboarding, constrained workflow authoring/publication, caller interaction, call inbox/detail, action reconciliation, roles and uncertain/error states. This is a candidate flow, not user-validated design or an approved screen scope. The existing personal-assistant-oriented inventory needs a reviewed business-first revision before baseline approval.


## Business-first UX disposition — 2026-10-15

UX-001–UX-022 are inherited inventory IDs and contain personal-assistant-specific assumptions (profile/context, contact rules, permissions, takeover and Android routing). Do not silently reinterpret those IDs as business-admin screens. UX-023–UX-033 are proposed business-specific additions; their IDs and screen scope remain unapproved.

Primary discovery path to validate: organization membership → supported business-number route → constrained workflow draft/test/publish → route activation → caller interaction and verification as required → evidence-backed call inbox/detail → confirmed action review and reconciliation → usage/privacy/operations. The exact navigation, device form factor and first-release screen set remain open.

Ticket/case views are conditional on a selected connector. Missed-call states are conditional on verified provider/carrier event coverage. Caller verification is a workflow/conversation state as well as a UX requirement; it must not be inferred from caller ID. No screen may display fabricated metrics or claim action success without authoritative evidence.

See [Business Assistant UX Wireflows Draft](BUSINESS_ASSISTANT_UX_WIREFLOWS_DRAFT.md), [Business Phone Assistant Requirements Addendum](../requirements/BUSINESS_ASSISTANT_REQUIREMENTS_ADDENDUM_DRAFT.md), and [Business-first MVP scope matrix](MVP_SCOPE_AND_FEATURE_GATES.md). This is desk-only work; no customer walkthroughs have occurred.
