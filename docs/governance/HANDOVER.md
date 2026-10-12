# Handover Guide

Start with README.md as the repository index, then read CURRENT_STATE.md, PROJECT_CHARTER.md, DECISION_LOG.md, DISCOVERY_PLAN.md, RESEARCH_REGISTER.md and ROADMAP.md. Follow the linked requirement, architecture, business, research, security, UX and quality documents relevant to the workstream. Important current documents include CORE_REQUIREMENTS_DRAFT.md, TRACEABILITY_MATRIX.md, MARKET_DEMAND_AND_SEGMENTATION.md, COMPETITIVE_ANALYSIS.md, TELEPHONY_FEASIBILITY.md, PRIVACY_AND_REGULATORY_RISK_REGISTER.md, OPEN_SOURCE_AND_PROVIDER_EVALUATION.md, VOICE_STACK_CANDIDATE_REVIEW.md, SYSTEM_ARCHITECTURE_OPTIONS.md, API_CONTRACT_DRAFT.md, DATA_MODEL_DRAFT.md, THREAT_MODEL.md, DATA_INVENTORY_AND_LIFECYCLE.md, UX_SCREEN_INVENTORY.md, CUSTOMER_VALIDATION_PLAN.md and VERIFICATION_AND_TEST_STRATEGY.md.

## Mission
Act as lead architect / senior principal engineer / engineering orchestrator for discovery and specifications. The owner requires comprehensive documents before code. Do not assume authority to approve business decisions.

## Operating contract
- Prefer primary sources: official docs, API references, pricing, terms, licence text and regulator publications.
- For important claims, record URL, source owner, access date, what it establishes, confidence and limitations.
- Separate verified facts, vendor claims, third-party reports, estimates, inferences and hypotheses.
- Validate provider/account/region/plan/carrier limits before claiming a capability.
- Include telephony, speech, model, storage, network, retries, monitoring, support, taxes and payment fees in cost analysis.
- Do not equate 10,000 registered users with 10,000 concurrent callers.
- Never allow client-provided arbitrary URLs, SQL, executable code or unbounded tool permissions. Use trusted server-side connectors and scoped domain APIs.
- Do not query domain databases directly. Do not store secrets or real customer call content in docs/tests.
- Keep product implementation blocked until explicit owner approval.

## Decision statuses
PROPOSED, RESEARCH_REQUIRED, EXPERIMENT_REQUIRED, DECIDED, APPROVED, DEFERRED. A recommendation is not an owner approval.

## Requirement quality
Each requirement needs stable ID, status, priority, evidence/rationale, actors, preconditions, main/alternate/failure flows, testable acceptance criteria, security/privacy implications, dependencies, verification strategy, observability, trace links and open questions.

## Current deliverable state (2026-10-12)

A broad discovery scaffold and first draft set has been pushed to GitHub. It includes competitor analysis, telephony feasibility, pricing/capacity scenarios, privacy/security issue-spotting, product scope, UX inventory and wireflows, positioning and GTM hypotheses, architecture options, API/data model drafts, core requirement drafts, traceability, test strategy and voice-agent evaluation gates. Latest additions include Android call-route constraints, a provider RFP/scorecard, capability governance, GTM experiments and a provider pricing evidence review. Public pricing is not route-specific proof: Ringg's ₹6/connected-minute bundle is not confirmed for consumer forwarding; Exotel lists voice streaming separately and says carrier forwarding charges are separate. See docs/research/PROVIDER_PRICING_EVIDENCE.md. These are not a complete approved baseline. No interviews, carrier tests, written provider quotes, legal opinion, load tests or implementation have been performed.

## Handover checklist
Update CURRENT_STATE, DECISION_LOG, research and requirement indexes; list completed work and source links; list unresolved risks/questions, owners and triggers; identify contradictions; state phase approvals; explicitly state whether implementation is authorised.

