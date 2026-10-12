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
- Latest verified main commit before this handover update: `23dfad1648bfff56ba5fcd7707789852b3e967af`. The next commit will update this handover record.
- Phase 0 remains incomplete. No interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Do not perform these activities without scope-specific approval; do not implement without separate explicit owner authorization.