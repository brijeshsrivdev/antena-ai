# Product Scope and Feature Catalogue — Draft for Discovery

**Status:** PROPOSED; not owner-approved. This is a discovery hypothesis, not a final MVP commitment. No implementation is authorised.

## 1. Product hypothesis

A configurable AI business phone assistant lets a business define bounded workflows for eligible inbound calls, use authorized customer data/actions, and review what happened through a tenant-isolated dashboard. Value depends on reliable business-number routing, useful workflow completion, caller trust, safe actions, operational visibility and affordable per-minute economics—not simply on generating speech.

## 2. Candidate first-release persona

**Primary persona hypothesis:** an owner or operations/support lead at a small or mid-sized business that receives repetitive inbound customer calls and needs consistent intake, action capture and visibility into outcomes.

This is not yet a validated segment. Interviews must compare candidate business types, call volume, workflow value, existing phone systems, support tooling, willingness to pay and operational risks. Personal AI call-assistant users are a later candidate segment, not the primary MVP.

## 3. Candidate MVP capabilities

| ID | Capability | Priority hypothesis | Why it may matter | Key uncertainty / acceptance direction |
|---|---|---|---|---|
| SCOPE-001 | Account, authentication and recovery | P0 | Protects personal profile and call records. | Choose authentication and recovery after threat model; acceptance includes account isolation and recovery abuse tests. |
| SCOPE-002 | Assistant profile setup | P0 | Lets users define name, language, tone and allowed behaviour. | Keep structured and constrained; no arbitrary client tool definitions. |
| SCOPE-003 | Personal context form | P0 | Gives the assistant relevant facts and boundaries. | Define minimum fields, sensitivity, versioning, review and deletion; context never grants permissions. |
| SCOPE-004 | Routing/forwarding onboarding and verification | P0 | The core experience depends on calls reaching the service. | Must be tested by carrier/SIM/device; clear activation, test call, status and deactivation. |
| SCOPE-005 | Live call handling | P0 | Core product value. | Requires proven two-way audio route, latency, turn-taking, interruptions and fallback. |
| SCOPE-006 | Caller disclosure and safe response policy | P0 | Protects caller trust and constrains harmful or misleading actions. | Exact wording and legal basis require review for launch jurisdiction. |
| SCOPE-007 | User takeover / transfer or end-call control | P0 candidate | Users need agency over high-value calls. | Must prove technical feasibility; do not promise until tested. |
| SCOPE-008 | Post-call summary and intent | P0 candidate | Turns conversation into actionable context. | Accuracy, uncertainty, sensitive-content handling and user correction must be tested. |
| SCOPE-009 | Call history and search | P1 candidate | Helps users retrieve previous conversations. | May be paid or deferred; retention and indexing costs require review. |
| SCOPE-010 | Full transcript/audio playback | P1 candidate | Offers detail beyond summary. | High privacy/storage/cost burden; explicit controls and legal review. |
| SCOPE-011 | Follow-up reminders/tasks | P1 candidate | Converts calls into next actions. | Start with user-confirmed reminders; no unapproved commitments or external actions. |
| SCOPE-012 | Caller/contact allowlist and denylist | P1 candidate | User controls which calls are handled. | Contact access minimisation, sync and false-positive risks. |
| SCOPE-013 | Usage meter and plan limits | P0 | Variable voice costs require predictable limits. | Accurate billing events, warnings, overage and safe exhaustion behaviour. |
| SCOPE-014 | Data export, deletion and retention settings | P0 | Trust and compliance foundation. | Deletion must cover primary storage, provider data and documented backup lifecycle. |
| SCOPE-015 | Abuse report and support | P0 | Call-handling errors and impersonation can cause harm. | Clear incident, dispute and urgent disable paths. |
| SCOPE-016 | Multi-language and code-switching | P1 candidate | Potential differentiator in India. | Enable only languages passing end-to-end quality tests. |
| SCOPE-017 | Voice cloning / imitation | Excluded from initial scope | High impersonation and fraud risk; not required to prove core value. | Revisit only with compelling evidence and separate consent/security review. |
| SCOPE-018 | Outbound calls initiated by assistant | Deferred | Adds telecom, consent, abuse and cost complexity. | Separate legal/provider gate; not a core first-release assumption. |
| SCOPE-019 | Domain profiles and connectors | Deferred after core validation | Enables future specialisations. | Trusted server-side tool registry and least-privilege permissions. |
| SCOPE-020 | Hospitality profile using Antena APIs | Future expansion | Reuses Antena domain capabilities. | Requires API capability audit and tenant-scoped auth; no direct database access. |
| SCOPE-021 | Advocate/legal profile | Deferred | Different professional duties and sensitive data. | Requires separate discovery, professional/legal review and integration boundary. |