## Latest increment — baseline consistency audit (2026-10-11)
- Read the current requirements draft, traceability matrix, API contract, data model, threat model, privacy/data inventory, UX screen inventory/wireflows, capability governance, capacity model, pricing models and decision log.
- Added `docs/governance/BASELINE_CONSISTENCY_AUDIT.md` with 12 P0/P1 gaps and a recommended order of resolution.
- Important reconciliation issue: `COST_SCENARIO_MODEL.md` uses 10k/75k/240k monthly-minute scenarios, while `CAPACITY_AND_SCALE_MODEL.md` and `PRICING_AND_UNIT_ECONOMICS.md` use 20k/150k/600k. These are based on different assumptions, not necessarily a factual contradiction, but a canonical shared workload table is needed before decisions.
- Price assumptions (₹4/₹7/₹12), a public ₹6/min anchor and future written quotes must remain clearly distinct.
- The audit is not an approval. Route tests, customer interviews, written quotes, legal review and final owner sign-off remain outstanding. Implementation is not authorised.

## Latest increment — workload and lifecycle normalization (2026-10-11)
- Added `docs/architecture/WORKLOAD_SCENARIO_BASELINE.md` to define one shared proposed low/base/high workload set for capacity and pricing references. Values remain assumptions; the 10k/75k/240k-minute cost sensitivity remains a separate alternate set.
- Linked the workload baseline from `CAPACITY_AND_SCALE_MODEL.md`, `PRICING_AND_UNIT_ECONOMICS.md` and `COST_SCENARIO_MODEL.md`.
- Normalized `CORE_REQUIREMENTS_DRAFT.md` status to DRAFT because formal review has not started.
- Added the baseline consistency audit. Neither the shared workload assumptions nor any requirement is owner-approved; implementation remains blocked.


## Latest increment — acceptance threshold register (2026-10-12)
- Added `docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md` with proposed starting points, evidence requirements and explicit open items for owner review.
- Proposed examples include disable access within two dashboard actions, 30 controlled repetitions per supported route configuration with a 95% exploratory success target, and 500 ms cancellation as a candidate to validate against provider/media semantics. These are not approved release criteria.
- Zero-tolerance candidate gates cover duplicate billing, cross-tenant access and unauthorised tool actions. Numeric latency, deletion, availability/recovery, capacity and summary-quality thresholds remain open pending evidence.
- Linked the register from README and REQUIREMENTS_INDEX.md. REQ-001 and REQ-006 now reference proposed AT-001/AT-004 values in the canonical requirements; NFR target decisions and evidence-dependent values remain open.
- No interviews, route tests, provider quotes, legal opinion, benchmarks or implementation have been performed. Product implementation remains unauthorised.


## Owner decision pack increment — 2026-10-12
- Added `docs/governance/OWNER_DECISION_PACK.md` to consolidate ten discovery decisions, their evidence needs, blocked dependencies and the explicit implementation gate.
- Linked the decision pack from README. It records the current hypotheses without treating them as approved and lists evidence not yet collected.
- Next evidence-led work should prioritize customer interviews, controlled call-route feasibility, comparable written provider quotes and jurisdiction-specific legal review. Experiments require owner approval; product code remains unauthorised.


## Phase 0 evidence workbook increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md` with private participant-record guidance, route-test capture rows, provider quote comparison and evidence-to-decision logging.
- This prepares fieldwork; it does not claim that interviews, telephony tests or provider outreach have occurred. Owner approval and safety checks are required before experiments.
- README now indexes the workbook. Implementation remains unauthorised.


## Latest increment — Phase 0 experiment approval checklist (2026-10-12)
- Added `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md` to require an explicit owner decision for each experiment scope before fieldwork, route testing, provider outreach or participant-based UX validation.
- Approval records cover hypothesis, scope, consent, data, safety/reversibility, spend ceiling, success and stop criteria, evidence hygiene and post-test review. The checklist itself does not grant approval.
- Indexed from README and referenced by ROADMAP.md and CURRENT_STATE.md. No fieldwork or implementation is authorised by this documentation increment.


