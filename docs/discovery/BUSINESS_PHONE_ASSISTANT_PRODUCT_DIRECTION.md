# Business Phone Assistant — Product Direction Reconciliation

**Status:** Owner direction captured for discovery; detailed MVP, requirements and release gates remain unapproved. Documentation only. No product implementation or external experiments are authorized by this document.

## 1. Primary product hypothesis

The primary MVP hypothesis is a **configurable AI business phone assistant**. A business configures how the assistant should handle eligible inbound calls to a supported business phone number. Callers interact with that assistant, and the business receives a clear, auditable record of call outcomes and any approved actions.

The product should be designed as a reusable, multi-tenant voice platform. Personal call-assistant mode is not the primary MVP; it may be reconsidered as a later product mode after the business workflow is validated.

This is a product-direction update, not proof of demand, telephony feasibility, legal compliance, provider support or approval to implement.

## 2. Actor vocabulary

| Concept | Preferred UI term | Domain/technical term | Meaning |
| --- | --- | --- | --- |
| Paying/configuring account | Business or Organization | Tenant | The organization subscribing to the platform and controlling its assistant, workflows, connected number, users and records. |
| Person calling the business | Caller; End Customer in business context | Caller / Customer record | The third party who calls the business and may or may not already have a customer record. |
| Human using the dashboard | Business user / Agent | Tenant member / Operator | An authorized person who configures workflows, reviews calls or handles escalations. |
| AI call session | Call | Call session | A provider-correlated call lifecycle, including route/provider events and the assistant interaction where available. |
| Work item created from a call | Ticket / Case | Ticket | A business record created only through a configured, authorized integration and confirmed result. |

Keep `Tenant` as the backend isolation boundary. Prefer `Business` or `Organization` in customer-facing UI. Use `Caller` for the person on the phone. Do not assume that the incoming number proves a caller's identity or ownership of a customer account.

## 3. Core business-admin journey

1. A business creates an account and invites authorized team members.
2. It connects or configures a phone number only through a route supported by the selected provider and deployment model.
3. It configures an assistant workflow from approved blocks: greeting/disclosure, intent selection/classification, data collection, lookup, conditional branching, approved action, confirmation, escalation and end-of-call.
4. It configures which customer records or systems can be queried, which actions may be performed, and when human review is required.
5. It tests the workflow with synthetic scenarios and completes route verification before activating the assistant.
6. It views call activity, summaries, confirmed actions, tickets, failures and follow-up work in a tenant-isolated dashboard.
7. It can pause/disable handling and inspect truthful route, provider and workflow status.

Workflow configuration is constrained structured data, not arbitrary code, SQL, scripts, prompts that grant permissions, or client-supplied connector URLs.

## 4. Core caller journey

1. A caller dials the business number.
2. If the supported route delivers an observable call event/media session, the platform resolves the tenant and applicable published workflow from trusted server-side configuration.
3. The assistant provides the approved AI disclosure and greeting, then determines the caller's intent.
4. The assistant may match the presented phone number to a business customer record. If it asks for a registered number or another identifier, it must follow a configured verification policy. Caller ID alone is not authentication.
5. The workflow collects the minimum required facts and may query only authorized, tenant-scoped data sources.
6. It may create a ticket/case or perform another explicitly approved action through a typed, allowlisted connector.
7. The assistant confirms an action only after authoritative success; uncertain or failed actions are reported honestly and routed to retry/reconciliation or a human.
8. The call ends, and the dashboard shows the supported call outcome, summary and action status, with content availability governed by the approved privacy and retention policy.

## 5. Workflow configuration model — candidate building blocks

A workflow version may eventually describe:
- Trigger: eligible inbound call, known/unknown caller, business schedule or supported call event.
- Opening: business identity, AI disclosure, greeting and language.
- Intent: a controlled intent list or bounded classification with an uncertainty branch.
- Identity: phone-number match, customer lookup, additional verification and failure branch.
- Data collection: required fields, validation and repeat/clarification behavior.
- Conditions: explicit branches on verified record attributes or collected values.
- Read action: a pre-registered, tenant-scoped query capability.
- Write action: ticket/case creation or another approved operation with idempotency and confirmation.
- Escalation: human handoff where supported, callback request or safe message capture.
- Completion: caller confirmation, reference number only after confirmed creation, and end-call.
- Failure handling: timeout, provider outage, connector error, ambiguous result, caller disconnect and out-of-scope request.
- Publication: draft, tested, published, versioned, paused and retired states, with each call pinned to a workflow version.

These are candidate concepts. The canonical schema, supported block list, version rules and permission model are not yet approved.

## 6. Example: product complaint workflow

