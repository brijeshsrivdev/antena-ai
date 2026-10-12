# Expanded Requirements Traceability — Working Draft

**Status:** DRAFT; not approved. No implementation authorised.  
**Draft ID set:** REQ-001–REQ-015 and NFR-001–NFR-010 are stable identifiers within the current working draft and are defined in `CORE_REQUIREMENTS_DRAFT.md`. They are not yet approved baseline requirements. Priority labels remain candidates. Candidate thresholds and unresolved target decisions are tracked in `ACCEPTANCE_THRESHOLD_REGISTER.md`; none is owner-approved.

## Functional traceability

| ID | Evidence state | UX | Architecture / data | Risks | Verification and exit gate |
|---|---|---|---|---|---|
| REQ-001 Activation and routing state | Route unproven; interviews pending; AT-001 proposed 2-action disable target | UX-007–UX-010 | Routing API/state machine; RoutingConfig | THR-011, PRIV-013 | Test state transitions and disable/recovery. Gate: before live pilot. |
| REQ-002 Route eligibility | Android desk review; controlled experiment required | UX-007–UX-009 | Route adapter and supported-combination registry | THR-011 | Test device/OS/operator/plan/SIM/forwarding matrix; get written provider support. Gate: before architecture freeze. |
| REQ-003 Profile/context | Hypothesis; customer evidence pending | UX-004–UX-005 | Profile API; AssistantProfile/ProfileVersion | THR-005, THR-018 | Schema, version isolation, injection and deletion tests. Gate: internal MVP. |
| REQ-004 Disclosure and bounded conversation | Legal/UX policy pending | UX-002, UX-012 | Realtime worker and policy gateway; ConsentRecord/CallEvent | PRIV-001, PRIV-002, THR-013 | Counsel-approved notice and scripted disclosure, urgency and out-of-scope tests. Gate: real-call pilot. |
| REQ-005 Session lifecycle | Provider unknown | UX-012–UX-013 | Webhook adapter/state machine; CallSession/CallEvent | THR-003, THR-004 | Signature, replay, duplicate and out-of-order tests. Gate: internal MVP. |
| REQ-006 Realtime quality/cancellation | No benchmark; AT-004 proposed 500 ms cancellation target, provider validation pending | UX-012 | Media/speech/model adapters | THR-017; NFR-001–003 | Measure latency, interruption, cancellation and failure paths. Gate: before MVP release. |
| REQ-007 Takeover | Route-dependent | UX-013 | Telephony/media adapter and transfer events | THR-011, THR-017 | Controlled success/failure/timeout/repeat tests. Gate: only if advertised; otherwise remove from MVP. |
| REQ-008 Summary/uncertainty | Value and accuracy unvalidated | UX-015 | Summary worker; CallSummary | THR-008, THR-013 | Labelled factuality tests for negation, names, dates, commitments and missing facts. Gate: internal MVP. |
| REQ-009 Usage/cost limits | Quotes pending | UX-018 | Usage API/ledger; UsageEvent/PlanEntitlement | THR-012 | Duplicate event, invoice reconciliation, quota exhaustion and abuse tests. Gate: before paid pilot. |
| REQ-010 Privacy/retention | Counsel/provider review pending | UX-002, UX-019 | Consent/deletion APIs; ConsentRecord/DeletionRequest | PRIV-001–005, PRIV-011, PRIV-013 | Approved data flow/notices and deletion tests across first-party/provider systems. Gate: real-call pilot. |
| REQ-011 Isolation | Design only; no tests | UX-014–UX-020 | AuthZ/storage/search/export/tool gateway | THR-001, THR-002, THR-007 | Cross-account negative tests across API, search, export, jobs and callbacks. Gate: internal MVP. |
| REQ-012 Domain connectors | Antena capability audit pending; future scope | Future domain profile | Server allowlist; ConnectorOperation/ToolInvocation; Antena API | THR-006, THR-007 | Tenant, scope, confirmation, idempotency and audit tests. Gate: hospitality profile, not core MVP. |
| REQ-013 History/transcript/audio | Data, cost and retention decisions pending | UX-014–UX-016, UX-019 | Call/summary/media APIs and artifacts | PRIV-003, PRIV-005, THR-008, THR-010 | Access, expiry, consent and deletion tests. Gate: summary/history scope before MVP; transcript/audio only if separately approved. |
| REQ-014 Support/urgent disable | Hypothesis; interviews pending | UX-009–UX-010, UX-021 | Control plane; SupportCase/AuditEvent | THR-011, THR-015, THR-017, PRIV-013–014 | Disable/recovery drill, incident simulation and support access audit. Gate: before pilot. |
| REQ-015 Observability/recovery | SLOs unapproved | UX-010, UX-021 | Operations plane and structured events | THR-003, THR-012, THR-017, PRIV-014 | Fault injection, alert/runbook, retry, spend and deletion-backlog tests. Gate: before pilot. |

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
