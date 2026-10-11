# Roadmap — Discovery to Release

Status: planning baseline only. Dates and implementation milestones are not committed.

## Phase 0 — Governed discovery (current)
Deliver charter, source-backed competitor/market research, customer validation plan, telephony feasibility, product scope, UX screen inventory, architecture/API/data model drafts, dependency/licence evaluation, threat model/data inventory, privacy/legal issue register, pricing/economics, capacity model, numbered requirements, traceability matrix and verification strategy.

**Exit gate:** owner reviews a coherent baseline and explicitly authorises implementation. No coding before this gate.

### Remaining discovery gaps before the Phase 0 exit gate

- Complete competitor source validation and hands-on feature/pricing review where possible.
- Conduct customer interviews; the interview plan exists but no interviews have occurred.
- Obtain written provider quotes and validate the exact incoming-call route on selected carrier/SIM/device combinations.
- Define measurable latency, routing, quality, cost, retention and capacity thresholds.
- Complete UX wireflows/visual specifications and accessibility review.
- Finish provider/licence and privacy/terms due diligence, country-specific legal review, and API/data model/requirements traceability.
- Resolve cross-document contradictions and request explicit owner approval.

## Phase 1 — Feasibility experiments (only after approval)
Run narrowly scoped, non-production experiments for call routing, streaming audio, interruption handling, latency, supported languages, cost per minute and provider failure modes. Define data handling and consent for test participants. No real customer rollout without a separate release gate.

## Phase 2 — Core MVP
Implement only the owner-approved minimum personal call-assistant flow, identity/configuration, call session lifecycle, history controls, security, metering, observability and support fundamentals. Use TDD and requirement traceability. Scope depends on validated telephony path.

## Phase 3 — Controlled pilot
Small invite-only cohort; verify reliability, user value, support burden, cost, abuse controls, consent, deletion and billing. Require explicit pilot approval and rollback criteria.

## Phase 4 — Hospitality profile
Expose selected hospitality actions through trusted Antena APIs with tenant-scoped authorization, audit and idempotency. The Antena backend remains authoritative.

## Phase 5 — Scale and expansion
Increase capacity against measured workloads; validate 10,000-user scenarios and operational readiness. Consider further professional profiles only after core product and connector governance are validated.

## Release gates
Each phase requires evidence, security/privacy review, operational readiness, acceptance criteria and explicit owner approval. Legal/advocate profile is deferred; it is not a dependency for the initial release.