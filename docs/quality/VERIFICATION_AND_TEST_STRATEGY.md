# Verification and Test Strategy — Draft

**Status:** Planning document only. No implementation or tests have been started. Date: 2026-10-11.

## 1. Objectives

Verify not only model output but the entire call experience: route setup, media, conversation, user control, privacy, billing, deletion and recovery. Test the supported carrier/device/plan matrix and fail safely outside it.

## 2. Test layers

### Product and policy tests
- Profile schema validation and versioning.
- Policy precedence and prompt-injection resistance.
- Caller disclosure, refusal/escalation and uncertainty behaviour.
- Summary factuality, negation, names, dates, numbers and explicit uncertainty.
- Tool permission boundaries and confirmation requirements.

### API and state-machine tests
- Authentication and object-level authorization.
- Routing state transitions and deactivation.
- Signed webhook validation, replay protection, duplicate/out-of-order events.
- Idempotent usage ledger, reconciliation and plan exhaustion.
- Profile changes during active sessions.
- Export/deletion lifecycle and provider deletion exceptions.

### Realtime voice tests
- Connection setup and time-to-first-audio.
- Turn-taking, interruption/barge-in, silence and DTMF where applicable.
- STT/TTS/model timeouts, cancellation and provider outage.
- Noisy audio, varied accents, supported languages and code-switching.
- Long calls, concurrent calls, disconnect/reconnect and transfer/takeover.
- No-audio, one-way audio, caller ID missing and wrong-route cases.

### Security/privacy tests
- Cross-tenant access to calls, summaries, exports and tools.
- Webhook forgery/replay and malicious input.
- Prompt injection via caller speech/profile context.
- Secret leakage, excessive logging and support-role abuse.
- Deletion from primary data, object storage, search, caches and provider systems.
- Rate-limit, spend-limit, duration-limit and resource exhaustion tests.

### UX and accessibility tests
- First-time setup with an unsupported operator/plan.
- Denied permissions, stale route status and failed test call.
- Emergency disable and restore normal calling.
- User understanding of AI disclosure, recording, retention and minute limits.
- Screen reader, dynamic text, contrast, touch target and offline states.

### Performance and resilience
- Load, burst, soak, failover and recovery tests.
- Provider quota exhaustion and rate limiting.
- Queue saturation, worker restart and out-of-order event replay.
- Database/storage bottlenecks and deletion backlog.
- Cost under low/base/high traffic and abusive usage.

## 3. Test data and privacy

- Use synthetic test audio and fictional profiles before any real-call experiment.
- Never use private customer call recordings in development or tests without a separately reviewed legal basis and explicit safeguards.
- Maintain a labelled evaluation set with consent and documented provenance if real speech is eventually required.
- Redact phone numbers and personal data from fixtures, logs and bug reports.
- Define retention/deletion for all test artifacts.

## 4. Metrics to define

- Routing setup and test-call success by carrier/device/plan.
- Connection failure and unexpected termination rates.
- p50/p95/p99 end-to-end time to first response audio.
- Interruption response latency and successful takeover rate.
- STT quality and summary factuality on an agreed labelled set.
- Harmful/misleading response rate and policy-violation rate.
- Usage reconciliation discrepancy and duplicate billing event count.
- Data deletion completion time and residual-artifact rate.
- Cost per connected minute and per active user.
- Support contacts per 100 active users.

Thresholds are intentionally not invented here. Agree them before testing so success criteria cannot be moved after seeing results.

## 5. Release gates

### Gate A — Feasibility experiment
Owner approval, controlled test plan, test participants/data consent, route eligibility, privacy safeguards and stop conditions.

### Gate B — Internal MVP
All P0 acceptance criteria pass; critical security/privacy findings resolved; cost and latency measured; runbooks and rollback/deactivation verified.

### Gate C — Private pilot
Counsel review for chosen jurisdiction, clear user/caller notices, support coverage, monitoring, spend caps, incident response and explicit pilot approval.

### Gate D — Public release
Reliability and retention evidence; load test to approved peak target; provider contracts reviewed; billing/support ready; store policy review; privacy/deletion flows verified; owner go/no-go approval.

## 6. TDD workflow after implementation is authorised

For each requirement:
1. Write/approve acceptance criteria and failure cases.
2. Add failing unit/contract/integration tests.
3. Implement the smallest change.
4. Run targeted and regression tests.
5. Add security, observability and operational evidence.
6. Update requirement traceability and handover.
7. Obtain review before merge.

No implementation work is authorised by this test strategy.

## 7. Verification artifact and evidence contract

Use [Deletion and Verification Reconciliation](../governance/DELETION_AND_VERIFICATION_RECONCILIATION.md) as the draft crosswalk from requirements and threshold IDs to planned evidence artifacts. It covers deletion targets, cross-account isolation, deletion-backlog/restore recovery, usage reconciliation, route disable/recovery, latency/cancellation, summary factuality and authentication/recovery.

A planned artifact or test layer is not proof of execution. Each future report should record requirement/threshold IDs, approved scope and configuration, test-plan/version, environment and provider versions, inputs, expected and observed outcomes, timestamps, evidence location, reviewer, failures and disposition. Preserve negative/partial outcomes; do not silently mark unknown or blocked cases as passed.

The acceptance threshold register remains the canonical source for threshold values/status. All existing thresholds remain proposed or open until the owner approves them. No tests or experiments are claimed completed by this section.


## Planned acceptance-test catalogue

`PLANNED_ACCEPTANCE_TEST_CATALOG.md` provides proposed scenario IDs for REQ-001–REQ-016, NFR-001–NFR-010 and cross-cutting failure/abuse cases. All scenarios are planning-only and NOT RUN. Use it with `ACCEPTANCE_CRITERIA_TESTABILITY_AUDIT.md` and `ACCEPTANCE_THRESHOLD_REGISTER.md`; do not record a pass until scope, provider/route/policy dependencies, test setup, threshold, denominator, evidence and reviewer are approved. The catalogue does not authorize implementation or external experiments.
