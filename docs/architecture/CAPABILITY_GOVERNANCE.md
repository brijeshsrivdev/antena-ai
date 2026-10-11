# AI Profile Capability Governance

**Status:** Proposed architecture/security policy. Not implemented or approved.

## Purpose
Allow one voice platform to support personal profiles and future domain profiles without giving a language model unrestricted access to systems. The model may propose a tool call; trusted application code authorizes, validates, executes and audits it.

## Non-negotiable boundaries
1. **Domain systems remain authoritative.** Hospitality reads/writes go through trusted Antena backend APIs. No direct database access.
2. **No client-supplied connector URLs.** Destinations, credentials, scopes and policies are provisioned server-side.
3. **No arbitrary code execution or dynamic tool creation from profile text.**
4. **Least privilege by profile, tenant and action.** A tool's existence does not mean every profile may use it.
5. **Explicit write confirmation.** Actions changing reservations, customer records, messages or payments must follow a server-enforced confirmation policy.
6. **No hidden authority from prompts.** Profile instructions cannot override access control, consent, business rules, spend caps or safety policy.
7. **Tenant isolation is enforced by backend authorization**, not by prompting the model to remember tenant IDs.
8. **Consequential tool actions are auditable**, with actor/profile version, tenant, capability, decision, outcome and correlation ID; avoid logging raw sensitive content unnecessarily.
9. **Idempotency and replay protection** for write actions and provider webhooks.
10. **Fail closed for uncertain authorization or connector state.** Never invent success or availability.

## Proposed capability record
Each capability defines a stable ID/version, purpose, user-visible disclosure, allowed profile types, tenant scope, input schema, read/write classification, sensitivity, authorization, confirmation policy, rate/cost limit, timeout, idempotency, output schema, retention class, error/retry policy, safe fallback, audit event, monitoring, owner, review date and deprecation plan.

## Proposed capability classes

| Class | Examples | Default rule |
|---|---|---|
| C0 — Public read | Public FAQs, published property address/hours | Enable after source validation |
| C1 — Tenant-scoped read | Approved tenant policy, booking status for an authorised user | Tenant scope and field minimisation required |
| C2 — Reversible write | Create callback request, capture enquiry | Confirm intent, idempotency and audit |
| C3 — Consequential write | Create/modify/cancel booking, send external message, charge/refund | Explicit confirmation and domain validation; consider human approval |
| C4 — Restricted | Payments, identity documents, sensitive personal data, legal/medical/financial commitments | Disabled by default; separate risk/legal approval or out of scope |

## Tool execution pipeline
1. Authenticate account and establish tenant scope outside the model.
2. Load a versioned server-managed profile and capability allowlist.
3. Parse the proposed action against a strict schema.
4. Apply identity, consent, tenant, action class, business rule, rate/spend limit and confirmation checks.
5. Execute via trusted connector with scoped service identity.
6. Validate domain response and normalise output.
7. Return bounded result to the model; never expose credentials or unrestricted records.
8. Record an audit event and meter usage.
9. If any step is uncertain, deny/stop, inform the user and route to a human or safe fallback.

## Prompt injection and untrusted content
Caller speech, transcripts, documents, retrieved pages and domain text are untrusted data, not instructions. They cannot alter tool permissions, profile scope or system policy. Tool outputs are schema-validated and treated as data. A caller cannot ask the assistant to disclose another tenant's information, change forwarding rules, reveal secrets or invoke an unapproved tool.

## Hospitality profile boundaries
Initial candidates for investigation: answer approved public FAQs, capture caller intent, create callback/enquiry requests, and retrieve authorised booking status where identity and tenant scope are proven. Do not claim live room/table availability, price, reservation confirmation, cancellation or refund unless the Antena domain API returns an authoritative result and policy allows the action.

## Profile lifecycle
- Profiles are server-defined templates with bounded structured user configuration.
- Each published version has owner, purpose, allowed capabilities, exclusions, test cases and review date.
- Capability changes require review and an audit event.
- Rollback to a prior approved profile version must be supported.
- Future advocate/legal profile is excluded from MVP and requires separate discovery and legal review.

## Acceptance evidence required before implementation
Threat-model review; tenant-isolation tests; prompt-injection test corpus; capability authorization matrix; schema-validation tests; replay/idempotency tests; audit redaction review; spend/rate-limit tests; failure/revocation tests; explicit owner approval.
