# UX Screen Inventory and Journey Requirements

**Status:** Draft discovery artifact. No visual design is approved; no implementation is authorised. Android-first remains a proposal subject to telephony feasibility.

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