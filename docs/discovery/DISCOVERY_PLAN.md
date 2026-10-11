# Discovery Plan

Status: PROPOSED. Implementation gate: CLOSED.

## Workstreams and deliverables

### W0 — Governance
Charter, current state, handover, decision log, research register, requirements index and approval gates. Exit: owner confirms governance approach.

### W1 — Product and competitors
Research MyEqual.ai's documented features, platform support, routing, pricing and limitations; direct and adjacent competitors; gaps and differentiation. Exit: source-backed feature matrix and competitive landscape.

### W2 — Customer and market validation
Segments, jobs-to-be-done, public feedback, interview guide, low-cost validation experiments, market sizing assumptions and willingness-to-pay questions. Exit: evidence-backed segment/problem or a defined validation experiment.

### W3 — Product definition
Vision, personas, full core/future feature catalogue, exclusions, stories, acceptance criteria, edge cases and configuration forms. Exit: each feature has priority, rationale, dependencies and verification.

### W4 — UX and visual design
Information architecture, navigation, wireflows, screen inventory, copy/tone, loading/empty/error/offline states, accessibility, design tokens and visual acceptance criteria. Exit: journeys and cosmetics reviewed.

### W5 — Telephony, speech and AI
Call-routing options, provider and carrier/region support, streaming, latency, interruption, languages, fallback, data-processing terms and account-specific tests. Exit: candidate approach and explicit go/no-go experiment criteria. Never assume native cellular interception.

### W6 — Open-source/dependencies
Licence, maintenance, releases, security advisories, commercial restrictions, ecosystem maturity, deployment cost, alternatives and exit strategy. Exit: each critical dependency accepted, rejected or assigned an experiment.

### W7 — Architecture/API
System and deployment diagrams, trust boundaries, connector registry, identity/tenant model, APIs, data flows, failure modes, versioning and ADRs. Exit: requirements trace to architecture; major uncertainties isolated.

### W8 — Privacy/security/legal
Data inventory, threat model, consent/notices, jurisdictional recording rules, retention/deletion, access controls, encryption, incident response and app-store policy. Exit: no unowned critical risk; legal advice obtained where needed.

### W9 — Pricing/economics
Plan hypotheses, usage limits, trial/overage, cost per minute, margin scenarios, fees/taxes, support, acquisition and break-even. Exit: owner reviews a traceable pricing hypothesis.

### W10 — 10,000-user scale/operations
Separate registered, monthly active and concurrent users. Model calls/user, duration distribution, peak arrivals, concurrency, retention, retries and growth. Define SLOs, monitoring, backpressure, recovery and support. Exit: measurable workload and load-test targets.

### W11 — Baseline and consistency review
Numbered requirements, acceptance criteria, traceability matrix, dependency graph, risks, roadmap and independent contradiction audit. Exit: owner approves baseline and explicitly authorises implementation.

## Priority order
1. Governance.
2. Competitor/product evidence and customer validation design.
3. Telephony feasibility early because it can invalidate the product premise.
4. Product scope and UX.
5. Dependencies and architecture.
6. Security/privacy/legal in parallel.
7. Pricing and capacity economics.
8. Requirements audit and owner approval.

## Evidence standard
For each important claim capture source title/organisation, URL, access date, publication date if known, source type, finding in your own words, limitations, confidence and affected decisions/requirements.

## Definition of done
All charter outputs are complete, unknowns are classified, high-risk assumptions have experiments, costs and capacity are transparent, requirements are testable, cross-doc contradictions are resolved, and the owner explicitly approves the baseline. Coding remains blocked until then.