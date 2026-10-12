# Acceptance Threshold Register — Draft

**Status:** DRAFT / owner decision required. This register proposes measurable starting points for review; it does not approve a threshold, establish product capability, or authorise implementation.

## Rules

- Keep a threshold marked **PROPOSED** until the owner explicitly approves it.
- Do not run a pass/fail experiment against a threshold that was selected after seeing its results.
- Route, jurisdiction, provider, device and language scope must be written beside each result.
- Safety, privacy and unauthorised-action failures are not traded off against average quality scores.
- Replace every proposed value with an approved value or an explicit “not applicable” rationale before baseline approval.

## Candidate thresholds for owner review

| ID | Area | Proposed starting point | Evidence needed | Status |
|---|---|---|---|---|
| AT-001 | Disable access | Reach disable instructions within 2 user actions from primary dashboard | Usability walkthrough; confirm emergency path | PROPOSED |
| AT-002 | Route verification | 30 controlled repetitions per supported configuration; target at least 95% successful expected routing | Owner-supervised tests; report numerator/denominator and confidence interval | PROPOSED; exploratory only |
| AT-003 | End-to-end latency | Establish p50/p95/p99 baseline first; do not set a release threshold before route/provider benchmark | Timestamped end-to-end measurements under low/base/peak load | OPEN — no numeric target |
| AT-004 | Cancellation | Stop downstream generation and playback within 500 ms of accepted cancellation, where provider/media architecture allows measurement | Instrumented cancellation test; validate provider semantics | PROPOSED |
| AT-005 | Duplicate billing | Zero duplicate ledger charges for duplicate/replayed provider events | Automated idempotency and reconciliation tests | PROPOSED |
| AT-006 | Cross-tenant isolation | Zero unauthorised cross-tenant reads, writes, exports or tool actions | Negative security tests across APIs, jobs, callbacks, search and exports | PROPOSED; zero-tolerance gate |
| AT-007 | Unauthorised actions | Zero actions outside server-side allowlist, scope or confirmation policy | Adversarial tool/prompt-injection evaluation | PROPOSED; zero-tolerance gate |
| AT-008 | Deletion | No numeric SLA until provider, backup and legal constraints are mapped; define per-data-class SLA before pilot | Deletion exercise across first-party stores and provider systems | OPEN |
| AT-009 | Availability and recovery | No numeric SLO/RTO/RPO until operating model and dependency contracts are known | Provider SLA review, restore drill, failure-mode analysis | OPEN |
| AT-010 | Capacity | Validate the proposed 10x peak multiplier; do not treat it as measured demand | Load/burst/soak tests and real usage evidence | OPEN |
| AT-011 | Spend limits | Hard server-side per-account and global caps must exist before any real-call pilot; amounts require owner approval | Simulated exhaustion and provider billing reconciliation | PROPOSED control; amounts OPEN |
| AT-012 | Summary quality | Define labelled evaluation set and acceptance rubric before comparing models; no numeric accuracy claim yet | Synthetic/consented corpus, factuality and uncertainty review | OPEN |

## Unresolved placeholders in core requirements

- REQ-001: dashboard actions to reach disable/recovery.
- REQ-006: cancellation latency and end-to-end latency targets.
- NFR-001–NFR-010: latency, routing, completion, availability, privacy/deletion, capacity, cost, accessibility, recovery and security targets.
- Retention/deletion values depend on data category, jurisdiction, provider contracts and legal review.

These placeholders must not be silently treated as zero, unlimited, or implicitly approved. Where a safe and measurable threshold cannot yet be set, record the missing evidence and block the relevant release gate.

## Decision procedure

1. Gather the required evidence for each threshold.
2. Review safety and privacy constraints before performance or cost trade-offs.
3. Record the owner decision and rationale in DECISION_LOG.md.
4. Update the canonical requirement and traceability matrix consistently.
5. Keep release blocked where a P0 requirement or legal/privacy control remains unresolved.

## Related documents

- docs/requirements/CORE_REQUIREMENTS_DRAFT.md
- docs/requirements/TRACEABILITY_MATRIX.md
- docs/quality/VERIFICATION_AND_TEST_STRATEGY.md
- docs/quality/VOICE_AGENT_EVALUATION_PLAN.md
- docs/research/TELEPHONY_VALIDATION_PROTOCOL.md
- docs/governance/BASELINE_CONSISTENCY_AUDIT.md
- docs/governance/DELETION_AND_VERIFICATION_RECONCILIATION.md — planned verification artifacts and deletion-target evidence mapping