## Latest increment — Phase 0 exit criteria and evidence map (2026-10-12)
- Added `docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md` to consolidate 20 gates, required evidence, current status and explicit exit conditions.
- Use it as the single review index for what can be completed by desk research, what requires separately approved fieldwork, what is blocked by external evidence, and what requires owner approval.
- Phase 0 remains incomplete; the map does not approve fieldwork, baseline or implementation.


## Latest increment — Phase 0 residual risk register (2026-10-12)
- Added `docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md` covering route feasibility, user control, demand, economics, legal/privacy, AI safety, reliability, capacity, deletion, brand, dependency and operational risks.
- Use it with the exit map and owner decision pack. It is not a quantitative risk assessment, proof of implemented controls or owner acceptance of residual risk.

## Latest continuation — traceability and roadmap gate reconciliation (2026-10-12)
- Corrected `docs/roadmap/ROADMAP.md`: Phase 0 includes governed discovery and non-code evidence collection under activity-specific approval; baseline approval, implementation authorization and pilot approval are separate gates. Product code and code-dependent experiments remain blocked until explicit implementation authorization.
- Added draft REQ-016 for account authentication/recovery after discovering the P0 product-scope catalogue had no dedicated requirement for SCOPE-001. Updated `REQUIREMENTS_INDEX.md`, `TRACEABILITY_MATRIX.md` and `MVP_SCOPE_AND_FEATURE_GATES.md` with a provisional scope-to-requirement crosswalk.
- SCOPE-011 (follow-up tasks/reminders) and SCOPE-012 (caller/contact allowlist/denylist) have no dedicated requirement coverage; defer them from MVP or draft requirements before inclusion. SCOPE-017/018/021 are explicitly excluded/deferred in the crosswalk.
- Reconciled `VOICE_AGENT_EVALUATION_PLAN.md` with `ACCEPTANCE_THRESHOLD_REGISTER.md`: the register is the single source for candidate numeric thresholds; removed unregistered numeric latency/intent/summary/takeover/reconciliation targets. Aligned `VOICE_PROVIDER_RFP.md` and `PROVIDER_PRICING_EVIDENCE.md` to the canonical 20k/150k/600k-minute quote scenarios, keeping 10k/75k/240k as a separate optional sensitivity set.
- Recomputed workload and cost scenario arithmetic; values match the documented formulas. Re-ran lexical reference checks: REQ-001–REQ-016 and NFR-001–NFR-010 appear in both core requirements and traceability; all 21 SCOPE IDs appear in the crosswalk; referenced UX/THR/PRIV IDs resolve. These checks do not establish semantic completeness or approval.
- At the time this note was first appended, main was `23dfad1648bfff56ba5fcd7707789852b3e967af`; subsequent reconciliation commits are recorded in the latest continuation entry below.
- Phase 0 remains incomplete. No interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Do not perform these activities without scope-specific approval; do not implement without separate explicit owner authorization.

## Latest verification follow-up — 2026-10-12
- Re-ran requirement and scope reference checks after adding REQ-016: REQ-001–REQ-016 and NFR-001–NFR-010 match between the core draft and traceability matrix; all 21 SCOPE IDs are present in the crosswalk; referenced UX/THR/PRIV IDs resolve.
- Checked local Markdown links in README against the current recursive repository tree: all 50 local targets exist. Checked the modified roadmap's links and found no broken local targets.
- Checked Markdown table column consistency in MVP_SCOPE_AND_FEATURE_GATES.md, TRACEABILITY_MATRIX.md and CORE_REQUIREMENTS_DRAFT.md. A stale three-column separator in the MVP scope tables was found and corrected; rerun found no table-row column mismatches in those files.
- Arithmetic for canonical and alternate workload/cost scenarios was recomputed and matches the documented formulas. Provider quote scenarios and evaluation thresholds have been reconciled to their canonical registers.
- Latest verified main before this handover update: `f4a53bc351ab2f94ba52a8dfe5187983d8a6eb14`. Phase 0 remains incomplete; no interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Implementation remains unauthorised.

