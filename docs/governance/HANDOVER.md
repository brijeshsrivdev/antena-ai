# Handover Guide

Read README, CURRENT_STATE, PROJECT_CHARTER, DECISION_LOG, DISCOVERY_PLAN, RESEARCH_REGISTER, REQUIREMENTS_INDEX, ARCHITECTURE_PRINCIPLES, ROADMAP and PRICING_AND_UNIT_ECONOMICS first.

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

## Handover checklist
Update CURRENT_STATE, DECISION_LOG, research and requirement indexes; list completed work and source links; list unresolved risks/questions, owners and triggers; identify contradictions; state phase approvals; explicitly state whether implementation is authorised.