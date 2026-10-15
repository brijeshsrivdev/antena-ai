# Data Model Draft — AI Voice Platform

**Status:** Conceptual data model, not a migration/schema. No implementation authorised.

## 1. Modelling principles

- Treat user/account ownership and tenant scope as explicit relationships.
- Keep the authoritative domain data in the domain system; AI stores references and minimum results, not a shadow copy of the full domain database.
- Version profiles and policies so each call can be traced to the configuration used.
- Separate call metadata, summary, transcript, audio, usage, consent and audit records because their access and retention needs differ.
- Do not put raw phone numbers or transcript content in generic metrics labels.
- Define deletion cascades and provider/backup lifecycle before selecting storage.
- Use internal IDs rather than exposing sequential IDs; still enforce authorization independently of identifier unpredictability.

## 2. Candidate entities

| Entity | Purpose | Candidate fields | Main relationships / constraints |
|---|---|---|---|
| Account | User/account lifecycle | id, status, created_at, region, deletion_state | Owns profiles, calls, usage and privacy requests. |
| AuthIdentity | Link to identity provider | id, account_id, provider, subject, created_at | Unique provider+subject; avoid storing credentials when delegated auth is used. |
| AccountSession | Track authenticated sessions/devices | id, account_id, auth_identity_id, created_at, last_seen_at, expires_at, revoked_at, device_label, risk_state | Server-revocable; avoid collecting unnecessary device fingerprints; token material is not stored in readable form. |
| RecoveryChallenge | Track an in-progress account recovery | id, account_id, recovery_method, challenge_digest, created_at, expires_at, consumed_at, attempt_count, state | Single-use, short-lived and rate-limited; store no plaintext recovery secret; mechanism and retention require approval. |
| AssistantProfile | Stable profile identity | id, account_id, name, status, active_version_id | Owner-scoped; no client-defined tool permissions. |
| ProfileVersion | Immutable profile snapshot | id, profile_id, version, schema_version, context_fields, policy_reference, created_at | Immutable after publish; each call references version. |
| SupportedRouteConfiguration | Versioned record of a route/device/operator/plan combination considered for support | id, route_type, region, device_os_range, operator/plan/SIM constraints, capability_set, evidence_status, evidence_ref, reviewed_at, version, status | Evidence-backed allowlist; unsupported or unverified combinations cannot be activated. Exact fields depend on the route and must not imply evidence exists before it is collected. |
| RoutingConfig | Selected route and setup state | id, account_id, supported_route_configuration_id, route_type, operator/region metadata, state, verified_at, last_check | Sensitive; changes audited; no secrets exposed to client. References the versioned route definition tested for this account. |
| CallSession | User-visible call lifecycle metadata | id, account_id, profile_version_id, routing_config_id, state, started_at, ended_at, route_status | One user-visible session may reference multiple provider legs; no raw audio in row. |
| ProviderLeg | One externally meaningful telephony/media leg within a CallSession | id, call_session_id, provider, provider_account_ref, opaque_provider_leg_ref, leg_role, direction, state, started_at, ended_at, last_authoritative_event_id, safe_failure_code | Unique reference scope must be provider/account-aware; do not infer caller identity, takeover success or billable duration from leg existence alone. |
| CallSummary | Structured outcome | id, call_session_id, summary_text, intent, confidence, processing_state, created_at | Access through call owner; separately deletable. |
| TranscriptArtifact | Transcript pointer/metadata | id, call_session_id, storage_ref, language, state, retention_until | Raw content stored separately with restricted access; optional. |
| AudioArtifact | Recording pointer/metadata | id, call_session_id, storage_ref, consent/notice reference, retention_until, state | Optional and high sensitivity; no default retention until approved. |
| CallEvent | Call lifecycle event | id, call_session_id, event_type, provider_event_id, occurred_at, received_at, safe_metadata | Idempotent provider event; no raw payload unless justified. |
| UsageEvent | Immutable provider usage or ledger event | id, account_id, call_session_id, provider, event_key, event_kind, unit_type, provider_quantity, normalized_quantity, occurred_at, received_at, reconciliation_state, original_event_id | Define uniqueness scope by provider/account/route/event type/period as appropriate; corrections/reversals are new linked entries, never destructive edits. |
| PlanEntitlement | Limits and features | id, account_id, plan_code, included_units, effective_from, effective_to, status | Versioned; limits enforced server-side. |
| ConsentRecord | Account-holder choices/consent evidence | id, account_id, subject_type, purpose, notice_version, choice, timestamp, withdrawn_at | Represents the account holder's choice only; do not treat it as evidence that a third-party caller was notified or consented. |
| CallerDisclosureEvent | Record a required caller-facing disclosure attempt/result where applicable | id, call_session_id, disclosure_policy_version, event_type, occurred_at, result, safe_metadata | Records what the system attempted or delivered, not legal consent by itself; exact event fields and retention depend on route and counsel review. |
| DeletionRequest | Track user/account erasure workflow | id, account_id, requested_scope, state, requested_at, completed_at, exception_code | Idempotent; parent workflow only; completion depends on required target results and approved exceptions. |
| DeletionTarget | Track one required deletion destination/artifact class | id, deletion_request_id, target_type, target_ref, state, attempt_count, last_attempt_at, next_retry_at, result_code, exception_owner, exception_expires_at | Minimal safe metadata; distinguishes primary stores, providers, exports, indexes and backups; exact targets and exceptions require approved lifecycle policy. |
| AuditEvent | Security/accountability | id, actor_type, actor_id, account_id, action, target_type, target_id, timestamp, safe_metadata | Append-only access policy; exclude raw call content. |
| ConnectorOperation | Server-defined tool registry | id, domain, operation_key, version, schema_ref, scope_policy, status | Configuration controlled by operator; never writable by ordinary user profile. |
| ToolInvocation | Track action requests/results | id, call_session_id, operation_id, input_digest, authorization_result, outcome, idempotency_key | Do not store secrets; redact payloads; every invocation authorized. |
| SupportCase | User issue/abuse report | id, account_id, call_session_id, category, state, created_at | Least-privilege access; no raw audio required by default. |

