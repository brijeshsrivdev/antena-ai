# Current State

Snapshot: 2026-10-13. Repository: brijeshsrivdev/antena-ai. Default branch: main.

- Product implementation: not started and not authorised.
- Discovery: in progress; charter approval pending.
- Commercial brand: not selected or cleared.
- Owner's process requirement: complete research, product/marketing strategy, pricing, architecture, UX, dependency evaluation, requirements and roadmap before any coding. Owner explicitly approves implementation start.

## Current primary product direction — 2026-10-13
- Primary MVP hypothesis: configurable, multi-tenant AI business phone assistant.
- Business/Organization is the preferred UI term; Tenant remains the backend isolation boundary; Caller/End Customer refers to the person calling the business.
- Businesses configure versioned inbound workflows from constrained blocks; callers interact with the assistant; authorized business users review call records, outcomes, confirmed tickets/actions and pending work.
- Product complaints and ticket creation are illustrative workflow examples, not yet validated vertical/integration decisions.
- Personal AI call-assistant mode is a later candidate, not the primary MVP.
- Business-number route, missed-call event coverage, caller identification, workflow schema, ticket connector, dashboard metrics, provider economics and jurisdiction-specific policy remain open.
- Use trusted, tenant-scoped connectors only; no direct database access or client-supplied arbitrary URLs, SQL, scripts or permissions.
- Hospitality may be a later domain integration through existing Antena APIs, after capability audit; legal/advocate support is not a first-release dependency.
- Target scale: 10,000 registered users remains a planning target, not a concurrency specification; model business accounts, active tenants, calls, connected minutes and peak concurrency separately.

## Open questions
Target segment, launch geography, core feature parity, call-routing model, provider stack, cost/minute, pricing, consent/retention, SLOs, acquisition strategy, open-source dependency choices, brand and domain availability.

## Discovery increments recorded
The existing baseline includes initial competitor/market analysis, Android telephony feasibility, customer validation plan, privacy/regulatory issue register, pricing/economics, capacity model, product scope, UX inventory, positioning/GTM hypotheses, open-source/provider review, voice-stack candidate review, requirements draft, architecture options, threat model, data inventory, test strategy, traceability matrix, API contract and data model drafts.

Latest additions:
- docs/research/COMPETITOR_MATRIX.md: feature and business comparison of Equal AI, hiRobin, Truecaller Assistant, native screening, Tring, voice-agent platforms and business telephony vendors.
- docs/business/COST_SCENARIO_MODEL.md: sensitivity analysis at assumed ₹4/₹7/₹12 per connected minute; not provider quotes. Illustrates that ₹249/month can be uneconomic at modest usage depending on actual cost.
- docs/discovery/CUSTOMER_INTERVIEW_PACK.md: neutral interview script, evidence capture and proposed qualitative exit gates. No interviews have occurred.
- docs/research/TELEPHONY_VALIDATION_PROTOCOL.md: owner-run carrier/device test matrix and safety boundaries. No live route tests have occurred.
- docs/discovery/UX_WIREFLOW_SPEC.md: textual onboarding, incoming-call, history, profile, billing and deletion flows. No visual prototype was created.

## Evidence and constraints
- Equal AI is the most direct benchmark found; hiRobin demonstrates a broader task-completion proposition. Public claims/store listings are not independent performance tests.
- Android call-screening/redirection APIs do not establish unrestricted cellular audio capture. Carrier forwarding and cloud voice remain hypotheses until route-specific tests and written provider confirmation.
- Public price anchors differ in scope and are not comparable all-in quotes. The ₹4/₹7/₹12 connected-minute cases are sensitivity assumptions only.
- 10,000 registered users is not a concurrency specification. MAU, minutes, peaks and provider limits need measured evidence.
- Antena hospitality integration must use trusted APIs; never direct database access or client-supplied arbitrary URLs.
- No interviews, carrier/device tests, written route-specific provider quotes, legal opinions, benchmarks, load tests or product implementation have been performed.