## Latest continuation — architecture/API/data/security semantic review (2026-10-12)
- Added `docs/governance/ARCHITECTURE_CONTRACT_SEMANTIC_REVIEW.md` with 12 P0/P1 findings and a recommended desk-only resolution order. The main unresolved themes are account-vs-tenant authority, call/provider-leg state, verified route disable semantics, distributed deletion completion, and canonical usage-event idempotency.
- Clarified `docs/architecture/API_CONTRACT_DRAFT.md` with account-session listing/revocation and account-recovery operations, and the distinction between account-holder choices and caller-facing disclosure evidence.
- Clarified `docs/architecture/DATA_MODEL_DRAFT.md` with AccountSession, RecoveryChallenge and CallerDisclosureEvent concepts. These are candidate conceptual entities, not approved schema decisions. Updated REQ-016 in the traceability matrix to point to the new contract concepts.
- Indexed the semantic review in README and recorded the increment in CURRENT_STATE.
- Remaining contract decisions must stay open where they depend on the route, provider, jurisdiction or owner choices. No provider-specific call state machine, retention period, authentication mechanism, endpoint schema or threshold is approved by this review.
- Phase 0 remains incomplete; no interviews, provider outreach, route tests, legal opinions, benchmarks, load tests or implementation have occurred. Do not treat documentation work as permission for those activities. Implementation remains unauthorised.

## State/event contract follow-up — 2026-10-12
- Added `docs/architecture/STATE_AND_EVENT_CONTRACTS_DRAFT.md` to spell out conceptual lifecycle states for call sessions/provider legs, routing, deletion and usage reconciliation. It covers duplicate/out-of-order events, verified-vs-requested status, immutable usage adjustments and safe uncertainty.
- Indexed the draft from README and linked it from the semantic review. These are provider-neutral candidates only; they must be mapped against actual route/provider contracts before implementation and do not prove route feasibility.
- Revalidated modified Markdown table column consistency after the account/session and caller-disclosure changes: no row/column mismatches were found. REQ-001–REQ-016 remain present in traceability, and the semantic review is indexed from README.
- Phase 0 remains incomplete; no interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Product implementation remains unauthorised.

## P0 contract coverage follow-up — 2026-10-12
A requirement-by-requirement review finds no P0 candidate release-ready on documentation alone. REQ-001, REQ-003, REQ-005, REQ-008, REQ-009, REQ-011, REQ-014, REQ-015 and REQ-016 have partial contract coverage. REQ-002, REQ-004, REQ-006 and REQ-010 remain materially blocked by route/provider evidence or legal review. REQ-007 remains conditional on a verified route. Key failure scenarios include duplicate/out-of-order callbacks, route disable without verified restoration, partial provider deletion, usage/invoice mismatch, cross-account export access, recovery replay and privacy-sensitive logging.

The coverage review is an audit conclusion, not an approval. The full draft contract references remain in CORE_REQUIREMENTS_DRAFT.md, TRACEABILITY_MATRIX.md, API_CONTRACT_DRAFT.md, DATA_MODEL_DRAFT.md, THREAT_MODEL.md, DATA_INVENTORY_AND_LIFECYCLE.md and STATE_AND_EVENT_CONTRACTS_DRAFT.md. Phase 0 remains incomplete; implementation remains unauthorised.


## UX/state contract reconciliation — 2026-10-12
- Added `docs/governance/UX_STATE_CONTRACT_RECONCILIATION.md` after comparing the UX screen inventory and textual wireflows with the API and lifecycle state drafts.
- Captured required user-facing distinctions for route verification/disable/restoration, live call and provider-leg status, takeover, distributed deletion, artifact availability, usage reconciliation, account recovery/session revocation, caller disclosure, follow-up tasks, contact permissions and support states.
- Added prohibited copy patterns and future verification scenarios for stale/conflicting events, delayed confirmations, partial deletion, late usage corrections, recovery replay and stale sessions. These scenarios are planning requirements only; no tests were executed.
- The UX drafts are generally directionally aligned, but final screen copy and flow states must use authoritative state and must not treat request acceptance as completion. Conditional features remain gated; SCOPE-011 and SCOPE-012 still need a dedicated requirement or explicit MVP deferral.
- Phase 0 remains incomplete. No interviews, provider outreach, live route tests, spending, legal opinions, benchmarks, load tests or implementation were performed by this increment. Do not merge the draft PR or begin implementation without the separately required authorization.


