# Antena AI — Product Discovery Baseline

> Working repository name only. Commercial brand is not approved.

This repository is for discovery and specification of a reusable AI voice platform. The current direction is to investigate a MyEqual.ai-style personal AI call assistant first, then add trusted domain-specific capabilities, initially hospitality.

**Phase: discovery and documentation only. Product implementation is not authorised.**

## Start here
- [Project charter](docs/governance/PROJECT_CHARTER.md)
- [Current state](docs/governance/CURRENT_STATE.md)
- [Handover guide](docs/governance/HANDOVER.md)
- [Discovery plan](docs/discovery/DISCOVERY_PLAN.md)
- [Customer validation plan](docs/discovery/CUSTOMER_VALIDATION_PLAN.md)
- [Proposed product scope and feature catalogue](docs/discovery/PRODUCT_SCOPE_AND_FEATURE_CATALOG.md)
- [UX screen inventory](docs/discovery/UX_SCREEN_INVENTORY.md)
- [Decision log](docs/governance/DECISION_LOG.md)
- [Research register](docs/research/RESEARCH_REGISTER.md)
- [Competitive analysis — Equal AI](docs/research/COMPETITIVE_ANALYSIS.md)
- [Telephony feasibility](docs/research/TELEPHONY_FEASIBILITY.md)
- [Requirements index](docs/requirements/REQUIREMENTS_INDEX.md)
- [Architecture principles](docs/architecture/ARCHITECTURE_PRINCIPLES.md)
- [Roadmap](docs/roadmap/ROADMAP.md)
- [Pricing and unit economics](docs/business/PRICING_AND_UNIT_ECONOMICS.md)
- [Privacy and regulatory risk register](docs/research/PRIVACY_AND_REGULATORY_RISK_REGISTER.md)
- [Open-source/provider evaluation framework](docs/research/OPEN_SOURCE_AND_PROVIDER_EVALUATION.md)
- [Positioning and go-to-market hypotheses](docs/business/POSITIONING_AND_GO_TO_MARKET.md)
- [10,000-user capacity model](docs/architecture/CAPACITY_AND_SCALE_MODEL.md)

## Non-negotiable rules
- No product code, infrastructure code, migrations, or deployable prototypes until the owner explicitly approves the documented baseline.
- Research claims must be sourced and distinguish verified facts, vendor claims, estimates, assumptions and hypotheses.
- Use trusted server-configured domain connectors and domain APIs; no direct domain database access and no client-supplied arbitrary backend URLs.
- Evaluate open-source dependencies for licence, maintenance, security, total cost and lock-in.
- Treat 10,000 users as a target requiring workload modelling, not as a concurrency specification.
- Keep handover and current-state documents up to date.

## Decision statuses
PROPOSED, RESEARCH_REQUIRED, EXPERIMENT_REQUIRED, DECIDED, APPROVED, DEFERRED.
