# Handover Guide

Read README, CURRENT_STATE, PROJECT_CHARTER, DECISION_LOG, DISCOVERY_PLAN, RESEARCH_REGISTER, REQUIREMENTS_INDEX, CORE_REQUIREMENTS_DRAFT, TRACEABILITY_MATRIX, ARCHITECTURE_PRINCIPLES, SYSTEM_ARCHITECTURE_OPTIONS, API_CONTRACT_DRAFT, DATA_MODEL_DRAFT, ROADMAP, PRICING_AND_UNIT_ECONOMICS, COMPETITIVE_ANALYSIS, TELEPHONY_FEASIBILITY, PRIVACY_AND_REGULATORY_RISK_REGISTER, OPEN_SOURCE_AND_PROVIDER_EVALUATION, VOICE_STACK_CANDIDATE_REVIEW, THREAT_MODEL, DATA_INVENTORY_AND_LIFECYCLE, UX_SCREEN_INVENTORY, CUSTOMER_VALIDATION_PLAN and VERIFICATION_AND_TEST_STRATEGY first.

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

## Current deliverable state (2026-10-11)

A broad discovery scaffold and first draft set has been pushed to GitHub. It includes competitor analysis, telephony feasibility, pricing/capacity scenarios, privacy/security issue-spotting, product scope, UX inventory, positioning hypotheses, architecture options, API/data model drafts, core requirement drafts, traceability and test strategy. These are not a complete approved baseline. No interviews, carrier tests, written provider quotes, legal opinion, load tests or implementation have been performed.

## Handover checklist
Update CURRENT_STATE, DECISION_LOG, research and requirement indexes; list completed work and source links; list unresolved risks/questions, owners and triggers; identify contradictions; state phase approvals; explicitly state whether implementation is authorised.