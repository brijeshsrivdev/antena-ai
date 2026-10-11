# Roadmap — Discovery to Release

Status: planning baseline only. Dates and implementation milestones are not committed.

## Phase 0 — Governed discovery (current)
Deliver charter, source-backed competitor/market research, customer validation plan, telephony feasibility, product scope, UX journeys, architecture, dependency/licence evaluation, privacy/legal analysis, pricing/economics, capacity model and numbered requirements.

**Exit gate:** owner reviews a coherent baseline and explicitly authorises implementation. No coding before this gate.

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