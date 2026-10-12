# Expanded Requirements Traceability — Working Draft

**Status:** DRAFT; not approved. No implementation authorised.  
**Draft ID set:** REQ-001–REQ-016 and NFR-001–NFR-010 are stable identifiers within the current working draft and are defined in `CORE_REQUIREMENTS_DRAFT.md`. They are not yet approved baseline requirements. Priority labels remain candidates. Candidate thresholds and unresolved target decisions are tracked in `ACCEPTANCE_THRESHOLD_REGISTER.md`; none is owner-approved.

## Functional traceability

| ID | Evidence state | UX | Architecture / data | Risks | Verification and exit gate |
|---|---|---|---|---|---|
| REQ-001 Activation and routing state | Route unproven; interviews pending; AT-001 proposed 2-action disable target | UX-006 (only if route/platform requires permissions), UX-007–UX-010, UX-022 (permission/notification status and stale state) | Routing API/state machine; SupportedRouteConfiguration/RoutingConfig | THR-011, PRIV-013 | Test state transitions and disable/recovery. Gate: before live pilot. |
| REQ-002 Route eligibility | Android desk review; controlled experiment required | UX-006–UX-009 (OS permission/role is route-dependent; do not imply eligibility from a grant alone) | Route adapter and supported-combination registry | THR-011 | Test device/OS/operator/plan/SIM/forwarding matrix; get written provider support. Gate: before architecture freeze. |
| REQ-003 Profile/context | Hypothesis; customer evidence pending | UX-004–UX-005 | Profile API; AssistantProfile/ProfileVersion | THR-005, THR-018 | Schema, version isolation, injection and deletion tests. Gate: internal MVP. |
| REQ-004 Disclosure and bounded conversation | Legal/UX policy pending | UX-002, UX-012 | Realtime worker and policy gateway; ConsentRecord/CallEvent | PRIV-001, PRIV-002, THR-013 | Counsel-approved notice and scripted disclosure, urgency and out-of-scope tests. Gate: real-call pilot. |
| REQ-005 Session lifecycle | Provider unknown | UX-012–UX-013 | Webhook adapter/state machine; CallSession/ProviderLeg/CallEvent | THR-003, THR-004 | Signature, replay, duplicate and out-of-order tests. Gate: internal MVP. |
| REQ-006 Realtime quality/cancellation | No benchmark; AT-004 proposed 500 ms cancellation target, provider validation pending | UX-012 | Media/speech/model adapters | THR-017; NFR-001–003 | Measure latency, interruption, cancellation and failure paths. Gate: before MVP release. |
| REQ-007 Takeover | Route-dependent | UX-013 | Telephony/media adapter and transfer events | THR-011, THR-017 | Controlled success/failure/timeout/repeat tests. Gate: only if advertised; otherwise remove from MVP. |
| REQ-008 Summary/uncertainty | Value and accuracy unvalidated | UX-015 | Summary worker; CallSummary | THR-008, THR-013 | Labelled factuality tests for negation, names, dates, commitments and missing facts. Gate: internal MVP. |
| REQ-009 Usage/cost limits | Quotes pending | UX-018 | Usage API/ledger; UsageEvent/PlanEntitlement | THR-012 | Duplicate event, invoice reconciliation, quota exhaustion and abuse tests. Gate: before paid pilot. |
| REQ-010 Privacy/retention | Counsel/provider review pending | UX-002, UX-019 | Consent/deletion APIs; ConsentRecord/CallerDisclosureEvent/DeletionRequest/DeletionTarget | PRIV-001–005, PRIV-011, PRIV-013 | Approved data flow/notices and deletion tests across first-party/provider systems. Gate: real-call pilot. |
| REQ-011 Isolation | Design only; no tests | UX-014–UX-020 | AuthZ/storage/search/export/tool gateway | THR-001, THR-002, THR-007 | Cross-account negative tests across API, search, export, jobs and callbacks. Gate: internal MVP. |
| REQ-012 Domain connectors | Antena capability audit pending; future scope | Future domain profile | Server allowlist; ConnectorOperation/ToolInvocation; Antena API | THR-006, THR-007 | Tenant, scope, confirmation, idempotency and audit tests. Gate: hospitality profile, not core MVP. |
| REQ-013 History/transcript/audio | Data, cost and retention decisions pending | UX-014–UX-016, UX-019 | Call/summary/media APIs and artifacts | PRIV-003, PRIV-005, THR-008, THR-010 | Access, expiry, consent and deletion tests. Gate: summary/history scope before MVP; transcript/audio only if separately approved. |
| REQ-014 Support/urgent disable | Hypothesis; interviews pending | UX-009–UX-010, UX-021 | Control plane; SupportCase/AuditEvent | THR-011, THR-015, THR-017, PRIV-013–014 | Disable/recovery drill, incident simulation and support access audit. Gate: before pilot. |
| REQ-015 Observability/recovery | SLOs unapproved | UX-010, UX-021–UX-022 | Operations plane and structured events | THR-003, THR-012, THR-017, PRIV-014 | Fault injection, alert/runbook, retry, spend and deletion-backlog tests. Gate: before pilot. |
| REQ-016 Account authentication/recovery | Gap identified from P0 account scope; provider/mechanism unselected | UX-003 | Account/session and recovery API operations; AuthIdentity, AccountSession, RecoveryChallenge, AuditEvent | THR-001, PRIV-006 | Authentication, enumeration, brute-force, recovery abuse, session expiry/revocation and recovery-challenge replay tests. Gate: before internal MVP. |