## Remaining Phase 0 gaps
1. Conduct customer interviews and preserve negative/contradictory evidence.
2. Run owner-supervised test calls on selected devices/carriers using the documented protocol.
3. Obtain at least two comparable written provider quotes for the exact route.
4. Complete source validation and hands-on competitor review where possible.
5. Set measurable acceptance thresholds and reconcile requirements, UX, API, data model, security and legal controls.
6. Complete exact-version dependency/licence/provider-terms review and jurisdiction-specific legal advice.
7. Validate visual wireflows with users, then complete a consistency audit.
8. Obtain explicit owner approval of the baseline before any implementation.

## Last verified state
README and linked documents must be verified against current main after this increment. Baseline remains a broad draft, incomplete and unapproved. Product implementation remains unauthorised.


## Latest discovery increment — 2026-10-11
- Added Android route decision analysis grounded in official CallScreeningService, CallRedirectionService and Google Play permissions guidance. It reinforces that screening/redirection APIs do not themselves provide unrestricted cellular audio access.
- Added a provider RFP and scorecard covering exact route eligibility, all call legs, model/media components, pricing, data terms, security, support and exit requirements. No provider has been contacted and no quote has been received.
- Added capability governance for profile allowlists, tenant-scoped Antena APIs, confirmation rules, audit, idempotency and prompt-injection boundaries.
- Added low-cost GTM experiments for consumer and hospitality segments. No marketing experiment has run.
- Updated README index. The baseline remains a draft; no coding or deployment is authorised.


## Quality evaluation increment — 2026-10-11
- Added docs/quality/VOICE_AGENT_EVALUATION_PLAN.md with synthetic-corpus design, consented controlled-call guidance, candidate latency/accuracy/route gates, security zero-tolerance cases, reproducibility metadata and pilot approval requirements.
- The numeric thresholds are proposed starting points only. No benchmark or load test has run, and no threshold is approved.

## Provider pricing evidence increment — 2026-10-11
- Added `docs/research/PROVIDER_PRICING_EVIDENCE.md` and indexed it from README.
- Public desk research found Ringg advertises ₹6/connected minute for a bundled voice-agent product; this does not establish support for the existing-number personal call-assistant route.
- Exotel's published business-phone packages exclude Voice Streaming, which requires a separate quote; Exotel's documentation also says mobile-carrier forwarding charges are separate.
- Truecaller's carrier-specific forwarding setup is evidence that this pattern exists in-market, not proof that our product can use the same route or terms.
- Updated the cost model to clarify non-comparable price scopes. No provider has been contacted, no quote received, and no call-route test performed.
- The baseline remains documentation-only, incomplete and unapproved. Implementation remains unauthorised.

## Competitor evidence increment — 2026-10-11
- Updated `docs/research/COMPETITOR_MATRIX.md` with Sharyx AI Call Assistant as an adjacent Android-listed product that describes forwarding to a dedicated AI number.
- Clarified that Equal AI's public terms describe variable paid-feature pricing; App Store ₹149/₹249 entries are not a universal subscription quote.
- README currently indexes 40 unique documentation links, including the provider pricing evidence document. The linked docs are still drafts and the baseline is not approved.

## Baseline consistency audit increment — 2026-10-11
- Added `docs/governance/BASELINE_CONSISTENCY_AUDIT.md`, a cross-document readiness review covering 12 P0/P1 gaps.
- Key findings: call-route feasibility and customer evidence remain unproven; provider pricing references have different scopes; cost/capacity scenarios use different workload assumptions; legal/privacy controls depend on route/provider/jurisdiction; requirement status language and traceability need normalization.
- The audit makes no product decisions and does not authorise implementation. README indexes the audit.

## Cross-document normalization increment — 2026-10-11
- Added `docs/architecture/WORKLOAD_SCENARIO_BASELINE.md` as a shared proposed low/base/high workload table: 20k / 150k / 600k monthly connected minutes, with explicit MAU, calls/user, duration and illustrative concurrency assumptions.
- Linked the shared scenario reference from capacity and pricing documents. The separate 10k / 75k / 240k minute set remains labelled as alternate sensitivity analysis, not directly comparable.
- Normalized the core requirements header to `DRAFT`, because formal review has not started. This does not approve any requirement.
- Added `docs/governance/BASELINE_CONSISTENCY_AUDIT.md` and linked it from README. Baseline remains incomplete; no coding or deployment is authorised.