## 3. Relationship outline

- Account 1:N AuthIdentity and AccountSession; RecoveryChallenge belongs to one account and is consumed or expired at most once.
- Account 1:N AssistantProfile.
- AssistantProfile 1:N ProfileVersion; one active version is selected by profile policy.
- Account 1:N RoutingConfig, CallSession, UsageEvent, ConsentRecord, DeletionRequest and SupportCase.
- SupportedRouteConfiguration is versioned independently; RoutingConfig references the exact route definition used for setup and verification.
- CallSession references the exact ProfileVersion and RoutingConfig used; CallSession 1:N ProviderLeg and CallEvent.
- CallerDisclosureEvent belongs to a CallSession and records disclosure execution separately from account-holder ConsentRecord. The legal meaning of each event remains jurisdiction- and route-dependent.
- CallSession 1:N ToolInvocation; optionally 0..1 or 1:N summaries/artifacts depending on revisions.
- UsageEvent references CallSession when attributable; adjustments/reversals reference the original event and remain auditable.
- DeletionRequest 1:N DeletionTarget; request-level completion is derived from the required target outcomes and approved exception policy, not from a single primary-store deletion.
- ToolInvocation references a server-defined ConnectorOperation version.
- Future domain-specific objects remain in the authoritative domain system; AI stores a scoped reference and only necessary response/outcome fields.

## 4. Sensitive fields and access controls

- Account, caller number, routing configuration, personal context, transcript, recording, summary, consent and support case are sensitive.
- Every read/write path must check account ownership and feature permission.
- Support access requires purpose, least privilege, audit and, where possible, time-limited access.
- Transcript/audio retrieval should use expiring authorized access rather than public object URLs.
- Connector credentials belong in a secrets manager or provider-controlled credential store, not in these entities or mobile configuration.
- Logs and audit metadata should avoid storing raw transcript/audio and should minimise phone numbers.

## 5. Data lifecycle and deletion

