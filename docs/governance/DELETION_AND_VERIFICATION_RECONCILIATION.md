# Deletion and Verification Reconciliation

**Status:** Desk-only consistency proposal; not owner-approved, not a retention policy, and not evidence of implemented or tested controls. Date: 2026-10-12.

## 1. Finding

The data inventory describes deletion across primary storage, object storage, indexes, caches, analytics, provider systems and backups. The conceptual model now separates a parent `DeletionRequest` from per-destination `DeletionTarget` records. The remaining gap is an explicit shared mapping from each data class to applicable destinations, accountable operational roles, target outcomes and verification evidence.

This document closes that documentation gap only. It does not set retention periods, deletion SLAs, legal exceptions, backup expiry, provider capabilities, or named operational owners.

## 2. Data-class to deletion-target map

| Data class | Candidate targets to discover and track | Minimum verification evidence | Open decision / guardrail |
|---|---|---|---|
| Account identifiers and authentication identity | Primary account/auth store; identity provider where applicable; caches/search; backups | Account deletion exercise; auth/session revocation; residual lookup check; backup policy evidence | Determine which minimal security/accounting records may need restricted retention after deletion, with qualified review. |
| Sessions and recovery challenges | Primary session/recovery store; caches; audit/security records; backups | Revoke active sessions; replay/expiry checks; verify challenge secrets are not retained in readable form | Define minimal security-event retention separately from active credential/session deletion. |
| Assistant profile and profile versions | Primary profile store; search/index/cache; model/provider copies only if sent or persisted; backups | Verify active and historical versions are inaccessible/deleted per policy; confirm downstream data-flow inventory | Minimise model context; do not assume a provider retained a copy unless the data flow shows it. |
| Routing configuration and route evidence | Primary routing store; operational cache; relevant support/audit records; backups | Remove or disable account-bound configuration; confirm secret revocation where relevant; preserve only approved evidence | Separate deletion of account-linked data from shared route-support evidence that contains no personal data. |
| Call metadata, events and provider legs | Primary call/event store; search/analytics; caches; provider control-plane records if retained; backups | Query by internal session ID and provider references; prove access is blocked and applicable target outcomes recorded | Keep minimal audit/usage evidence only where approved; provider event availability and deletion support are unknown. |
| Live audio/media, recording and transcript | Object/media storage; derived transcript/index; processing queues; caches; speech/model provider systems; backups | Verify object removal or policy-defined expiry; check derivatives and queues; obtain provider deletion result or record an approved exception | Recording/transcript remain optional and off by default pending review; do not claim immediate physical backup erasure. |
| Summary and extracted intent | Primary summary store; search/index/cache; exports; downstream provider copies if any; backups | Confirm summary and indexed/exported copies follow the request scope; verify access and correction/deletion behavior | A summary is a separate artifact from source audio/transcript; deletion of one must not imply deletion of all. |
| Tasks/reminders and contact mappings | Task/reminder store; scheduled-job queue; notification payloads; contact index/cache; backups | Confirm pending jobs are cancelled or safely neutralised; verify no later notification/action is emitted | SCOPE-011/SCOPE-012 remain deferred or need separate requirements; consequential actions require user confirmation. |
| Usage and billing ledger | Usage store; billing/payment provider records; invoice/export records; backups | Reconcile immutable original and adjustment events; confirm account-visible access is removed as approved; record provider/financial exception | Never destructively rewrite the ledger to simulate deletion. Retention and permitted minimisation require qualified review. |
| Consent and caller-disclosure records | Consent/notice store; linked audit records; relevant provider records if applicable; backups | Verify request/withdrawal state and exact notice version/event evidence; confirm policy-defined treatment | Account-holder choice, caller disclosure and legal consent are distinct. Do not delete or retain indiscriminately without approved policy. |
| Security/audit events and support records | Audit/support stores; search/analytics; attachments; backups | Access review, redaction and policy check; verify approved minimisation or exception | Content-free, bounded audit data is preferred; legal/security hold treatment remains open. |
| Operational telemetry | Metrics/logging/tracing; analytics exports; vendor observability systems; backups | Search for account/session identifiers; verify redaction, aggregation or target removal per policy | Avoid caller numbers and raw content in labels. Aggregated data may have different treatment only under an approved policy. |
| Domain connector data (future) | Transient worker/cache; connector/provider logs; task/result store; backups | Verify only approved minimum fields were persisted and transient caches expire; audit connector scopes | Future Antena data must use trusted APIs; do not create a shadow domain database. |

