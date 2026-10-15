# Business Phone Assistant Requirements Addendum — Draft

**Status:** PROPOSED DRAFT; not owner-approved and not baselined. Documentation-only. No implementation is authorized.  
**Date:** 2026-10-15  
**Parent set:** `CORE_REQUIREMENTS_DRAFT.md` (REQ-001–REQ-016; NFR-001–NFR-010)  
**Purpose:** Add business-specific requirements without silently reinterpreting inherited personal-assistant requirements.

## 1. How to use this addendum

The original core requirements were drafted for a personal AI call assistant. Several requirements are reusable foundations, but the business phone assistant has additional concepts: organizations and membership, tenant-owned workflows, third-party caller verification, provider-observed call outcomes, and connector actions with authoritative results.

The identifiers below are **proposed working IDs** for cross-document review. They are not approved baseline requirements, and the existing IDs are not thereby approved. Do not implement against this addendum until the owner approves the complete discovery baseline and separately authorizes implementation.

- Keep the existing REQ/NFR IDs stable while reviewing this proposal.
- Where this addendum overlaps an existing requirement, treat it as a business-specific elaboration candidate—not an implicit replacement.
- No numeric threshold is introduced here. Thresholds require a named workload, measurement boundary, denominator, evidence source and explicit owner approval.
- Every item remains subject to segment/workflow validation, route/provider evidence, privacy/security review and UX/API/data reconciliation.

## 2. Proposed requirements

### REQ-017 — Organization membership and resource authorization

**Priority:** P0 candidate. **Status:** PROPOSED, not approved.  
**Intent:** Organization-scoped resources and operations must be authorized using the authenticated account, active membership, role, resource ownership and requested operation.

Acceptance criteria:
- Every organization-scoped read, write, search, export, callback, background job and connector operation derives organization scope from trusted server-side authorization, not a client-supplied organization ID alone.
- An account without active membership cannot access an organization's resources; membership removal or role downgrade takes effect according to a documented revocation policy.
- Cross-organization access attempts do not disclose resource existence or content beyond the approved error contract and cause no side effects.
- The role matrix explicitly distinguishes viewing calls, editing workflows, publishing workflows, managing routes, managing integrations, exporting data, managing members and billing.
- Caller ID, workflow text, model output and possession of an opaque resource ID never grant organization authorization.

**Related existing requirements:** REQ-011, REQ-016, NFR-010.  
**Planned scenarios:** BPA-001, BPA-002.  
**Open dependencies:** Organization membership/data model, role matrix, API authorization contract, support access model and threat-model review.

### REQ-018 — Constrained workflow definition, lifecycle and version binding

**Priority:** P0 candidate. **Status:** PROPOSED, not approved.  
**Intent:** Business users configure inbound call workflows only through a validated, constrained set of product-defined blocks and permissions.

Acceptance criteria:
- Workflow configuration rejects unknown blocks, invalid fields, unsupported transitions, arbitrary executable code, SQL, client-supplied URLs and model-granted permissions before publication.
- Draft, validation, synthetic test, publish, pause and retirement states have explicit permitted transitions, actor permissions and auditable state changes.
- Only an eligible published version may be selected for a new call. Each execution records the exact immutable workflow version it uses.
- Publishing a new version does not silently change the version used by an active call; active-call behavior is governed by a documented version policy.
- Workflow pause and telephony-route disable are distinct controls with separate requested, pending, confirmed or unverified states.
- Synthetic workflow tests cannot create real external side effects unless a separately approved sandbox/contract-test mechanism is explicitly selected.

**Related existing requirements:** REQ-001, REQ-003, REQ-005, REQ-012, REQ-014.  
**Planned scenarios:** BPA-003, BPA-004, BPA-005, BPA-018.  
**Open dependencies:** Workflow schema, allowed block registry, version policy, UX lifecycle, audit events and connector simulation boundary.

### REQ-019 — Caller matching and protected-data verification

**Priority:** P0 candidate if customer data or protected actions are in the first workflow. **Status:** PROPOSED, not approved.  
**Intent:** Caller matching must not be confused with authentication or authorization.

Acceptance criteria:
- Caller ID may be used as a matching signal but is not, by itself, proof of caller identity or permission to disclose protected customer information.
- When a workflow requires caller verification, protected fields and actions remain unavailable until the configured approved verification policy succeeds.
- Zero, one or multiple customer-record matches produce explicit branches; ambiguity does not select a record silently.
- Failed, abandoned, disputed or unavailable verification follows a bounded, documented fallback and does not leak whether protected data exists.
- Verification methods, data collected, retry limits, accessibility, threat assumptions and jurisdiction-specific requirements are approved before a live workflow relies on them.

**Related existing requirements:** REQ-004, REQ-010, REQ-011, REQ-012.  
**Planned scenarios:** BPA-006, BPA-007.  
**Open dependencies:** First workflow, data classification, verification policy, privacy/legal review and abuse threat model.

### REQ-020 — Evidence-backed call outcomes and observation coverage

**Priority:** P0 candidate. **Status:** PROPOSED, not approved.  
**Intent:** The product must represent what the evidence supports and make the limits of call observation explicit.

Acceptance criteria:
- Call observations preserve source, provider/route reference, event time, receive time, correlation and deduplication/reconciliation status as defined by the selected route contract.
- The outcome model distinguishes, at minimum, assistant-handled, caller-abandoned, missed-before-assistant-connection, route/provider failure, workflow/action failure, unknown or conflicting state, and unobserved-call coverage limitation where applicable.
- The system does not claim full missed-call capture unless selected provider/carrier evidence demonstrates the required coverage for the advertised route.
- Absence of an assistant session is not proof that no call occurred; absence of a provider event is not proof that a call was missed.
- Handoff is exposed only for a route with verified capability; transfer success is shown only after authoritative confirmation.
- Workflow pause, route-disable request, route-disable confirmation and unverified route state remain distinct.

