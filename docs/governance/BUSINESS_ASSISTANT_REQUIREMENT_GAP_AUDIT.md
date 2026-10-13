# Business Phone Assistant — Requirement and Acceptance Coverage Gap Audit

**Date:** 2026-10-13  
**Status:** Desk-only gap analysis; draft and unapproved. No implementation, interviews, provider outreach, route tests, legal review, performance tests or product tests performed. All supplemental scenarios are NOT RUN.

## 1. Purpose and decision boundary

PR #5 records the primary product hypothesis as a configurable, multi-tenant AI business phone assistant. The existing requirement set and original planned acceptance catalogue were written primarily around a personal call assistant. This audit maps what can be reused, what requires reinterpretation, and what is not adequately specified for the business-oriented hypothesis.

This document is not approval of the detailed MVP, requirements, workflow schema, integrations, legal position, numeric thresholds or implementation. Existing REQ/NFR IDs remain stable draft identifiers. Do not silently treat a lexical match as semantic coverage.

## 2. Summary

- The existing 16 functional requirements and 10 NFRs provide useful shared foundations: route state, provider session integrity, bounded voice interaction, disclosure, summaries, usage, privacy, isolation, trusted connectors, support, observability and account security.
- The existing 68 planned scenarios cover the existing REQ/NFR draft, but they do **not** fully cover the business workflow lifecycle, caller verification, missed-call event visibility, ticket-action outcomes or business dashboard metric contracts.
- The most significant semantic change is REQ-003: a personal profile/context is not the same thing as a tenant-owned, constrained, versioned workflow definition with draft/test/publish/pause/retire lifecycle and per-call version pinning.
- REQ-011 must be interpreted as organization/tenant isolation across business users, workflows, phone routes, callers/customer records, calls, integrations, tickets, exports and background work—not only user-to-user isolation.
- Caller ID may assist matching but is not authentication. A caller verification policy is required before protected customer data is disclosed.
- “Missed call” visibility depends on provider/carrier event evidence. The assistant alone cannot prove calls that never reach it.
- Ticket creation is only a candidate action. A selected typed connector, authorization contract, idempotency and authoritative outcome/reconciliation are prerequisites before promising it.
- No requirement, threshold or scenario is approved or executed by this audit.

## 3. Existing requirement coverage crosswalk