## Requirements and MVP scope increment — 2026-10-11
- Expanded `docs/requirements/TRACEABILITY_MATRIX.md` to map REQ-001–REQ-015 and NFR-001–NFR-010 to evidence state, UX, architecture/data boundaries, risks, verification and proposed release gates.
- Added `docs/discovery/MVP_SCOPE_AND_FEATURE_GATES.md` to distinguish core candidates, conditional features and deferred scope. It is not an approved MVP.
- Updated `REQUIREMENTS_INDEX.md` to point to the traceability and scope-gate artefacts.
- Remaining blockers are unchanged: customer interviews, owner-supervised route tests, comparable provider quotes, jurisdiction-specific legal review, complete measurable acceptance criteria, and owner approval.


## Acceptance-threshold register increment — 2026-10-12
- Added `docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md` and linked it from README and REQUIREMENTS_INDEX.md.
- The register distinguishes proposed candidate thresholds from open values. No threshold has owner approval; REQ-001 and REQ-006 now reference proposed AT-001/AT-004 values in the canonical requirements; NFR target decisions remain open.
- Candidate controls include a two-action disable path, an exploratory route-verification target, measurable cancellation, and zero-tolerance checks for duplicate charges, cross-tenant access and unauthorised actions. These require review and evidence before use as release gates.
- No interviews, carrier/device tests, written provider quotes, legal opinions, benchmarks, load tests or implementation have occurred. Implementation remains unauthorised.


## Owner decision pack increment — 2026-10-12
- Added `docs/governance/OWNER_DECISION_PACK.md` to consolidate ten discovery decisions, their evidence needs, blocked dependencies and the explicit implementation gate.
- Linked the decision pack from README. It records the current hypotheses without treating them as approved and lists evidence not yet collected.
- Next evidence-led work should prioritize customer interviews, controlled call-route feasibility, comparable written provider quotes and jurisdiction-specific legal review. Experiments require owner approval; product code remains unauthorised.


## Phase 0 evidence workbook increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md` with private participant-record guidance, route-test capture rows, provider quote comparison and evidence-to-decision logging.
- This prepares fieldwork; it does not claim that interviews, telephony tests or provider outreach have occurred. Owner approval and safety checks are required before experiments.
- README now indexes the workbook. Implementation remains unauthorised.


## Experiment approval checklist increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md` as a scope-specific approval gate for discovery activities, with separate conditions for interviews, telephony tests, provider outreach and UX validation.
- The checklist covers consent, minimum necessary data, private handling of identifiable evidence, budget ceilings, safe restoration/disable procedures, stop conditions and post-activity review.
- It is a preparation document, not approval to run fieldwork. No interviews, provider outreach, route tests, quotes, legal opinions or benchmarks are claimed complete; implementation remains unauthorised.
- README and roadmap now index/reference the checklist.


## Phase 0 exit criteria increment — 2026-10-12
- Added `docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md`, consolidating 20 gates across customer validation, route feasibility, provider costs, legal/privacy, scope, UX, requirements, architecture, security, operations, brand and owner decisions.
- The map explicitly distinguishes prepared documentation from uncollected evidence and from owner approvals. It records Phase 0 as incomplete and implementation as unauthorised.
- README and roadmap now index/reference the exit map. No external experiment or implementation is claimed complete.


## Residual-risk register increment — 2026-10-12
- Added `docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md` with 18 risks, current evidence state, mitigation references and stop conditions.
- Linked it from README, Phase 0 exit map, owner decision pack and consistency audit. Risks remain open unless evidence and explicit owner disposition support closure; implementation remains unauthorised.


## Repository navigation verification — 2026-10-12
- Parsed the current README Markdown links and compared all 49 local `.md` targets against the recursive Git tree on `main`; all 49 targets exist. No broken local README document links were found in this check.
- This is a repository-link check only; it does not validate external URLs, source freshness, factual claims or the completeness of the research baseline.