1. Ask whether the caller is reporting a new issue or following up.
2. Attempt a tenant-scoped match using the incoming number, if permitted and available.
3. If no reliable match exists, ask for the registered number or reference and follow the business's approved verification steps.
4. Identify the product/order and collect the complaint description and required fields.
5. If the customer or purchase cannot be verified, do not reveal protected customer/order details; continue only with a safe generic intake path or escalate.
6. Create a ticket through an approved support connector using an idempotency key.
7. If the result is confirmed, provide the returned ticket reference. If the result is ambiguous, do not claim success; mark it pending/unknown and route it for reconciliation.
8. Present the call, identification status, summary, ticket status and any next action in the business dashboard.

## 7. Missed calls and outcome semantics

Do not use one undifferentiated "missed call" status.

- **Assistant-handled:** a session reached the assistant and the caller interacted with it.
- **Caller abandoned:** the caller disconnected before the configured intake/handling milestone.
- **Missed before assistant connection:** a call event is known, but the assistant did not answer/connect.
- **Route/provider failure:** evidence indicates delivery, connection or provider failure.
- **Unobserved call:** the platform has no reliable event proving the call happened; it must not claim comprehensive missed-call capture.
- **Action failed or unknown:** the call was handled, but an attempted ticket or connector action failed or has an ambiguous outcome.

Capturing calls that never reach the assistant requires provider/carrier call-event or call-detail evidence. It is not guaranteed by the assistant alone. Define event source, coverage and reconciliation for every advertised missed-call metric.

## 8. Business dashboard — candidate information architecture

- **Overview:** call volume, answer/connection outcomes, unresolved calls, confirmed tickets and workflow/provider health. Each metric needs a documented denominator and event source.
- **Call inbox:** answered, caller-abandoned, missed-before-connection, failed-route and needs-attention queues, with filters and search.
- **Call detail:** event timeline, caller number/label and identification confidence/status, workflow version, summary, available transcript/audio only when separately approved, actions attempted, connector result, ticket link and audit trail.
- **Workflow builder:** drafts, versions, test scenarios, publish/pause status and change history.
- **Customers/integrations:** scoped connection status and minimum necessary customer lookup fields; not a general-purpose data export surface.
- **Tickets/follow-up:** confirmed ticket reference, status, owner and pending/failed action reconciliation.
- **Team and access:** least-privilege roles, tenant membership and audit.
- **Usage and billing:** provider-derived connected/billable units, per-leg cost visibility where available, limits and alerts.
- **Privacy and operations:** retention/deletion status, support issue reporting, route/provider health and disable controls.

Do not display fabricated example metrics as real data, infer ticket creation from a model response, or expose one tenant's records to another.

## 9. Security and trust invariants

- Every workflow, phone route, call, customer lookup, ticket and dashboard query is bound server-side to a tenant.
- Caller ID is a matching signal, not proof of identity; disclose no protected customer information until the configured verification policy is satisfied.
- Model-generated intent or extracted fields are untrusted inputs. Validate them before branching or performing actions.
- Only server-registered typed connectors can run. The model cannot expand its own tools or privileges.
- Writes require authorization, tenant scope, idempotency, audit and explicit confirmation rules appropriate to the action.
- Provider callbacks must be authenticated, replay-safe, idempotent and reconciled when duplicated or out of order.
- Never claim a ticket, transfer, callback, refund or other action succeeded without authoritative confirmation.
- Define safe handling for emergencies, abusive calls, sensitive data, silence, caller disconnection and provider/connector outages.
- Audio, transcript and summary collection, retention and access remain separately gated by privacy, provider terms and jurisdiction-specific review.
- Human handoff is conditional on the selected route/provider actually supporting it; otherwise offer only validated alternatives.

## 10. Discovery and release gates still open

Before baselining the business-oriented MVP, resolve and evidence:
1. Target business segment and highest-value first workflow; product complaints are an example, not yet a validated vertical.
2. Number model: existing business number/forwarding, hosted number, SIP/PBX or another provider-supported route.
3. Exact inbound call event/media support, caller-ID behavior, missed-call event coverage, transfer/handoff and safe fallback.
4. Workflow block catalogue, version/publish model, testing model and permission/confirmation semantics.
5. First customer system integration and ticket data contract; no assumption that a generic ticket connector exists.
6. Tenant roles, end-customer identification and verification requirements.
7. Dashboard metrics, outcome taxonomy and authoritative sources for each status.
8. Privacy, recording/transcription, disclosure, retention, deletion and target-jurisdiction legal review.
9. Provider pricing for all call legs and AI/connector costs, usage limits and unit economics.
10. Numbered requirements, acceptance criteria, planned scenarios and traceability updated to the approved scope.
11. Customer interviews, route/provider evidence and explicit owner approval of the baseline.

## 11. Boundary of this change

This direction reconciliation is desk-only documentation. It does not mean customer demand is validated, any provider supports the desired route, legal review is complete, a ticketing integration exists, requirements are approved, Phase 0 has passed, or product implementation is authorized.