**Related existing requirements:** REQ-001, REQ-002, REQ-005, REQ-007, REQ-013, REQ-014, REQ-015; NFR-002, NFR-003, NFR-009.  
**Planned scenarios:** BPA-012, BPA-013, BPA-014, BPA-015, BPA-017, BPA-018.  
**Open dependencies:** Selected route/provider event matrix, event taxonomy, reconciliation policy, route/handoff tests and operational recovery contract.

### REQ-021 — Authorized connector action and authoritative outcome

**Priority:** P0 only if a domain write action is selected for the first workflow; otherwise conditional/deferred. **Status:** PROPOSED, not approved.  
**Intent:** Any external business action must use a server-registered typed connector operation with least privilege and a reconciliable outcome.

Acceptance criteria:
- Only approved connector operations, schemas and scopes can be invoked; model text and workflow configuration cannot register new connectors, expand scopes or bypass authorization.
- Every action is bound to the authorized organization, call, workflow version and actor/policy context.
- A connector timeout or accepted request is not treated as success. The UI presents success only after the connector's authoritative result contract confirms it.
- Retrying a potentially completed write uses an agreed idempotency/reconciliation contract and does not blindly create duplicates.
- Action states distinguish not requested, denied, pending, confirmed success, confirmed failure and unknown/reconciliation-required.
- Ticket/case creation remains out of committed scope until the first connector and its authentication, schema, scopes, failure behavior, cost and support contract are selected.

**Related existing requirements:** REQ-008, REQ-009, REQ-012, REQ-015; NFR-007, NFR-010.  
**Planned scenarios:** BPA-009, BPA-010, BPA-011.  
**Open dependencies:** Validated workflow, selected integration, typed connector contract, idempotency key policy, audit model and authoritative reconciliation source.

### REQ-022 — Dashboard metric provenance and tenant-scoped reporting

**Priority:** P0 candidate for an operational business product. **Status:** PROPOSED, not approved.  
**Intent:** Business dashboard metrics must be explainable, tenant-scoped and based on explicit evidence contracts.

Acceptance criteria:
- Every displayed call, missed-call, completion, ticket/action and usage metric has a documented source, inclusion/exclusion rule, denominator, time window, freshness indication and unknown-state treatment.
- Metrics do not count unknown/unobserved events as success or as evidence that no call occurred.
- Late, duplicate, conflicting and reconciled events follow documented metric correction rules; historical corrections are auditable where needed.
- Every query and export enforces organization authorization and the approved data-access policy.
- The dashboard distinguishes assistant/workflow outcomes from provider/route availability and from external connector-action outcomes.

**Related existing requirements:** REQ-009, REQ-011, REQ-013, REQ-015; NFR-002, NFR-003, NFR-005, NFR-007, NFR-010.  
**Planned scenarios:** BPA-016, supported by BPA-012–BPA-015.  
**Open dependencies:** Canonical event model, metric dictionary, reporting query model, workload and usage definition.

## 3. Proposed coverage map

| Proposed requirement | Planned scenario IDs | Main documents to reconcile |
| --- | --- | --- |
| REQ-017 Organization membership and resource authorization | BPA-001, BPA-002 | Domain contract, data model, API contract, threat model, UX team/access flows |
| REQ-018 Constrained workflow definition, lifecycle and version binding | BPA-003, BPA-004, BPA-005, BPA-018 | Workflow block/schema proposal, state/event contract, API contract, UX wireflows, audit model |
| REQ-019 Caller matching and protected-data verification | BPA-006, BPA-007 | Data model, privacy/data inventory, threat model, caller workflow, legal/privacy review |
| REQ-020 Evidence-backed call outcomes and observation coverage | BPA-012, BPA-013, BPA-014, BPA-015, BPA-017, BPA-018 | Provider capability matrix, state/event contract, call inbox UX, incident/recovery runbooks |
| REQ-021 Authorized connector action and authoritative outcome | BPA-009, BPA-010, BPA-011 | Capability governance, API/data contract, connector registry, action state contract, selected integration |
| REQ-022 Dashboard metric provenance and tenant-scoped reporting | BPA-016 and outcome-source scenarios BPA-012–BPA-015 | Metric dictionary, usage model, dashboard UX, event/reconciliation contract |

## 4. Decisions deliberately not made

This addendum does not select:
- the first business vertical, segment or validated workflow;
- a telephony/provider route or whether missed-call event coverage is complete;
- a ticket/case system or any production connector;
- a caller verification method;
- legal basis, disclosure/consent language, retention period or jurisdictional legal interpretation;
- dashboard success thresholds, SLOs, concurrency, price or cost limits.

These remain discovery gates, not implementation assumptions.

## 5. Review and approval checklist

Before this addendum is baselined:
1. Review every proposed requirement with the owner and mark accepted, revised, deferred or rejected.
2. Reconcile the accepted set against the core requirement draft, scope catalogue, UX inventory/wireflows, API/domain/data/state contracts, threat model, traceability matrix and acceptance catalogue.
3. Add any missing test cases and confirm that each criterion is observable with a named evidence source.
4. Resolve whether REQ-021 is core or deferred based on the validated first workflow.
5. Approve thresholds only after measurement boundaries and workload assumptions are documented.
6. Keep all planned scenarios NOT RUN until a separate approved test plan and safe execution authorization exist.
7. Keep Phase 0 incomplete until its evidence gates are met; require separate explicit implementation authorization before product code.