## Source and requirement consistency pass — 2026-10-12
- Rechecked official Android CallScreeningService/CallRedirectionService references, Google Play call/SMS policy, MeitY's DPDP Rules index and TRAI's TCCCPR amendments index. Updated RESEARCH_REGISTER.md, ANDROID_CALL_ROUTE_DECISION.md and PRIVACY_AND_REGULATORY_RISK_REGISTER.md with source dates, limitations and recheck requirements.
- Clarified that REQ-001–REQ-015 and NFR-001–NFR-010 are stable IDs within the current draft, while their content, priorities and traceability remain unapproved. The core draft and requirements index no longer imply the IDs themselves are awaiting reconciliation.
- README's 49 local Markdown links were checked against the recursive repository tree; all targets exist. This did not validate external URLs or prove factual completeness.
- No interviews, live route tests, provider quotes, legal opinions, benchmarks, load tests or implementation have occurred. Phase 0 remains incomplete and implementation unauthorised.


## External claim traceability increment — 2026-10-12
- Added `docs/research/EXTERNAL_CLAIM_LEDGER.md` with 17 consequential claims, source classes, evidence scope, exclusions, confidence/status and decision impact.
- Indexed the ledger in README and registered it as RES-024 in the research register.
- The ledger explicitly separates official platform/regulator documentation from vendor assertions, store-reported signals and internal scenario assumptions. It does not turn public pricing into an all-in quote or platform API documentation into route feasibility.
- This is desk-research organisation only. It does not claim every external page was re-opened during this pass, nor does it resolve route feasibility, customer demand, provider terms, legal applicability or performance.
- No interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Phase 0 remains incomplete and implementation remains unauthorised.


## Requirement-reference verification increment — 2026-10-12
- Programmatically compared identifiers across CORE_REQUIREMENTS_DRAFT.md, TRACEABILITY_MATRIX.md, UX_SCREEN_INVENTORY.md, THREAT_MODEL.md, PRIVACY_AND_REGULATORY_RISK_REGISTER.md and ACCEPTANCE_THRESHOLD_REGISTER.md.
- Result: all 15 REQ IDs and 10 NFR IDs appear in both the core draft and traceability matrix; all referenced UX/THR/PRIV IDs were found in their source documents; AT-001 and AT-004 references resolve.
- Recorded the result and its limits in BASELINE_CONSISTENCY_AUDIT.md. This confirms identifier presence only, not requirement quality, semantic coverage, acceptance, legal sufficiency or implementation.
- Added EXTERNAL_CLAIM_LEDGER.md and indexed it in README and RESEARCH_REGISTER.md. Existing README links had previously been checked as 49 valid local paths; the newly added ledger file and README link were separately confirmed, but a fresh full recursive-tree scan has not been run.
- Phase 0 remains incomplete. No interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Implementation remains unauthorised.