The map is a discovery checklist, not a claim that every target exists. For each selected provider and deployed component, the data-flow inventory must mark each target **present**, **not present with evidence**, or **unknown**. Unknown targets block a full-deletion claim.

## 3. Candidate request and target semantics

Keep the parent workflow separate from individual destination results.

- **Request:** `requested` → `in_progress` → `completed` only when every required target is confirmed deleted or covered by an explicitly approved policy outcome; otherwise remain pending or use `completed_with_exception` only after required review.
- **Target:** candidate outcomes are `pending`, `in_progress`, `deleted_confirmed`, `retryable_failure`, `not_applicable_approved`, and `exception_review_required`. These are proposals for contract review, not approved enum values.
- A transient provider failure, unknown target, missing backup policy or unreviewed legal hold must not be silently counted as success.
- Every exception should have a safe reason code, accountable role, review/expiry date where applicable, and a user-visible explanation that does not disclose security-sensitive internals.
- Repeated requests must be idempotent. Retries must not resurrect deleted data or repeat unrelated external actions.
- Deletion status is account-authorized. Do not reveal provider identifiers, other users' artifacts, raw content, secrets or internal infrastructure.
- “Primary data removed”, “provider confirmed”, “backup expired by policy”, and “completed with reviewed exception” are distinct evidence statements.

No retention duration or deadline is inferred by this state model. Define policy by data class and destination after provider terms, applicable obligations and recovery architecture are reviewed.

## 4. Operational responsibility model

Named people/teams and on-call coverage are not established. Assign these roles before a pilot; one person may hold multiple roles only if conflicts and backup coverage are documented.

| Responsibility | Accountable role to name | Required action / escalation trigger |
|---|---|---|
| Request orchestration | Product/backend operations owner | Monitor request age, retry backlog and stuck targets; prevent false completion. |
| First-party stores and indexes | Data/platform owner | Execute and verify deletion in each owned store; report inaccessible or inconsistent targets. |
| Provider-side copies | Provider/integration owner | Confirm documented deletion API/terms, submit supported requests, retain safe result evidence, escalate unknown outcomes. |
| Backups and restore behavior | Infrastructure/DR owner | Document expiry and restore controls; ensure deleted data is not silently reintroduced after restore. |
| Exception approval | Privacy/legal decision owner, with qualified counsel where needed | Decide permissible retention/exception scope, user communication and expiry; engineering must not self-approve legal exceptions. |
| Security incident or unauthorized access | Security/incident owner | Escalate exposed content, unauthorized deletion/status access, or suspected data reappearance. |
| User communication and support | Support owner | Explain pending/partial/completed states and provide a correction/escalation path without overclaiming. |

## 5. Requirement, threshold and verification artifact crosswalk

The following are proposed future artifacts and coverage pointers, not evidence that tests have been designed in full or executed. Requirement priorities/statuses remain draft. “NOT RUN” means no result is claimed in this discovery repository.