| Existing ID | Reuse for business assistant | Business-specific gap or required reinterpretation | Recommended disposition |
| --- | --- | --- | --- |
| REQ-001 Activation/routing state | Business phone route activation, verified state, pause/disable and recovery | Route belongs to an organization; workflow publication and route activation are distinct states. Define what can be disabled if provider confirmation is unavailable. | Retain ID; revise wording and state contract during baseline revision. |
| REQ-002 Supported-route eligibility | Provider/number/region/plan eligibility and pre-activation verification | Specify hosted number, forwarding, SIP/PBX or other route candidates without assuming any is supported; define call-event and media coverage separately. | Retain ID; route matrix and evidence gate remain open. |
| REQ-003 Versioned assistant profile/context | Constrained configuration and policy separation | Major mismatch: business workflow schema, approved blocks, validation, test fixtures, draft/publish/pause/retire, change audit and per-call version pinning are missing as explicit acceptance criteria. | Expand or split into a dedicated workflow requirement before baseline approval. |
| REQ-004 Disclosure/bounded conversation | AI disclosure, intent handling, safe response and termination | Define business identity, approved opening/disclosure, out-of-scope handling, uncertainty branch and applicable language policy. | Retain ID; align to business caller journey after policy review. |
| REQ-005 Authenticated call lifecycle | Provider event authentication, idempotency, ordering and call/session identity | Explicitly model organization, number/route, provider call IDs, provider legs, workflow version and calls known only through event/record evidence. | Retain ID; update event mapping and tests. |
| REQ-006 Real-time quality/cancellation | Voice quality, interruption, timeout and safe termination | Measure business workflow completion and caller-safe fallback as well as voice interaction; no latency target is approved. | Retain ID; update evaluation rubric after workflow selection. |
| REQ-007 Takeover/handoff | Human handoff or safe fallback where route supports it | Handoff must be capability-gated; business hours, target/queue, timeout, failed transfer and fallback behavior are not yet specified. | Conditional; no handoff promise without provider/route evidence. |
| REQ-008 Post-call summary/uncertainty | Summary and accurate extracted outcome | Add structured call outcome, collected fields, customer verification status, action/ticket state and provenance; model text is not authoritative action evidence. | Retain ID; expand business outcome contract. |
| REQ-009 Usage/cost guardrails | Idempotent metering, limits and reconciliation | Business plans may require per-organization, phone number, workflow, connected minute and provider-leg attribution; billing unit and all-leg cost remain open. | Retain ID; reconcile with business workload scenarios and quotes. |
| REQ-010 Privacy/consent/retention | Notice, consent records where applicable, deletion and data minimization | Identify business configuration, caller data, customer lookup, ticket payloads, audio/transcript/summary and provider-event metadata as separate data classes. | Retain ID; policy and qualified jurisdiction review remain blockers. |
| REQ-011 Tenant/profile isolation | Core multi-tenant security requirement | Current user-oriented criteria do not explicitly enumerate organization membership/roles and isolation of workflows, numbers, caller/customer records, connectors, tickets, exports, callbacks and jobs. | Expand or split; add organization-level negative tests. |
| REQ-012 Trusted domain connector boundary | Allowlisted, typed, scoped connector actions | Ticket/case creation and customer lookup need selected integration contracts, least privilege, schema validation, idempotency, authoritative result and ambiguous-result reconciliation. | Retain ID; connector remains unselected and ticket creation unapproved. |
| REQ-013 Call history/media controls | Call inbox/detail, optional transcript/audio lifecycle | Add outcome taxonomy, provider event provenance, workflow version, action status, missing/unobserved event distinction and tenant-scoped dashboard queries. | Retain ID; update call-history scope and data contract. |
| REQ-014 Support/urgent disable | Business owner can pause handling and report incidents | Need organization-level roles, route/workflow pause semantics, and explicit handling of route disable that cannot be authoritatively confirmed. | Retain ID; define owner/admin/operator permissions. |
| REQ-015 Observability/recovery | Provider/model/connector failures and bounded retries | Define authoritative event source and denominator for each dashboard metric; distinguish assistant-handled, caller-abandoned, missed-before-connection, route failure, unobserved and action-unknown. | Retain ID; add event taxonomy and metric contract. |
| REQ-016 Account authentication/recovery | Dashboard identity, session revocation and recovery | Add organization invitation, membership changes and role changes; account authentication alone does not establish organization authorization. | Retain ID; complement with tenant membership/authorization requirements. |
| NFR-001 Latency | End-to-end voice and action latency | Define clock boundaries across telephony, model, connector and caller-visible confirmation after a workflow is selected. | Keep threshold open; add metric definitions first. |
| NFR-002 Route success | Business-number route and media/event delivery | Separate call connection, media availability, event visibility and missed-call event coverage; each needs a defined denominator. | Keep blocked pending route/provider evidence. |
| NFR-003 Conversation completion | Safe completion of an eligible workflow | Define completed workflow vs safe termination, caller abandonment, unsupported intent and failed/unknown action. | Add outcome rubric before target approval. |
| NFR-004 Availability | Service and dependency availability | Define product service boundary and provider dependency reporting; do not imply the platform observes all calls. | Keep target open. |
| NFR-005 Privacy/deletion | Data-class lifecycle and target-level deletion | Include workflow revisions, caller/customer records, connector payloads, ticket references and provider event metadata where retained. | Keep blocked on data map/policy. |
| NFR-006 Capacity | Peak calls, sessions and background work | Registered-user count is insufficient; model organizations, active numbers, call arrival rate, peak concurrent calls, connected minutes and connector traffic. | Update workload model before sizing. |
| NFR-007 Cost | Cost per connected minute and account | Include provider call legs, model/media, connector and support costs; no public headline price is an all-in quote. | Keep unapproved pending comparable quotes. |
| NFR-008 Accessibility | Dashboard and setup accessibility | Include workflow-builder, call inbox/detail, status/alerts and keyboard/screen-reader behavior. | Retain; UX scope needs update. |
| NFR-009 Recovery | Control-plane recovery | Include workflow publication state, route/number config, integration credentials and event/usage reconciliation. | Retain; RTO/RPO remain open. |
| NFR-010 Security | Threat-model verification | Add tenant boundary, workflow publish privilege, connector permission, caller verification, webhook replay and action ambiguity. | Retain; threat-model update required. |