## Policy-source and conditional-UX reconciliation — 2026-10-12
- Rechecked current Google Play SMS/Call Log policy, Exotel's official business-phone pricing and the DPDP Act commencement Gazette. The external claim ledger now records the specific limitations and avoids equating vendor package prices with an all-in route quote or a Rules index date with the Gazette's commencement-notification date.
- Updated Android route and privacy research with explicit Play policy constraints and commencement caveats. No Play review or legal opinion has been obtained.
- Updated UX screen inventory and wireflow to distinguish conditional contact preferences, optional transcript/audio, route-dependent takeover and user-confirmed tasks from a promised MVP. The core experience should not depend on broad contact-book access by default.
- These are desk-research and document-consistency changes only. No customer interviews, provider outreach, route tests, legal opinions, benchmarks, load tests or implementation occurred. Phase 0 remains incomplete; implementation remains unauthorised.
## Threshold and quote-scenario consistency pass — 2026-10-12
- Aligned `VOICE_AGENT_EVALUATION_PLAN.md` with `ACCEPTANCE_THRESHOLD_REGISTER.md`: the threshold register is now explicitly the source of truth for candidate numeric gates, and unregistered numerical latency/intent/summary/takeover/reconciliation targets were removed from the evaluation table. Proposed route gate AT-002 remains unapproved; latency stays baseline-first under AT-003.
- Aligned `VOICE_PROVIDER_RFP.md` with `WORKLOAD_SCENARIO_BASELINE.md` by making 20k/150k/600k monthly connected minutes the default quote comparison set. The 10k/75k/240k-minute set is explicitly optional and separate, not to be blended with the canonical scenario.
- Updated `BASELINE_CONSISTENCY_AUDIT.md`. No thresholds are owner-approved, no provider has been contacted, no tests or interviews have run, and implementation remains unauthorised.
## Workload arithmetic verification — 2026-10-12
- Independently recomputed monthly minutes, average concurrency, illustrative 10× peaks and cost tables at ₹4/₹7/₹12 plus the ₹6/min public benchmark for the canonical and alternate scenario sets. All reviewed arithmetic matches the stated formulas.
- This does not validate scenario inputs, demand, peak multiplier, route support or applicability of a public vendor price. `BASELINE_CONSISTENCY_AUDIT.md` records the verification and limitations.
## Roadmap gate sequencing update — 2026-10-12
- Corrected a roadmap ambiguity: Phase 0 now contains governed discovery and non-code evidence collection under activity-specific approval; baseline approval is distinct from implementation authorization; Phase 1 implementation requires both the approved baseline and a separate explicit owner authorization; pilot approval is separate again.
- Experiments that require product code remain blocked until implementation authorization. This correction does not approve interviews, route tests, provider outreach, spending, implementation or deployment.
## Product-scope traceability increment — 2026-10-12
- Added draft REQ-016 for account authentication and recovery after identifying that the P0 scope catalogue included these capabilities without a dedicated requirement. Updated the requirements index and traceability matrix.
- Added a SCOPE-001–SCOPE-021 crosswalk to `TRACEABILITY_MATRIX.md` and provisional scope/requirement mappings to `MVP_SCOPE_AND_FEATURE_GATES.md`.
- SCOPE-011 follow-up reminders/tasks and SCOPE-012 caller/contact allowlist/denylist remain unmapped to dedicated requirements and should be deferred or specified before MVP inclusion. All priorities and mappings remain drafts.
- The working set is now REQ-001–REQ-016 and NFR-001–NFR-010. The earlier identifier check covered 15 REQ IDs before REQ-016 was added; a fresh cross-reference check is required after this update. No implementation is authorized.
## Post-crosswalk verification — 2026-10-12
- Re-ran the draft identifier check after adding REQ-016. The core requirements and traceability matrix both contain REQ-001–REQ-016 and NFR-001–NFR-010 with no missing IDs in either direction. All 21 SCOPE IDs from the product catalogue appear in the crosswalk; UX/THR/PRIV references resolve to the source inventories.
- SCOPE-011 and SCOPE-012 have no direct REQ mapping and must be deferred or specified before MVP inclusion; SCOPE-017/018/021 are currently excluded/deferred. The audit records that lexical presence is not semantic completeness or approval.

## Architecture/API/data/security semantic review — 2026-10-12
- Added `docs/governance/ARCHITECTURE_CONTRACT_SEMANTIC_REVIEW.md` to record 12 semantic findings across account/session recovery, account-vs-tenant authority, caller disclosure vs account consent, call/provider-leg state, route disable semantics, deletion completion, usage idempotency, callback validation, exports/support access and observability.
- Clarified the API draft with candidate account-session listing/revocation and recovery operations. Clarified the data model with AccountSession, RecoveryChallenge and a separate CallerDisclosureEvent concept; ConsentRecord now explicitly represents account-holder choices, not proof of third-party caller notice/consent.
- Updated REQ-016 traceability to identify the proposed API/data records and session/recovery abuse tests. These are draft contract clarifications, not an approved schema, provider selection or legal determination.
- Phase 0 remains incomplete. No interviews, provider outreach, route tests, legal opinions, benchmarks, load tests or implementation have occurred. Product implementation remains unauthorised.

- Added `docs/architecture/STATE_AND_EVENT_CONTRACTS_DRAFT.md` with conceptual call/session and provider-leg events, route activation/disable states, distributed deletion states, usage reconciliation, idempotency and callback-validation rules. It explicitly avoids promising provider-specific states or route capabilities.
- The semantic contract review and state/event draft are documentation artifacts only. Route-specific state mapping, auth mechanism, data retention/deletion SLA, billing units and operational owners remain open.


