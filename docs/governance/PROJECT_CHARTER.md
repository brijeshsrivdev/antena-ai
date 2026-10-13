# Project Charter

Status: PROPOSED — owner approval pending. Date: 2026-10-11. Phase: discovery and documentation only.

## Purpose
Discover and specify a reusable, multi-tenant AI voice platform whose primary MVP hypothesis is a configurable AI business phone assistant. Businesses configure supported inbound call workflows, authorized customer lookups/actions, and dashboard visibility into call outcomes. Personal call-assistant mode is a later candidate, not the primary MVP. Hospitality may be a future domain integration through trusted Antena APIs; legal/advocate and other professional domains are not launch commitments.

## Candidate capabilities to research
- Business-owned assistant configuration and versioned inbound call workflows using constrained, approved blocks.
- Handling of calls delivered through a proven, supported business-number/telephony route.
- Caller identification and verification rules; customer lookup must not treat caller ID as proof of identity.
- Tenant-scoped, allowlisted read/write connectors, initially to be selected through discovery; ticket/case creation is a candidate action, not an assumed integration.
- Call history, missed-call/route outcome distinctions, summaries and operational dashboard, subject to event availability, consent, law and retention policy.
- Dedicated AI API for orchestration, sessions, tenant/workflow resolution, provider abstraction and policy enforcement.
- Human escalation only where supported by the chosen route/provider; otherwise provide a validated fallback.

These are hypotheses, not a final product promise.

## Required before implementation approval
1. Evidence-backed customer segment, problem and competitive position.
2. Complete core/future feature catalogue and exclusions.
3. End-to-end user journeys and UI/UX, including visual and error states.
4. Market and competitor research with sources and confidence.
5. Pricing, unit economics, acquisition assumptions and 10,000-user workload model.
6. Architecture, API contracts, data model, threat model and compliance requirements.
7. Open-source/provider evaluation including licences and maintenance.
8. Numbered requirements, acceptance criteria, dependencies and verification methods.
9. Roadmap, risk register, test strategy, operations and support plan.
10. Handover documentation and explicit owner approval.

## Non-goals during discovery
No product code, deployable prototypes, infrastructure changes, database migrations, or production deployment. No claim of native cellular call interception until feasibility and platform restrictions are validated. No commercial brand selection or trademark-clearance claim without screening.

## Success criteria
The owner can make an informed go/no-go decision from traceable evidence, explicit assumptions, cost/capacity scenarios, testable requirements, reviewed UX and documented risks. Implementation starts only after explicit owner approval.