| Requirement / threshold | Planned verification artifact | Minimum evidence needed | Current state |
|---|---|---|---|
| REQ-001; AT-001 | Activation/disable usability walkthrough; route state-transition and recovery report | Action path, configuration/version, timestamps, authoritative state, disable and restoration outcomes | NOT RUN; AT-001 PROPOSED; route evidence blocked |
| REQ-002; AT-002 | Versioned supported-route matrix and controlled route test report | Device/OS/operator/plan/SIM/forwarding configuration, expected vs observed routing, numerator/denominator, confidence interval, written provider eligibility | NOT RUN; AT-002 PROPOSED/exploratory |
| REQ-003 | Profile schema/version and context-isolation test report | Validation failures, immutable published version, active-call version behavior, prompt-injection boundary and profile deletion | NOT RUN; customer value and profile policy open |
| REQ-004 | Disclosure policy review record and scripted disclosure/safe-escalation test report | Route-specific notice delivery/one-way audio/failure behavior, jurisdiction-specific qualified review, urgency and out-of-scope cases | NOT RUN; blocked by route and legal/product review |
| REQ-005 | Provider callback contract suite and call-session/provider-leg reconciliation report | Signature/replay verification, duplicate/out-of-order events, provider-account/session mapping, terminal-state precedence and late events | NOT RUN; provider contract unselected |
| REQ-006; AT-003, AT-004 | Timestamped end-to-end latency and cancellation benchmark | Clock semantics, route/provider/language/load, p50/p95/p99, accepted-cancel to stopped generation/playback; compare only against pre-approved threshold | NOT RUN; AT-003 OPEN, AT-004 PROPOSED |
| REQ-007 | Takeover/transfer route-specific success/failure/timeout report | Supported-route evidence, duplicate request handling, unknown/late outcome reconciliation, verified user-visible result | NOT RUN; conditional on route support |
| REQ-008; AT-012 | Versioned labelled summary-evaluation set, rubric and evaluation report | Provenance/consent, negation/names/dates/commitments/missing facts, uncertainty scoring, predeclared acceptance decision | NOT RUN; AT-012 OPEN |
| REQ-009; AT-005, AT-011 | Usage idempotency/replay suite, quota-exhaustion simulation and provider invoice reconciliation report | Duplicate/replay cases, immutable adjustments, provider billable units/rounding/multiple legs, hard account/global cap and stop conditions | NOT RUN; AT-005 PROPOSED; AT-011 control PROPOSED, amounts OPEN; quotes pending |
| REQ-010; REQ-013; NFR-005; AT-008 | Data-class/deletion-target matrix and end-to-end deletion exercise report | In-scope destinations marked present/not present with evidence; per-target outcomes; retries/partial failure; provider and backup evidence; approved exceptions | NOT RUN; AT-008 OPEN; privacy/provider policy blocked |
| REQ-011; AT-006 | Cross-account authorization report covering APIs, search, exports, jobs, callbacks and tool gateway | Defined negative test set with zero unauthorized reads/writes/status disclosures/actions; include revoked-session and object-reference cases | NOT RUN; AT-006 PROPOSED zero-tolerance gate |
| REQ-012 | Connector capability/scope contract suite and adversarial authorization report | Server allowlist, tenant/account scope, schema validation, confirmation/idempotency, audit and denied arbitrary URL/SQL/tool attempts | NOT RUN; future hospitality scope; Antena capability audit pending |
| REQ-013 | History/summary/media authorization, expiry and deletion report | Distinguish metadata, summary, transcript and audio; expired/revoked access; optional media disabled unless separately approved | NOT RUN; P1 candidate; transcript/audio feature-gated |
| REQ-014; AT-001 | Disable/recovery drill, support access audit and incident tabletop | Independent recovery path, named escalation owner, timestamps, support least privilege, verified restoration and stop conditions | NOT RUN; ownership/runbooks open |
| REQ-015; AT-009, AT-010, AT-011 | Monitoring/runbook exercise, deletion-backlog alert test, restore drill and load/burst/soak report | Alert ownership, queue recovery, approved RTO/RPO, measured peak profile, spend-cap enforcement and provider outage behavior | NOT RUN; AT-009 OPEN, AT-010 OPEN, AT-011 amounts OPEN |
| REQ-016 | Authentication/recovery abuse and session-revocation report | Enumeration, brute force, expiry, replay, recovery abuse, session expiry/revocation and authorization after revocation | NOT RUN; authentication mechanism unselected |
| NFR-001 | End-to-end latency benchmark by route/provider/language/load | Approved p95/p99 targets before confirmatory test; timestamped sample distributions | NOT RUN; target OPEN under AT-003 |
| NFR-002 | Route reliability matrix report | Approved per-configuration threshold, controlled repetitions and confidence interval | NOT RUN; threshold OPEN/proposed under AT-002 |
| NFR-003 | Conversation completion/failure classification report | Predefined completion, safe fallback, disconnect, cancellation and one-way-audio categories; denominator and observed rates | NOT RUN; target OPEN |
| NFR-004 | Availability/incident measurement and dependency review | Approved SLO, maintenance policy, dependency scope and representative observation period | NOT RUN; target OPEN under AT-009 |
| NFR-005 | Data-class retention/deletion evidence pack | Approved per-class schedule/SLA, first-party/provider deletion exercise, backup policy and reviewed exceptions | NOT RUN; AT-008 OPEN |
| NFR-006 | Load, burst, soak and provider-quota report | Approved concurrency/CPS profile, workload mix, bottleneck and failure behavior; validate rather than assume the 10x multiplier | NOT RUN; target open under AT-010 |
| NFR-007 | Cost and invoice reconciliation report | Comparable written route-specific quotes, measured billable units, invoice reconciliation and approved margin/stress case | NOT RUN; provider quotes and approved cost target missing |
| NFR-008 | Accessibility audit and assistive-technology walkthrough | Chosen standard, screen reader, dynamic text, contrast, touch targets and error/fallback flows | NOT RUN; standard/target open |
| NFR-009 | Backup/restore and incident recovery exercise | Owner-approved RTO/RPO, restore evidence, deletion non-resurrection check and route/control-plane recovery | NOT RUN; target open under AT-009 |
| NFR-010; AT-006, AT-007 | Threat-control test report and independent review appropriate to exposure | AuthZ, webhook replay, secrets/logging, tool allowlist, prompt injection and zero-tolerance action/isolation cases | NOT RUN; thresholds proposed; review scope open |