## UX/state semantic reconciliation — 2026-10-12
- Added `UX_STATE_CONTRACT_RECONCILIATION.md` and indexed it from README. Compared UX inventory/wireflows against API and lifecycle contracts.
- Captured lifecycle-backed wording and states for route activation/disable/restoration, live call/takeover, deletion, transcript/audio availability, usage reconciliation, account recovery/session revocation, caller disclosure, conditional follow-up tasks/contact rules and support incidents.
- Added anti-pattern copy examples and future verification scenarios. These are planning artifacts, not evidence that testing occurred.
- UX/state desk review is complete for this pass. Phase 0 and baseline approval remain incomplete; provider/route and legal evidence plus owner decisions remain open. No implementation is authorised.


## Requirement-to-contract coverage audit — 2026-10-12
- Added `REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md` and linked it from README and the traceability matrix. It maps all current REQ-001–REQ-016 draft requirements to API operations, data/state contracts, threat/privacy controls, failure scenarios and future verification evidence.
- Added candidate `SupportedRouteConfiguration`, `ProviderLeg` and `DeletionTarget` records to the conceptual data model so route eligibility, multi-leg call identity and distributed deletion have explicit representations. Usage corrections remain immutable linked events.
- This is a documentation coverage improvement, not release evidence. No P0 candidate is release-ready on documentation alone; route/provider, legal/privacy, pricing/invoice, operations and authentication decisions remain open.
- Phase 0 remains incomplete, PR #1 remains draft/unmerged, and implementation is not authorized.


## API operation coverage refinement — 2026-10-12
- Added proposed API operations for evidence-backed route eligibility, owner correction of supported summary fields, and deletion-status retrieval. These make the API contract better align with REQ-002, REQ-008 and REQ-010.
- The operations remain conceptual and require schema/security review; route evidence, factuality evaluation, legal/privacy policy and deletion lifecycle evidence remain unresolved. No implementation is authorized.


## Deletion and verification reconciliation increment — 2026-10-12

- Added `docs/governance/DELETION_AND_VERIFICATION_RECONCILIATION.md` to connect each data class with candidate deletion destinations, target-level outcomes, role-based ownership, and planned verification evidence for REQ-001–REQ-016, NFR-001–NFR-010 and applicable AT-001–AT-012.
- Reconciled the data inventory, verification strategy, acceptance threshold register, requirement-contract coverage audit and Phase 0 exit map to the new artifact.
- This is documentation-only. Retention periods, deletion SLA, backup expiry, legal exception policy, named owners and candidate target-state enums remain unapproved. Planned tests are not run evidence; AT-008 remains OPEN.
- Phase 0 remains incomplete; product implementation, external experiments and provider outreach remain unauthorized without separate explicit approval. PR #1 remains draft and unmerged.


## Cross-document consistency review increment — 2026-10-12

- Added `docs/governance/FINAL_CROSS_DOCUMENT_CONSISTENCY_REVIEW.md` to record the semantic review across requirements, UX, MVP scope, API/data/state, security/privacy, thresholds and Phase 0 gates.
- Rechecked the REQ-001–REQ-016 and NFR-001–NFR-010 presence in both core requirements and traceability; all are present. Confirmed the SCOPE-001–SCOPE-021 crosswalk exists.
- Corrected the traceability matrix to map conditional UX-006 permissions to REQ-001/REQ-002 and UX-022 notification/permission status to REQ-001/REQ-015. A permission grant or notification is not proof of a verified route.
- SCOPE-011 tasks/reminders and SCOPE-012 contact/caller rules remain intentionally without direct requirement coverage and must stay deferred or receive reviewed requirements before MVP inclusion.
- The review confirms the remaining blockers are evidence/owner decisions, not merely missing documents: customer validation, route feasibility/restoration, comparable provider quotes, qualified jurisdiction-specific legal review, data lifecycle policy, operational ownership and unapproved thresholds.
- Phase 0 remains incomplete; no interviews, route tests, provider outreach, quotes, legal opinions, benchmarks, load tests or implementation were performed. PR #1 remains draft/unmerged; no merge is authorized.


## Acceptance-criteria testability audit — 2026-10-12