Deletion semantics must be defined for each entity and all downstream copies:
- profile context and versions;
- call metadata and summaries;
- transcript/audio artifacts and provider-side copies;
- search indexes, caches and derived summaries;
- exports, support attachments and analytics;
- backups according to documented expiration;
- consent and security records where limited retention may be legally necessary.

A deletion request should expose its state and record any legal/operational exception. Do not promise immediate physical deletion from immutable backups unless the system can actually guarantee it.

## 6. Open modelling questions

- Whether one account can have multiple profiles/phone numbers and how profiles map to routes.
- Which fields and uniqueness scopes are required for provider-leg mapping across forwarding, media and takeover legs.
- How supported-route combinations and their evidence are versioned, reviewed and retired.
- Which per-target deletion outcomes are required to claim completion or a reviewed exception.
- Whether transcript/audio is stored at all and where.
- How to model caller notice/consent without collecting unnecessary third-party identifiers.
- Which metadata must be retained for billing reconciliation and disputes.
- Data residency and tenant-isolation strategy.
- Retention durations, deletion SLAs, backups and legal holds.
- Search/indexing and encrypted-field requirements.

## 7. Approval status

No schema, database, field type, retention duration or migration is approved. Finalise this model only after product scope, provider contracts, data inventory and legal review are approved.

## Business phone assistant domain alignment — 2026-10-13

The [Business Assistant Domain Contract Draft](BUSINESS_ASSISTANT_DOMAIN_CONTRACT_DRAFT.md) identifies candidate domain records that need explicit review against this model: Organization, OrganizationMembership, WorkflowDefinition, immutable WorkflowVersion, WorkflowExecution, CallerReference, ActionExecution, and source-provenanced CallObservation/CallOutcome. These are conceptual candidates, not approved tables or migrations. Do not add them to a production schema until the owner approves the scope and the data lifecycle, authorization and provider evidence are reviewed.


## Proposed business requirement entity alignment — 2026-10-15

The following entity relationships are candidates for the proposed REQ-017–REQ-022 addendum. They are not approved tables, ORM models or migrations.

| Proposed requirement | Candidate entities / relationships | Required ownership, authorization and lifecycle decisions |
|---|---|---|
| REQ-017 | Organization; OrganizationMembership; role/grant record; AuditEvent | Organization owns business resources; membership is separate from Account; every read/write/search/export/job/callback needs server-side organization authorization. Define member removal and historical audit retention. |
| REQ-018 | WorkflowDefinition 1:N immutable WorkflowVersion; WorkflowExecution references exactly one version | Define draft/published/paused/retired state, validation result, publisher, timestamps, rollback policy and version pinning. Retain only the approved metadata needed for audit; workflow content may itself contain sensitive business data. |
| REQ-019 | CallerReference; CallerMatchResult or minimal match metadata; VerificationAttempt/VerificationState | Avoid copying full customer records into the AI system. Define identifier minimization, match ambiguity, verification evidence retention and deletion exceptions. Caller phone number alone is not an authenticated identity. |
| REQ-020 | CallObservation; CallSession; ProviderLeg; CallOutcome/ReconciliationRecord | Separate provider observations from the assistant session; store source/provenance and event/receive times. Define deduplication, late/conflicting event handling and data lifecycle. |
| REQ-021 | ActionExecution; ConnectorOperationVersion; ActionResult/ReconciliationReference | Bind action to organization, call, workflow version and approved operation. Store minimal request/result metadata, idempotency reference and authoritative outcome; secrets stay in managed credential storage. |
| REQ-022 | MetricDefinition/version; derived tenant-scoped query/report results; optional correction/audit metadata | Prefer derived metrics unless a justified snapshot is needed. Define data source, denominator, freshness, late-event correction, aggregation leakage controls and retention. |

Cross-cutting: document the retention/deletion target for workflow versions, caller references, verification attempts, call observations, action payload/result metadata, audit events and any derived reports. Do not assume deleting a CallSession automatically deletes provider-side observations or downstream business-system records; record external-system ownership and deletion limitations.