### Acceptance-threshold status control

- **PROPOSED** means a candidate value/control awaits explicit owner approval; it is not a release gate yet.
- **OPEN** means no numeric target has been set or the necessary evidence is missing. Do not invent a value or treat it as zero/unlimited.
- **NOT RUN** means no experiment, benchmark, deletion exercise, load test, security test or pilot result is claimed.
- AT-001, AT-002, AT-004, AT-005, AT-006, AT-007 and the control aspect of AT-011 remain proposed; AT-003, AT-008, AT-009, AT-010 and AT-012 remain open. AT-011 spend amounts remain open. Any status change must be made in the canonical acceptance threshold register and supported by an owner decision or evidence, not only in this crosswalk.

For each executed report, capture requirement/threshold IDs, approved scope/configuration, test-plan version, environment and provider versions, inputs, expected and observed outcomes, timestamps, evidence location, reviewer, failures and disposition. A generic “passed” checkbox without reproducible evidence is insufficient.

## 6. Reconciliation rules

1. The threshold register is the source of truth for numeric candidate thresholds and their status. Do not introduce competing numeric gates in this document.
2. The traceability matrix and requirement-contract coverage audit remain the requirement index; this document adds verification detail but does not make requirements approved.
3. A prepared plan is not test evidence. A proposed threshold is not owner approval. A provider feature claim is not route-specific proof.
4. An acceptance criterion without a named future evidence artifact, scope and expected result is not verification-ready; mark the gap rather than assuming coverage.
5. A failed, partial or unknown result remains visible in the report and blocks the relevant gate until resolved or explicitly accepted by the owner with rationale and limits.

## 7. Decisions still required

- Confirm data classes, in-scope stores, providers and derived copies after the architecture/provider shortlist is selected.
- Approve per-class retention, backup expiry, deletion deadlines, user-visible semantics and exception rules after qualified review.
- Name accountable operational, provider, infrastructure, privacy/legal, security and support roles.
- Review the proposed target outcomes and test artifact names before converting them into schemas or automation.
- Approve numeric thresholds or document non-applicability in the canonical threshold register before experiments.
- Authorize any interviews, route tests, provider outreach, spending or other external activity separately. This document authorizes none.

## Related documents

- [Data inventory and lifecycle](../security/DATA_INVENTORY_AND_LIFECYCLE.md)
- [Data model draft](../architecture/DATA_MODEL_DRAFT.md)
- [State and event contracts](../architecture/STATE_AND_EVENT_CONTRACTS_DRAFT.md)
- [API contract draft](../architecture/API_CONTRACT_DRAFT.md)
- [Requirement-to-contract coverage audit](REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md)
- [Verification and test strategy](../quality/VERIFICATION_AND_TEST_STRATEGY.md)
- [Acceptance threshold register](../requirements/ACCEPTANCE_THRESHOLD_REGISTER.md)
- [Phase 0 exit criteria and evidence map](PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md)