## 4. Explicit first-release exclusions (proposed)

- No unrestricted cellular call-audio capture assumption.
- No arbitrary caller-provided or client-provided backend URL, SQL, scripts or tool permissions.
- No autonomous commitments, purchases, financial/legal advice, or external side effects without an explicit, scoped permission and suitable confirmation.
- No voice cloning by default.
- No automated promotional outbound calling.
- No legal/advocate profile dependency.
- No direct access from the AI layer to Antena or any other domain database.
- No “unlimited minutes” plan without verified economics and controls.
- No claim that all carriers, countries, devices or languages are supported until tested.

## 5. Core end-to-end journey hypothesis

1. Business creates an account and configures authorized team access.
2. Business connects a phone number through a supported and verified route.
3. Business configures and tests a versioned workflow using approved blocks and connectors.
4. Eligible caller reaches the assistant; the platform resolves the tenant and published workflow from trusted configuration.
5. Assistant discloses its AI role under the approved policy, identifies intent and follows bounded workflow steps.
6. Caller identity is matched and verified according to policy before protected customer data is disclosed.
7. The assistant records a complaint/enquiry and may invoke an authorized connector; writes are confirmed only from authoritative results.
8. The dashboard shows call outcome, summary, workflow version, action/ticket status and pending failures.
9. Authorized business users can correct supported fields, review audit history, request data lifecycle actions and pause/disable handling.
10. Usage is metered transparently with server-enforced limits and safe exhaustion behavior.

Each step needs normal, alternate, error, timeout, recovery and accessibility states in the UX spec.

## 6. Safety and trust invariants

- Profile instructions are untrusted data and cannot expand tool permissions.
- The assistant should state uncertainty and ask the caller to repeat/clarify rather than fabricate.
- Emergency or highly sensitive scenarios require a defined safe policy; exact scope needs legal/product review.
- No action that materially commits the user should happen without an approved authorization and confirmation model.
- User can disable call handling through a clear, documented path.
- Call content is tenant-isolated and excluded from model training by default unless an explicitly reviewed, informed opt-in policy says otherwise.
- Logs should avoid raw audio/transcript content by default.
- A provider outage must not create silent call misrouting.

## 7. Validation required before baselining scope

- Evidence that the chosen segment has frequent, consequential call-handling pain.
- Competitor review and feature parity decision.
- Carrier/telephony path feasibility and safe fallback.
- Caller disclosure, recording and data-processing legal review.
- End-to-end latency and speech quality thresholds.
- Verified unit economics and usage limit hypotheses.
- UX walkthrough and accessibility review.
- Numbered requirements with testable acceptance criteria.
- Owner approval of final MVP scope.

## 8. Decision status

All priorities and scope choices in this file are proposals. Owner approval is required before they become a committed product baseline.

## Business workflow direction reconciliation — 2026-10-13

The primary MVP hypothesis is a configurable AI business phone assistant, not a personal assistant. The candidate first-release buyer is a business owner or operations/support lead; the end customer is the caller. See [`BUSINESS_PHONE_ASSISTANT_PRODUCT_DIRECTION.md`](BUSINESS_PHONE_ASSISTANT_PRODUCT_DIRECTION.md) for the detailed actor vocabulary, call journeys, workflow building blocks, complaint example, missed-call semantics and dashboard concepts.

Important additions to discovery: define a versioned workflow model and safe publication lifecycle; verify caller identity before protected disclosure; choose and contract-test a first typed connector before promising ticket creation; distinguish calls not observed by the platform from calls observed but missed/failed; and give each dashboard metric an authoritative event source and denominator. These remain proposed scope and do not authorize implementation.
