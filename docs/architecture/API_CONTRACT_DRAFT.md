# API Contract Draft — AI Voice Platform

**Status:** Conceptual contract, not an approved API specification. No implementation authorised.

## 1. Design rules

- Version public APIs explicitly; use a consistent error envelope and correlation ID.
- Authenticate every control-plane request; enforce object-level authorization at each resource.
- Do not accept arbitrary connector URLs, SQL, executable code, provider credentials or model/system prompts from untrusted clients.
- Use idempotency keys for mutating requests and provider callbacks where duplication is possible.
- Keep long-lived call media off ordinary JSON control-plane endpoints; use the selected provider's authenticated media transport.
- Return honest status: configured, pending, verified, degraded, failed, disabled or unknown.
- Separate user-visible call metadata from raw audio/transcript access.
- Distinguish the account holder's product choices/consents from notices or legal-basis evidence relating to third-party callers; a product account setting is not proof that a caller was notified or consented.
- Keep domain connectors server-defined and scoped.
- Define rate limits, retention impact, audit events and abuse controls per operation.

## 2. Resource areas and proposed operations

These names are illustrative; route shapes and schemas require review.

| Resource area | Proposed operation | Purpose | Security/contract notes |
|---|---|---|---|
| Account | Read current account | Show account status and user settings | Derived from authenticated principal; do not trust client-supplied owner ID. |
| Account/session | List and revoke active sessions/devices | Let an account owner inspect and revoke access after device loss or suspected compromise | Require recent re-authentication for sensitive changes; revoke server-side; do not rely on client-only logout. |
| Account recovery | Start and complete recovery | Recover access through an approved recovery factor | Anti-enumeration responses, rate limits, short-lived single-use challenges, replay protection and audit; mechanism remains undecided. |
| Profile | Create/update profile draft | Configure voice, language, boundaries and structured context | Schema allowlist; validate length/types; version every published change. |
| Profile | Publish profile version | Make reviewed configuration active | Explicit user action; preserve version reference for each call session. |
| Profile / call summary | Correct supported summary fields | Let the account owner correct supported extracted facts | Owner-authorized, validated fields; preserve an audit/version history; do not silently rewrite source call evidence or treat a correction as model-confirmed truth. |
| Routing | List supported route options / check eligibility | Show only route configurations eligible for the user's known region/device/operator/plan/SIM inputs | Derive from a versioned server-side supported-route registry with evidence status; unknown or untested combinations must remain unsupported/unverified, not inferred compatible. |
| Routing | Get routing status | Show active/setup/failed state | Never infer success solely from a client action. |
| Routing | Start setup / verify route | Guide and verify approved route | Route-specific capability and operator constraints; rate limit tests. |
| Routing | Disable route | Stop assistant handling and guide restoration | Idempotent; report verified vs unverified deactivation distinctly. |
| Calls | List calls / get call metadata | History and status | Pagination, per-user authorization, minimal fields. |
| Calls | Get summary | Read summary and confidence/status | Separate permission and retention from transcript/audio. |
| Calls | Get transcript/audio access | Optional media access | Feature entitlement, consent/legal policy, expiring access and audit. |
| Calls | Request user takeover | Transfer/bridge where supported | Only expose for validated routes; idempotent; time-bounded state transition. |
| Usage | Read usage | Show minutes/limits | Explain source metric and update delay. |
| Usage | Read invoice/plan | Show plan state | Billing provider is source of truth for payment state; usage ledger for metered events. |
| Privacy | Request export | Create export job | Re-authentication, limited expiry, audit, least privilege. |
| Privacy | Request deletion | Begin data deletion workflow | Idempotent; expose pending/completed/exception state. |
| Privacy | Get deletion status | Show request-level progress and safe outstanding-target/exception categories | Account-authorized; distinguish requested, in progress, partial, primary removed, completed and reviewed exception; never claim full deletion based only on primary-store state. |
| Support | Report call issue | Capture category/session ID | Do not require raw content upload; redact fields. |
| Connector | Execute allowed action | Invoke a pre-registered domain capability | Server-selected operation, typed payload, scoped auth, policy check, audit and idempotency. |

## 3. Common error envelope

Proposed shape:
- code: stable machine-readable error identifier;
- message: safe user-facing explanation;
- request_id: correlation ID;
- retryable: boolean;
- retry_after_seconds: optional;
- details: field validation or safe recovery hints, never secrets or other users' data.

Suggested error classes: UNAUTHENTICATED, FORBIDDEN, NOT_FOUND, VALIDATION_FAILED, ROUTE_UNSUPPORTED, ROUTE_UNVERIFIED, STATE_CONFLICT, RATE_LIMITED, QUOTA_EXCEEDED, PROVIDER_UNAVAILABLE, PROVIDER_TIMEOUT, MEDIA_FAILED, TRANSFER_UNSUPPORTED, DELETION_PENDING, INTERNAL_ERROR.

Do not expose provider tokens, raw call content, stack traces or internal hostnames in client errors.

## 4. Provider webhook contract requirements

- Verify the provider's signature according to official documentation before trusting body content.
- Enforce timestamp/replay rules where the provider supports them.
- Store provider event ID and idempotency result; repeated events must not duplicate side effects or billing.
- Validate expected account/route/session mapping.
- Bound body size and accepted content types.
- Reject unknown event types safely and alert on repeated invalid signatures.
- Define event ordering and final-state reconciliation.
- Specify the canonical call state machine and allowed transitions, including late/out-of-order events, route deactivation, provider-leg versus user-visible call identity, and reconciliation when provider state disagrees with local state.
- Keep raw payload retention minimal and redact personal content.

## 5. Tool/connector contract

Each server-defined operation must include:
- operation ID and version;
- domain and tenant scope;
- typed input/output schema;
- authorization policy and required user confirmation;
- timeout and retry/idempotency semantics;
- data minimisation rules;
- audit event type;
- allowed profile types;
- error taxonomy and safe user-facing result;
- rate/cost limit.

The model may propose a tool call, but only the server-side policy gateway may authorize it. Profile text cannot register a new operation or widen scopes.

## 6. API non-functional requirements

- Authentication/authorization on every protected operation.
- Defined pagination and maximum page size.
- Rate limits per user, IP, route setup, export/deletion and provider webhook.
- Request deadlines and cancellation propagation.
- Structured audit and metrics without raw call content by default.
- Versioned schemas and backward-compatibility policy.
- Contract tests for client/server and provider adapters.
- Data retention and deletion implications documented per resource.
- OpenAPI specification generated only after the domain model and requirements are approved.

## 7. Decisions still open

Authentication protocol/provider; session ownership and concurrency; exact endpoints/schemas; webhook providers; API versioning style; event bus; data model; idempotency storage; transcript/audio delivery; rate limits; error codes; connector versioning.

## 8. Approval status

No endpoint, schema or provider contract is approved. Convert this draft into versioned OpenAPI and provider-specific contract tests only after the owner approves the baseline and implementation gate.