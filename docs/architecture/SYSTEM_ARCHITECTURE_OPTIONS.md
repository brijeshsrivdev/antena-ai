# System Architecture Options and Trust Boundaries

**Status:** Architecture discovery draft; no option is approved. Date: 2026-10-11. No product code or deployment is authorised.

## 1. Goals and constraints

- Support an Android-first personal call assistant if the call route is feasible.
- Provide a dedicated AI API for account/profile configuration, session orchestration, policy enforcement, metering and provider abstraction.
- Keep telephony/media routing distinct from profile configuration and domain business logic.
- Make the AI layer usable by multiple profiles over time, without letting profiles or clients grant arbitrary capabilities.
- Use Antena's trusted backend APIs for any future hospitality operations. Never query Antena's database directly from the AI service.
- Treat legal/advocate and other professional profiles as future integrations, not initial dependencies.
- Support a 10,000-registered-user planning target, but size against measured active/concurrent sessions and provider constraints.

## 2. Candidate deployment shapes

### Option A — Managed voice platform with custom AI API
Mobile app → supported carrier-forwarding/PSTN/SIP path → managed telephony/media → voice-agent worker/framework → model/STT/TTS providers. The custom AI API handles identity, profiles, policies, usage, history and connectors.

**Benefits:** faster path to validate media/session lifecycle; managed infrastructure may reduce realtime operations.
**Costs/risks:** provider pricing, regional number/call support, data processing, lock-in, transfer/takeover limitations and hidden media charges.

### Option B — Programmable telephony plus direct model APIs
Mobile app → carrier-forwarding or VoIP route → programmable telephony/media stream → custom realtime orchestration → speech/model providers. The AI API and realtime worker are separate deployable responsibilities even if initially co-located.

**Benefits:** more control over the pipeline, event model and provider choice.
**Costs/risks:** more implementation/operations complexity, difficult latency tuning, provider-specific media behaviour and need for robust reconnect/failure handling.

### Option C — Self-hosted media and orchestration
Mobile app/network route → self-hosted SIP/WebRTC/media service → orchestration framework → hosted or self-hosted speech/model services.

**Benefits:** more control over media/data and potential long-term cost flexibility at sufficient scale.
**Costs/risks:** highest operational burden; SIP security, capacity, on-call, patching, observability, availability and model-serving costs. Not justified until traffic and quality requirements are measured.

### Option D — VoIP-first product
User receives or routes calls through a product-controlled VoIP number/app; cloud service handles the media. Native cellular number takeover is not promised.

**Benefits:** more controllable media path and simpler end-to-end test boundary.
**Costs/risks:** changes user behaviour, number acquisition/porting, PSTN charges, regional rules and reduced fit for users who expect their existing SIM number to remain the interface.

## 3. Recommendation for discovery

Keep Option A and Option B as the primary candidates and Option D as a fallback/product alternative. Do not choose until the actual incoming-call route, caller-ID behaviour, takeover, legal requirements and written provider costs are verified. Option C should be justified by measured scale/cost/privacy needs, not assumed to be cheaper.

## 4. Logical component boundaries

- **Android client:** onboarding, constrained profile forms, routing setup/status, controls, history/summary UI, privacy controls and usage display. It is not trusted to set tool permissions.
- **Identity/account boundary:** authenticated user, session/device management, account recovery and abuse controls.
- **AI API/control plane:** profile versions, policy rules, session metadata, call lifecycle coordination, usage metering, provider configuration and audit events.
- **Realtime session worker:** manages one live conversation, deadlines, turn-taking, tool requests, cancellation, provider fallback and termination. Must be bounded by concurrency and spend controls.
- **Telephony/media adapter:** normalises provider webhooks/media events, validates signatures, maps call IDs to sessions, and enforces idempotency.
- **Speech/model adapters:** explicit interfaces for STT, LLM/realtime model and TTS, with provider-specific limits represented in capability metadata.
- **Policy/tool gateway:** authorises each tool call against user, tenant, profile, scope, resource and action. Never trust profile text as a permission grant.
- **Persistence:** profiles, versioned preferences, call metadata, summaries, consent/notice versions, usage events and audit. Audio/transcripts are separate data classes with separate retention.
- **Domain connector registry:** server-defined, allowlisted operations only. Hospitality calls Antena APIs with tenant-scoped credentials; no direct database access.
- **Operations plane:** metrics, traces, alerts, cost monitoring, provider health, support/incident workflows and deletion jobs.

## 5. Conceptual flow

1. User authenticates and configures a constrained profile.
2. Server validates profile schema and stores a versioned configuration; secret/provider settings remain server-side.
3. User configures an approved routing method and completes a test call.
4. Telephony provider sends a signed event; adapter verifies it, applies idempotency and creates a session only if route/account state permits.
5. Session worker receives supported media, applies disclosure and policy, and calls speech/model adapters within deadlines.
6. Any tool request is validated by policy/tool gateway; a hospitality operation, if later enabled, uses a trusted Antena API and its authorization contract.
7. Session termination emits durable usage/audit events; summary generation is separate from the realtime path where possible.
8. User sees summary/usage and can correct, export or delete records under the retention policy.

## 6. Security and reliability boundaries

- Authenticate every control-plane API; authorise at object/tenant level, not just by endpoint.
- Verify provider webhook signatures and reject replayed/duplicate events safely.
- Never accept arbitrary client-defined connector URLs, SQL, scripts or unrestricted tool schemas.
- Separate user profile data from system policy and tool grants.
- Keep model context scoped to the current user/call; minimise data sent to each provider.
- Bound each call by duration, concurrency, spend and tool budget.
- Use deadlines and cancellation propagation across STT/model/TTS; retries must not duplicate actions or billing events.
- Record audit metadata without raw transcript/audio by default.
- Have explicit behaviour for provider outage, transfer failure, no audio, timeouts, abuse, emergency cues and exhausted quotas.
- Keep call routing state observable and reversible.

## 7. Conceptual API areas to specify

These are resource areas, not final endpoints:
- account/session;
- profile and profile-version management;
- routing setup, verification, status and deactivation;
- call lifecycle events and call history;
- summary/transcript/audio access with distinct permissions;
- user preferences and caller policies;
- usage ledger, plan limits and billing webhooks;
- data export/deletion requests;
- trusted connector capabilities and tool execution;
- support/incident reporting.

Each API needs authn/authz, idempotency, rate limits, versioning, error taxonomy, audit semantics, retention impact and test contract before implementation.

## 8. Decisions still open

Telephony route; managed versus custom media; realtime framework; model/STT/TTS provider; deployment region; stateful session strategy; storage/retention; authentication; pricing/metering; SLOs; provider failover; API versioning; tenant model; connector permissions.

## 9. Required next steps

1. Complete call-route feasibility and provider quote collection.
2. Define target journeys and measurable quality/latency requirements.
3. Map data classes and threat model.
4. Create ADRs for telephony, realtime stack, data retention, auth and deployment only when evidence is sufficient.
5. Validate component boundaries against numbered requirements.
6. Obtain owner approval before any experiment or implementation.