## Non-functional traceability

| ID | Boundary | Evidence required before approval |
|---|---|---|
| NFR-001 Latency | Media + speech/model path | Approved p50/p95/p99 targets, then measured end-to-end results by route/language. |
| NFR-002 Route success | Route matrix | Owner-approved threshold, controlled repetitions and confidence intervals. |
| NFR-003 Conversation completion | Session/media state machine | Defined completion/failure classes and safe-fallback target. |
| NFR-004 Availability | API/provider dependencies | Approved SLO, maintenance and provider-failure policy. |
| NFR-005 Privacy/deletion | Stores, providers, exports, logs and backups | Per-data-class retention and deletion SLA; counsel review and deletion exercise. |
| NFR-006 Capacity | Sessions, queues, provider limits | Approved concurrency/CPS profile and load/burst/soak evidence. |
| NFR-007 Cost | Usage ledger and provider invoice | Written quotes, invoice reconciliation and approved stress-case margin. |
| NFR-008 Accessibility | Android UI/content | Chosen standard and audit of screen-reader, text scaling, contrast and touch targets. |
| NFR-009 Recovery | Control-plane and route state | Approved RTO/RPO and successful restore/disable drill. |
| NFR-010 Security | Auth, webhooks, tools, storage, secrets | Negative tests, threat review and independent assessment appropriate to exposure. |

## Reference consistency

The matrix assumes these ID ranges exist in current drafts:
- UX-001–UX-022: `UX_SCREEN_INVENTORY.md`
- THR-001–THR-018: `THREAT_MODEL.md`
- PRIV-001–PRIV-014: `PRIVACY_AND_REGULATORY_RISK_REGISTER.md`

This mapping is a manual review, not an automated reference check. Validate all references against the current branch before approval.

## Contract coverage audit

See [REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md](../governance/REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md) for the requirement-by-requirement mapping of proposed API operations, data/state contracts, threat/privacy controls, failure scenarios, verification evidence and remaining blockers. This audit does not approve requirements or authorize implementation.

## Blocking evidence

- Customer interviews and negative evidence.
- Owner-supervised carrier/SIM/device route tests.
- At least two comparable written provider quotes for the exact route.
- Jurisdiction-specific counsel review and provider contract/data terms.
- Owner review of proposed thresholds in `ACCEPTANCE_THRESHOLD_REGISTER.md`; NFR numeric targets and evidence-dependent thresholds remain open.
- Final MVP scope and route-dependent feature list.
- Versioned API/data contracts and operational runbooks.
- Benchmarks, load/security/deletion tests after explicit experiment/implementation approval.
- Named operational/privacy/support owners.
- Explicit owner approval of baseline and implementation start.