## 4. Scope gaps that must be resolved before a baseline

| Gap | Why existing requirements/tests are insufficient | Required artifact before approval |
| --- | --- | --- |
| Organization and membership model | Account login is not equivalent to organization/tenant membership or role authorization. | Organization/member/role requirements and API/data contract. |
| Workflow lifecycle | Profile versioning does not define constrained workflow blocks, validation, test, publish, rollback, pause, retirement or immutable call version binding. | Workflow lifecycle requirement, state contract and UX flow. |
| Caller matching and verification | Caller ID is a signal, not proof of identity; existing account authentication does not cover a third-party caller. | Verification policy by workflow and protected-data class, with failure paths. |
| Call outcome taxonomy | Generic call history cannot safely distinguish call activity, caller abandonment, route failure and unobserved calls. | Canonical event/outcome model with authoritative source for each state. |
| Missed-call visibility | Calls that never reach the assistant may be invisible without carrier/provider events or call-detail evidence. | Provider capability matrix, coverage limits and reconciliation design. |
| Ticket/case actions | A model response or connector timeout does not prove a ticket exists. No connector is selected. | First integration decision, typed schema, auth scopes, idempotency and authoritative status/reconciliation. |
| Dashboard metric semantics | Volume and success percentages are misleading without event source, denominator, exclusions and freshness. | Metric dictionary and query/tenant isolation rules. |
| Human handoff | Existing conditional takeover scenario is not a business routing contract. | Route capability evidence, target/queue policy, timeout and fallback definition. |
| Business workload/cost | 10,000 registered users is not peak concurrency; business usage differs from personal usage. | Revised workload scenarios and comparable provider quote basis. |
| Business data lifecycle | Customer records, workflows and connector payloads extend the data map beyond personal profiles/call records. | Data inventory, retention/deletion map, access matrix and privacy review. |

## 5. Supplemental planned acceptance scenarios

The following IDs supplement—not replace—the original TC/NT catalogue. They are proposed to expose business-assistant gaps; all remain **NOT RUN**, and some cannot be made executable until scope/provider/connector decisions are approved.