- Added `ACCEPTANCE_CRITERIA_TESTABILITY_AUDIT.md` to assess REQ-001–REQ-016 and NFR-001–NFR-010 for observable assertions, negative/partial/timeout/duplicate/out-of-order/revoked/stale-state coverage, missing measurement contracts and future evidence artifacts.
- The audit distinguishes criteria that are behaviorally testable in part from those blocked by provider/route/legal evidence, unapproved thresholds or scope decisions. It does not alter the canonical threshold register or approve requirements.
- Indexed the audit in README and linked it from the traceability matrix. This pass is documentation-only; no tests, interviews, route experiments, provider outreach, benchmarks, load tests, legal review or implementation were performed.
- Phase 0 remains incomplete; product implementation and external activity remain unauthorized without separate explicit approval. PR #1 was merged to `main` as `0c7e6bb86806eec226f263b09b539eb7c269b6e0`. This new audit is on branch `docs/acceptance-testability-audit-2026-10-12`; it is not merged.


## Planned acceptance-test catalogue — 2026-10-13

- Added `docs/quality/PLANNED_ACCEPTANCE_TEST_CATALOG.md` with 48 functional scenarios across REQ-001–REQ-016, 20 non-functional scenarios across NFR-001–NFR-010 and 8 cross-cutting fault/abuse scenarios.
- Each row states preconditions, action/stimulus, expected observable result, planned evidence and current dependency/status. All scenarios are planning-only and NOT RUN.
- Linked the catalogue from README, the traceability matrix and verification strategy. It complements rather than replaces the testability audit and threshold register; no thresholds or requirements were approved.
- PR #2 was merged into `main` as `ef6bb0c62d9c97f29dd2d07d3a21c6d281763fb5`. The new catalogue is on branch `docs/acceptance-test-catalog-2026-10-13`; it is not merged.
- Phase 0 remains incomplete. No product tests, interviews, route tests, provider outreach, legal review, benchmarks, load tests or implementation were performed. Implementation remains unauthorized.


## Business phone assistant direction increment — 2026-10-13
- Recorded the owner's direction to make the configurable AI business phone assistant the primary MVP hypothesis and move personal call-assistant mode to a later candidate.
- Added `docs/discovery/BUSINESS_PHONE_ASSISTANT_PRODUCT_DIRECTION.md` defining actor vocabulary, business-admin and caller journeys, constrained workflow building blocks, product-complaint example, missed-call outcome semantics, dashboard information architecture, trust invariants and discovery gates.
- This is a direction update, not demand validation or approval of detailed MVP requirements. Call routing, provider/event coverage, integrations, legal/privacy policy, unit economics and owner approval of the full baseline remain open.
- PR #3's planned acceptance-test catalogue is now merged to `main` as `ac3801d15c55e71d2c09609e0404c99fc12cfa53`; all catalogue scenarios remain planning-only and NOT RUN.
- Documentation-only change. No implementation, customer interviews, route tests, provider outreach, legal opinions, benchmarks or load tests were performed. Product implementation remains unauthorized.



## Business assistant requirement/acceptance gap audit — 2026-10-13
- Mapped REQ-001–REQ-016 and NFR-001–NFR-010 against the business phone assistant hypothesis; documented semantic gaps in workflow lifecycle/versioning, organization membership/roles, caller verification, call outcome/event provenance, missed-call visibility, connector writes, dashboard metric contracts, business workload and data lifecycle.
- Added 18 supplemental BPA scenarios to the planned acceptance catalogue. The original 68 scenarios and the 18 supplemental scenarios are all NOT RUN; this work is documentation-only.
- Requirements, scope, thresholds and provider/integration choices remain unapproved. Phase 0 remains incomplete and product implementation remains unauthorized.


## Business assistant domain contract draft — 2026-10-13

- Added `docs/architecture/BUSINESS_ASSISTANT_DOMAIN_CONTRACT_DRAFT.md` to align organization/membership, workflow lifecycle/version pinning, caller verification, call observation/outcomes, connector action results and dashboard metric provenance.
- Linked the conceptual contract from the API/data/state, threat-model, UX and traceability drafts. These are documentation cross-references, not approved endpoints, tables, events, roles, requirements or screens.
- Organization role policy, workflow schema, caller verification, provider event coverage, ticket connector, data lifecycle, thresholds and initial workflow remain open. Phase 0 is incomplete; all original and BPA acceptance scenarios remain NOT RUN; implementation remains unauthorized.


