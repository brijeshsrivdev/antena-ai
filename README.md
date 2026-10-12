# Antena AI — Product Discovery Baseline

> Working repository name only. Commercial brand is not approved.

This repository is for discovery and specification of a reusable AI voice platform. The current direction is to investigate a MyEqual.ai-style personal AI call assistant first, then add trusted domain-specific capabilities, initially hospitality.

**Phase: discovery and documentation only. Product implementation is not authorised.**

## Start here
- [Project charter](docs/governance/PROJECT_CHARTER.md)
- [Current state](docs/governance/CURRENT_STATE.md)
- [Baseline consistency and readiness audit](docs/governance/BASELINE_CONSISTENCY_AUDIT.md)
- [Architecture/API/data/security semantic review — findings open, baseline not approved](docs/governance/ARCHITECTURE_CONTRACT_SEMANTIC_REVIEW.md)
- [Phase 0 exit criteria and evidence map — incomplete, owner review required](docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md)
- [Phase 0 residual risk register — open risks, evidence and stop conditions](docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md)
- [Handover guide](docs/governance/HANDOVER.md)
- [Discovery plan](docs/discovery/DISCOVERY_PLAN.md)
- [Customer validation plan](docs/discovery/CUSTOMER_VALIDATION_PLAN.md)
- [Customer interview pack](docs/discovery/CUSTOMER_INTERVIEW_PACK.md)
- [Phase 0 evidence workbook](docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md)
- [Phase 0 experiment approval checklist — approval required before fieldwork](docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md)
- [Proposed product scope and feature catalogue](docs/discovery/PRODUCT_SCOPE_AND_FEATURE_CATALOG.md)
- [MVP scope and feature gates](docs/discovery/MVP_SCOPE_AND_FEATURE_GATES.md)
- [UX screen inventory](docs/discovery/UX_SCREEN_INVENTORY.md)
- [UX wireflow specification](docs/discovery/UX_WIREFLOW_SPEC.md)
- [Decision log](docs/governance/DECISION_LOG.md)
- [Owner decision pack — discovery choices and gates](docs/governance/OWNER_DECISION_PACK.md)
- [Research register](docs/research/RESEARCH_REGISTER.md)
- [External claim ledger — sources, limitations and decision impact](docs/research/EXTERNAL_CLAIM_LEDGER.md)
- [Competitive analysis — Equal AI](docs/research/COMPETITIVE_ANALYSIS.md)
- [Competitor matrix](docs/research/COMPETITOR_MATRIX.md)
- [Market demand and segmentation](docs/research/MARKET_DEMAND_AND_SEGMENTATION.md)
- [Telephony feasibility](docs/research/TELEPHONY_FEASIBILITY.md)
- [Telephony validation protocol](docs/research/TELEPHONY_VALIDATION_PROTOCOL.md)
- [Requirements index](docs/requirements/REQUIREMENTS_INDEX.md)
- [Core requirements draft](docs/requirements/CORE_REQUIREMENTS_DRAFT.md)
- [Requirements traceability matrix](docs/requirements/TRACEABILITY_MATRIX.md)
- [Acceptance threshold register — proposed, owner review required](docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md)
- [Architecture principles](docs/architecture/ARCHITECTURE_PRINCIPLES.md)
- [Roadmap](docs/roadmap/ROADMAP.md)
- [Pricing and unit economics](docs/business/PRICING_AND_UNIT_ECONOMICS.md)
- [Voice cost scenario model](docs/business/COST_SCENARIO_MODEL.md)
- [Privacy and regulatory risk register](docs/research/PRIVACY_AND_REGULATORY_RISK_REGISTER.md)
- [Open-source/provider evaluation framework](docs/research/OPEN_SOURCE_AND_PROVIDER_EVALUATION.md)
- [Voice-stack candidate review](docs/research/VOICE_STACK_CANDIDATE_REVIEW.md)
- [Initial threat model](docs/security/THREAT_MODEL.md)
- [Data inventory and lifecycle](docs/security/DATA_INVENTORY_AND_LIFECYCLE.md)
- [Verification and test strategy](docs/quality/VERIFICATION_AND_TEST_STRATEGY.md)
- [Positioning and go-to-market hypotheses](docs/business/POSITIONING_AND_GO_TO_MARKET.md)
- [System architecture options](docs/architecture/SYSTEM_ARCHITECTURE_OPTIONS.md)
- [API contract draft](docs/architecture/API_CONTRACT_DRAFT.md)
- [Data model draft](docs/architecture/DATA_MODEL_DRAFT.md)
- [Capacity and scale model](docs/architecture/CAPACITY_AND_SCALE_MODEL.md)
- [Shared workload scenario baseline](docs/architecture/WORKLOAD_SCENARIO_BASELINE.md)

## Latest discovery additions
- [Android call route constraints and decision gates](docs/research/ANDROID_CALL_ROUTE_DECISION.md)
- [Voice provider RFP and evaluation scorecard](docs/research/VOICE_PROVIDER_RFP.md)
- [India voice-provider pricing evidence](docs/research/PROVIDER_PRICING_EVIDENCE.md)
- [AI profile capability governance](docs/architecture/CAPABILITY_GOVERNANCE.md)
- [Go-to-market experiment plan](docs/business/GTM_EXPERIMENT_PLAN.md)

- [Voice-agent evaluation and release gates](docs/quality/VOICE_AGENT_EVALUATION_PLAN.md)

## Non-negotiable rules
- No product code, infrastructure code, migrations, or deployable prototypes until the owner explicitly approves the documented baseline.
- Research claims must be sourced and distinguish verified facts, vendor claims, estimates, assumptions and hypotheses.
- Use trusted server-configured domain connectors and domain APIs; no direct domain database access and no client-supplied arbitrary backend URLs.
- Evaluate open-source dependencies for licence, maintenance, security, total cost and lock-in.
- Treat 10,000 users as a target requiring workload modelling, not as a concurrency specification.
- Keep handover and current-state documents up to date.

## Decision statuses
PROPOSED, RESEARCH_REQUIRED, EXPERIMENT_REQUIRED, DECIDED, APPROVED, DEFERRED.
