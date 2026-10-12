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

## 5. Verification artifact crosswalk

These artifacts are future work. Their names identify planned evidence, not tests already run.

| Requirement / threshold | Planned verification artifact | Pass evidence needed | Current state |
|---|---|---|---|
| REQ-010, REQ-013, NFR-005, AT-008 | `deletion-target-matrix.md` or equivalent versioned fixture; end-to-end deletion exercise report | Each in-scope data class mapped to present/non-present targets; per-target result; retries/partial failure; provider and backup evidence; policy-approved exceptions | NOT RUN; AT-008 OPEN |
| REQ-011, AT-006 | Cross-account authorization test report for request creation/status, exports, jobs and callbacks | No unauthorized cross-account read/write/status disclosure in defined test set | NOT RUN; threshold PROPOSED |
| REQ-015, NFR-009, AT-009 | Deletion-backlog alert/runbook exercise and backup/restore drill | Named owner, detection, escalation, safe retry, recovery evidence and approved RTO/RPO | NOT RUN; AT-009 OPEN |
| REQ-009, AT-005 | Duplicate/out-of-order usage event and provider invoice reconciliation report | No duplicate ledger charge in the defined replay set; discrepancies linked to immutable adjustments and reconciled against provider evidence | NOT RUN; threshold PROPOSED |
| REQ-001, REQ-014, AT-001 | Disable/recovery usability walkthrough and controlled route recovery report | Approved supported-route scope; timestamped state transitions; restoration independently verified; failure paths exercised | NOT RUN; AT-001 PROPOSED; route evidence BLOCKED |
| REQ-006, AT-003/AT-004 | Timestamped end-to-end latency/cancellation benchmark by route and provider | Defined clocks and sample conditions; p50/p95/p99; provider cancellation semantics; results compared only with pre-approved threshold | NOT RUN; AT-003 OPEN, AT-004 PROPOSED |
| REQ-008, AT-012 | Versioned labelled summary-evaluation set, rubric and evaluation report | Provenance/consent for data; explicit factuality and uncertainty scoring; predeclared acceptance decision | NOT RUN; AT-012 OPEN |
| REQ-016 | Authentication/recovery abuse and session-revocation test report | Enumeration, brute force, replay, expiry and revoked-session cases covered with recorded results | NOT RUN; mechanism unselected |

Do not use a generic “test passed” checkbox without a versioned test plan, scope/configuration, input set, expected outcome, observed outcome, timestamp, environment/provider version, evidence location, reviewer and disposition of failures.

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