## Business assistant UX wireflows draft — 2026-10-13

- Added `docs/discovery/BUSINESS_ASSISTANT_UX_WIREFLOWS_DRAFT.md` with textual flows for organization/route onboarding, constrained workflow validation and publication, caller interaction, call inbox/detail, connector outcomes and high-impact controls.
- The flows preserve unknown/unobserved states and distinguish workflow pause from route disable; they do not promise missed-call capture, handoff, recording or ticket creation without evidence and approval.
- No user research or usability testing occurred. UX, initial workflow, role policy, route/provider, privacy/legal decisions and feature scope remain open; Phase 0 remains incomplete and product implementation remains unauthorized.



## Business assistant requirements addendum — 2026-10-15
- Added a proposed, unapproved REQ-017–REQ-022 addendum for organization authorization, constrained workflow lifecycle/version binding, caller verification, evidence-backed call outcomes, authoritative connector actions and dashboard metric provenance.
- Mapped proposed requirements to BPA-001–BPA-018 in the traceability matrix. All scenarios remain NOT RUN; requirement IDs, priorities and scope remain proposed.
- The inherited core requirement draft was explicitly labelled as personal-assistant-origin material pending semantic review. This does not approve or silently repurpose any existing requirement.
- Phase 0 remains incomplete. Product implementation remains unauthorized.



## Business-first scope reconciliation — 2026-10-15
- Added proposed SCOPE-022–SCOPE-028 for organization authorization, constrained business workflows, caller verification, evidence-backed call outcomes, typed connector actions, dashboard metrics and conditional human handoff.
- Marked SCOPE-002/003 personal profile/context as legacy/secondary-mode candidates, deferred for the primary business assistant hypothesis; they are not substitutes for workflow configuration.
- Added a business-first MVP candidate matrix mapped to existing and proposed requirements. No feature, route, integration, caller verification method or threshold is approved by this documentation update.
- All BPA scenarios remain NOT RUN; Phase 0 remains incomplete; product implementation remains unauthorized.



## Business-first UX inventory reconciliation — 2026-10-15
- Added proposed UX-023–UX-033 for organization membership/roles, constrained workflow lifecycle, business route state, call inbox/detail, connector reconciliation, dashboard metrics, caller verification and action outcomes.
- Explicitly labelled UX_WIREFLOW_SPEC.md as inherited personal-assistant material; BUSINESS_ASSISTANT_UX_WIREFLOWS_DRAFT.md remains the candidate business-flow reference.
- Form factor, screen inclusion, navigation, route, connector and first workflow remain undecided. No customer UX validation has occurred.
- All screen IDs and flows remain draft; Phase 0 remains incomplete and product implementation remains unauthorized.


## Business assistant architecture contract alignment — 2026-10-15
- Added conceptual mappings for proposed REQ-017–REQ-022 across API resource families, candidate data entities, state/event contracts, business domain vocabulary and threat areas.
- API schemas, entities, states, event names and threats remain drafts; no provider route or connector was selected, and no tests were run.
- All BPA scenarios remain NOT RUN; Phase 0 remains incomplete and product implementation remains unauthorized.



## Decision pack and roadmap business-first reconciliation — 2026-10-15
- Updated owner decision items and decision log to reflect the business phone assistant as the primary hypothesis, while leaving segment, workflow, route, form factor, connector and metric semantics open.
- Reconciled Phase 1 roadmap language to the business assistant and added evidence gates for first workflow, route/event coverage, workflow lifecycle, caller verification, connector and dashboard metrics.
- No product decision was marked approved from these desk-only edits. Phase 0 remains incomplete; product implementation remains unauthorized.



## Business customer-validation materials reconciliation — 2026-10-15
- Reframed the customer interview pack, validation plan and GTM experiment hypotheses around business decision-makers, front-line call handlers and bounded inbound workflows.
- Added a market-demand note distinguishing consumer category signals from unvalidated B2B demand and expanded the competitor matrix's comparison boundaries across consumer assistants, voice-agent platforms and business telephony vendors.
- No interviews, outreach, campaigns, route tests, provider quotes or spend occurred. All fieldwork remains subject to separate owner approval; Phase 0 remains incomplete and implementation remains unauthorized.
