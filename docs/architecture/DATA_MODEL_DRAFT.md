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
| AssistantProfile | Stable profile identity | id, account_id, name, status, active_version_id | Owner-scoped; no client-defined tool permissions. |
| ProfileVersion | Immutable profile snapshot | id, profile_id, version, schema_version, context_fields, policy_reference, created_at | Immutable after publish; each call references version. |
| RoutingConfig | Selected route and setup state | id, account_id, route_type, operator/region metadata, state, verified_at, last_check | Sensitive; changes audited; no secrets exposed to client. |
| CallSession | Call lifecycle metadata | id, account_id, profile_version_id, provider, provider_call_ref, state, started_at, ended_at, route_status | Provider reference uniqueness/idempotency; no raw audio in row. |
| CallSummary | Structured outcome | id, call_session_id, summary_text, intent, confidence, processing_state, created_at | Access through call owner; separately deletable. |
| TranscriptArtifact | Transcript pointer/metadata | id, call_session_id, storage_ref, language, state, retention_until | Raw content stored separately with restricted access; optional. |
| AudioArtifact | Recording pointer/metadata | id, call_session_id, storage_ref, consent/notice reference, retention_until, state | Optional and high sensitivity; no default retention until approved. |
| CallEvent | Call lifecycle event | id, call_session_id, event_type, provider_event_id, occurred_at, received_at, safe_metadata | Idempotent provider event; no raw payload unless justified. |
| UsageEvent | Billable event ledger | id, account_id, call_session_id, provider, event_key, unit_type, quantity, timestamp, reconciliation_state | Unique idempotency key; immutable corrections via adjustment events. |
| PlanEntitlement | Limits and features | id, account_id, plan_code, included_units, effective_from, effective_to, status | Versioned; limits enforced server-side. |
| ConsentRecord | Notice/choice evidence | id, account_id, subject_type, purpose, notice_version, choice, timestamp, withdrawn_at | Store minimum evidence; caller-notice events may need separate representation. |
| DeletionRequest | Track erasure workflow | id, account_id, requested_scope, state, requested_at, completed_at, exception_code | Idempotent; tracks provider and backup lifecycle. |
| AuditEvent | Security/accountability | id, actor_type, actor_id, account_id, action, target_type, target_id, timestamp, safe_metadata | Append-only access policy; exclude raw call content. |
| ConnectorOperation | Server-defined tool registry | id, domain, operation_key, version, schema_ref, scope_policy, status | Configuration controlled by operator; never writable by ordinary user profile. |
| ToolInvocation | Track action requests/results | id, call_session_id, operation_id, input_digest, authorization_result, outcome, idempotency_key | Do not store secrets; redact payloads; every invocation authorized. |
| SupportCase | User issue/abuse report | id, account_id, call_session_id, category, state, created_at | Least-privilege access; no raw audio required by default. |

## 3. Relationship outline

- Account 1:N AssistantProfile.
- AssistantProfile 1:N ProfileVersion; one active version is selected by profile policy.
- Account 1:N RoutingConfig, CallSession, UsageEvent, ConsentRecord, DeletionRequest and SupportCase.
- CallSession references the exact ProfileVersion and RoutingConfig used.
- CallSession 1:N CallEvent and ToolInvocation; optionally 0..1 or 1:N summaries/artifacts depending on revisions.
- UsageEvent references CallSession when attributable; provider adjustments remain auditable.
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
- How to represent a forwarded call versus provider legs and takeover legs.
- Whether transcript/audio is stored at all and where.
- How to model caller notice/consent without collecting unnecessary third-party identifiers.
- Which metadata must be retained for billing reconciliation and disputes.
- Data residency and tenant-isolation strategy.
- Retention durations, deletion SLAs, backups and legal holds.
- Search/indexing and encrypted-field requirements.

## 7. Approval status

No schema, database, field type, retention duration or migration is approved. Finalise this model only after product scope, provider contracts, data inventory and legal review are approved.