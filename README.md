# Antena AI — Product Discovery Baseline

> Working repository name only. Commercial brand is not approved.

This repository is for discovery and specification of a reusable AI voice platform. The current direction is to investigate a MyEqual.ai-style personal AI call assistant first, then add trusted domain-specific capabilities, initially hospitality.

**Phase: discovery and documentation only. Product implementation is not authorised.**

## Start here
- [Project charter](docs/governance/PROJECT_CHARTER.md)
- [Current state](docs/governance/CURRENT_STATE.md)
- [Handover guide](docs/governance/HANDOVER.md)
- [Discovery plan](docs/discovery/DISCOVERY_PLAN.md)
- [Decision log](docs/governance/DECISION_LOG.md)
- [Research register](docs/research/RESEARCH_REGISTER.md)
- [Requirements index](docs/requirements/REQUIREMENTS_INDEX.md)
- [Architecture principles](docs/architecture/ARCHITECTURE_PRINCIPLES.md)
- [Roadmap](docs/roadmap/ROADMAP.md)
- [Pricing and unit economics](docs/business/PRICING_AND_UNIT_ECONOMICS.md)

## Non-negotiable rules
- No product code, infrastructure code, migrations, or deployable prototypes until the owner explicitly approves the documented baseline.
- Research claims must be sourced and distinguish verified facts, vendor claims, estimates, assumptions and hypotheses.
- Use trusted server-configured domain connectors and domain APIs; no direct domain database access and no client-supplied arbitrary backend URLs.
- Evaluate open-source dependencies for licence, maintenance, security, total cost and lock-in.
- Treat 10,000 users as a target requiring workload modelling, not as a concurrency specification.
- Keep handover and current-state documents up to date.

## Decision statuses
PROPOSED, RESEARCH_REQUIRED, EXPERIMENT_REQUIRED, DECIDED, APPROVED, DEFERRED.