## Requirement-to-contract coverage audit — 2026-10-12
- Added `docs/governance/REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md`, indexed it from README and linked it from `TRACEABILITY_MATRIX.md`. It maps REQ-001–REQ-016 to proposed API operations, data/state contracts, threat/privacy controls, failure scenarios, future verification artifacts and unresolved blockers.
- Updated traceability references for routing configuration, provider-leg lifecycle and privacy/deletion records.
- Aligned the conceptual data model with the state/event contract by adding candidate `SupportedRouteConfiguration`, `ProviderLeg` and `DeletionTarget` entities and clarifying immutable usage adjustments. These remain draft concepts, not approved schemas.
- The audit finds no P0 candidate release-ready on documentation alone. Route/provider evidence, legal/privacy review, invoice reconciliation, operational runbooks and auth-policy decisions remain open. The verification scenarios are planned only; no tests were run.
- Phase 0 remains incomplete. No interviews, provider outreach, live route tests, spending, legal opinions, benchmarks, load tests or implementation were performed or authorized by this documentation pass. PR #1 remains draft and unmerged.


## API operation coverage refinement — 2026-10-12
- Added explicit proposed operations to `API_CONTRACT_DRAFT.md` for listing/checking evidence-backed supported route options, correcting supported summary fields with audit/version semantics, and retrieving deletion status with per-target completion distinctions.
- These additions close naming/representation gaps found during the requirement-to-contract audit; they do not prove route support or approve endpoint schemas. The coverage audit now records these as proposed operations.
- Phase 0 remains incomplete; PR #1 remains draft and unmerged. No implementation or external activity is authorized.


## Deletion and verification reconciliation increment — 2026-10-12

- Added `DELETION_AND_VERIFICATION_RECONCILIATION.md`: data-class-to-target inventory, candidate request/target outcomes, role-based operational accountability, and a full REQ-001–REQ-016 / NFR-001–NFR-010 / AT-001–AT-012 future-verification crosswalk.
- Linked the reconciliation from README, the data inventory, verification strategy, acceptance threshold register, requirement-contract coverage audit and Phase 0 exit map.
- Explicitly left retention durations, deletion SLA, backup expiry, legal exceptions, named operational owners and candidate target enums unapproved. Unknown destinations block a full-deletion claim.
- Verification artifacts are plans only. No tests, deletion exercise, restore drill, route tests, interviews, provider outreach, legal opinions or implementation were performed by this pass. AT-008 remains OPEN and Phase 0 remains incomplete.
- PR #1 remains draft/unmerged. Do not merge without explicit owner instruction; product implementation and external experiments remain unauthorized.


## Cross-document consistency review increment — 2026-10-12

- Added `FINAL_CROSS_DOCUMENT_CONSISTENCY_REVIEW.md` and indexed it from README.
- Verified presence of REQ-001–REQ-016 and NFR-001–NFR-010 in both core requirements and traceability, plus SCOPE-001–SCOPE-021 in the scope crosswalk.
- Added explicit conditional traceability for UX-006 (platform permissions) and UX-022 (notifications/status). The matrix warns that permission grants/notifications do not prove route eligibility or verified routing.
- SCOPE-011/SCOPE-012 remain unassigned to dedicated requirements and must not silently enter MVP.
- Remaining blockers: customer/problem evidence; route/provider feasibility and restoration; comparable quotes/invoice costs; jurisdiction-specific legal/privacy review; approved retention/deletion/backup policy; operational owners/runbooks; measurable, owner-approved thresholds.
- Review is documentation-only, not independent external approval or release evidence. Phase 0 remains incomplete and implementation is not authorized. PR #1 remains draft/unmerged; merge requires explicit owner instruction.