Requirement priority is provisional. Completing this matrix does not itself authorise implementation.

## Product-scope to requirement crosswalk

The product-scope catalogue uses SCOPE IDs; this table makes their current relationship to the requirement baseline explicit. A blank requirement mapping is intentional only where the feature is deferred/excluded or remains outside the proposed MVP; it is not evidence of complete coverage.

| Scope ID | Capability | Requirement mapping | Current treatment / gap |
|---|---|---|---|
| SCOPE-001 | Account, authentication and recovery | REQ-016, REQ-011 | P0 candidate; REQ-016 added to close the previously unmapped authentication/recovery gap. |
| SCOPE-002 | Assistant profile setup | REQ-003 | P0 candidate. |
| SCOPE-003 | Personal context form | REQ-003 | P0 candidate. |
| SCOPE-004 | Routing/forwarding onboarding and verification | REQ-001, REQ-002 | P0 candidate; blocked by route evidence. |
| SCOPE-005 | Live call handling | REQ-004, REQ-005, REQ-006 | P0 candidate; blocked by route/provider/legal evidence. |
| SCOPE-006 | Caller disclosure and safe response policy | REQ-004, REQ-010 | P0 candidate; jurisdictional policy review required. |
| SCOPE-007 | User takeover / transfer or end-call control | REQ-007 | Conditional; remove from MVP promise if route cannot support it. |
| SCOPE-008 | Post-call summary and intent | REQ-008 | P0 candidate; factuality evaluation required. |
| SCOPE-009 | Call history and search | REQ-013 | P1 candidate; may be narrowed to summaries/metadata. |
| SCOPE-010 | Full transcript/audio playback | REQ-013, REQ-010 | Off unless separately approved; retention/legal/provider gates apply. |
| SCOPE-011 | Follow-up reminders/tasks | — | P1 candidate, not fully specified by current REQs; defer or create a requirement before inclusion. User confirmation required. |
| SCOPE-012 | Caller/contact allowlist and denylist | — | Conditional/P1; not directly covered by current REQs. Defer or create a dedicated requirement before inclusion; contact-book handling and rule semantics need definition. |
| SCOPE-013 | Usage meter and plan limits | REQ-009 | P0 candidate. |
| SCOPE-014 | Data export, deletion and retention settings | REQ-010, REQ-013 | P0 privacy foundation, subject to data-class/provider lifecycle decisions. |
| SCOPE-015 | Abuse report and support | REQ-014, REQ-015 | P0 candidate. |
| SCOPE-016 | Multi-language and code-switching | REQ-006 | P1 candidate; supported languages require end-to-end evidence. |
| SCOPE-017 | Voice cloning / imitation | — | Excluded from initial scope; no requirement should be added unless scope is separately reopened. |
| SCOPE-018 | Assistant-initiated outbound calls | — | Deferred; requires separate legal/provider and abuse analysis before a requirement is drafted. |
| SCOPE-019 | Domain profiles and connectors | REQ-012 | Deferred after core validation. |
| SCOPE-020 | Hospitality profile using Antena APIs | REQ-012 | Future expansion; Antena capability audit required. |
| SCOPE-021 | Advocate/legal profile | — | Deferred; separate discovery and professional/legal review required. |

This crosswalk is a draft consistency aid. The mapped requirements do not approve the corresponding features. The explicit gaps for SCOPE-011 and SCOPE-012 must be resolved by either deferring those features or drafting and reviewing dedicated requirements before baseline approval.


## UX inventory coverage clarification

- **UX-006 (assistant permissions / system role)** is conditionally traced to REQ-001/REQ-002. It must only be presented when required by the selected platform/route; a permission grant is not proof that call routing is supported or verified.
- **UX-022 (notifications and permission status)** is traced to REQ-001/REQ-015 for truthful status, stale-state handling and notification failure. Notifications are not authoritative route-state evidence, and private lock-screen content must remain minimised.
- **UX-011 (caller handling preferences/contact access)** and **UX-017 (follow-up tasks)** remain conditional and unmapped to dedicated functional requirements. Keep them deferred or create/review explicit requirements before MVP inclusion, consistent with the scope crosswalk.