| Test ID | Area | Planned scenario and expected observable result | Status / dependency |
| --- | --- | --- | --- |
| BPA-001 | Organization isolation | A member of Organization A attempts to read or mutate Organization B's workflow, number, caller/customer record, call, integration or ticket; deny without data leakage or side effect. | NOT RUN — role and tenant contract needed. |
| BPA-002 | Membership/roles | Removed member or downgraded role attempts configuration, publication, export and operational actions; deny according to the approved role matrix and audit the decision. | NOT RUN — role matrix open. |
| BPA-003 | Workflow schema | Submit unknown blocks, malformed fields, unsupported actions, arbitrary URLs/SQL/scripts or prompt text attempting to grant permissions; reject before publication. | NOT RUN — canonical block/schema contract needed. |
| BPA-004 | Workflow publication | Draft, tested, published, paused and retired workflow versions are exercised; only eligible published versions handle new calls, and state is truthful. | NOT RUN — lifecycle/state contract open. |
| BPA-005 | Version pinning | Publish a new workflow during an active call; the active call stays bound to its documented version while a new call uses the new eligible version. | NOT RUN — version policy open. |
| BPA-006 | Caller matching | Incoming caller ID matches zero, one or multiple customer records; assistant follows match policy and does not reveal protected details based on caller ID alone. | NOT RUN — matching policy/data model open. |
| BPA-007 | Caller verification | Caller fails, abandons or disputes the required verification step; protected data/actions remain unavailable and a safe intake/escalation path is offered. | NOT RUN — verification policy/legal review open. |
| BPA-008 | Intent uncertainty | Caller intent is unsupported or classification confidence is insufficient under the approved rubric; ask a bounded clarification or use safe fallback, without invoking an action. | NOT RUN — rubric/workflow policy open. |
| BPA-009 | Ticket creation success | Approved workflow invokes a configured typed connector; show a ticket reference only after authoritative success and bind the result to the correct tenant/call. | NOT RUN — connector not selected. |
| BPA-010 | Ambiguous write | Connector times out after possible side effect; do not blindly duplicate creation or claim success; expose pending/unknown and reconcile by idempotency/reference. | NOT RUN — connector contract/reconciliation open. |
| BPA-011 | Connector authorization | Workflow or model attempts an unregistered operation, wrong tenant scope, excessive fields or unauthorized write; reject before side effect and audit safely. | NOT RUN — connector/permission schema open. |
| BPA-012 | Caller abandonment | Caller disconnects at each configured intake milestone; record the observed milestone and abandonment outcome without claiming successful workflow completion. | NOT RUN — event and outcome definitions open. |
| BPA-013 | Missed before assistant connection | Provider/carrier event shows a call was offered but assistant did not connect; show a missed-before-connection state only when evidence supports it. | NOT RUN — provider event coverage unproven. |
| BPA-014 | Unobserved call boundary | No reliable provider/carrier event exists for a call; do not infer a complete missed-call count or report an unobserved call as captured. | NOT RUN — source coverage contract open. |
| BPA-015 | Route/provider failure | Evidence indicates route or provider failure; distinguish it from caller abandonment, assistant failure and unknown status. | NOT RUN — provider event mapping open. |
| BPA-016 | Dashboard metric provenance | Each displayed call/ticket/success metric has a documented source, denominator, exclusions and freshness; unknown events are not silently counted as success or absence. | NOT RUN — metric dictionary open. |
| BPA-017 | Handoff capability gate | For an unsupported route, hide/disable handoff and use only an approved fallback; for a supported route, report transfer success only on authoritative confirmation. | NOT RUN — route capability evidence open. |
| BPA-018 | Workflow/route urgent pause | Authorized operator pauses a workflow or disables a route during an incident; show requested, pending, confirmed or unverified states without conflating workflow pause and telephony disable. | NOT RUN — authority and route-state contract open. |

## 6. Recommended requirement change plan

1. Keep existing IDs stable while preparing a reviewed business-oriented revision; do not silently repurpose acceptance criteria.
2. Expand or split REQ-003 for the constrained workflow schema/lifecycle and version pinning.
3. Expand REQ-011 and REQ-016 to distinguish organization membership/roles from account authentication and caller identity verification.
4. Expand REQ-005, REQ-013 and REQ-015 around provider event provenance, canonical call outcomes, missed-call visibility and dashboard metric definitions.
5. Expand REQ-012 with the first selected connector's typed action contract, idempotency and ambiguous-result reconciliation; ticket creation remains conditional until selected.
6. Update the UX inventory/wireflows, API/data/state contracts, threat model, privacy/data inventory, workload model, and scope-to-requirement crosswalk to the approved workflow.
7. Review the original TC/NT scenarios for personal-assistant assumptions and revise them only through a deliberate requirement version change. Supplemental BPA scenarios remain planned and NOT RUN.
8. Approve measurable thresholds only after the workload, provider capability, measurement boundaries and evidence method are specified.
9. Keep Phase 0 incomplete until required customer evidence, route/provider evidence, qualified privacy/legal review and owner decisions are documented.
10. Require explicit owner approval of the complete discovery baseline and a separate implementation authorization before any product code.

## 7. Verification of this audit

This pass is a documentation crosswalk. It does not execute the original or supplemental scenarios, validate provider capabilities, establish customer demand, select an integration, approve thresholds, complete legal review, or authorize implementation. All 68 original catalogue scenarios and all 18 BPA scenarios remain NOT RUN.
