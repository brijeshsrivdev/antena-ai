# Roadmap — Discovery to Release

Status: planning baseline only. Dates and implementation milestones are not committed.

## Phase 0 — Governed discovery (current)
Deliver charter, source-backed competitor/market research, customer validation plan and interview pack, telephony feasibility and test protocol, product scope, UX screen inventory and wireflows, architecture/API/data model drafts, dependency/licence evaluation, threat model/data inventory, privacy/legal issue register, pricing/economics and cost scenarios, capacity model, numbered requirements, traceability matrix and verification strategy.

**Exit gate:** owner reviews a coherent baseline and explicitly authorises implementation. No coding before this gate.

### Remaining discovery gaps before Phase 0 exit
- Conduct customer interviews; interview pack exists but no interviews have occurred. Record negative and contradictory findings.
- Obtain owner-run carrier/SIM/device evidence using the telephony protocol; no live tests have occurred.
- Obtain at least two comparable written provider quotes for the exact intended route, including every call leg, model usage, data terms, taxes, failure billing and limits.
- Complete source validation and hands-on competitor feature/pricing review where possible.
- Define measurable routing success, takeover, latency, language quality, privacy, cost, retention and capacity thresholds before running tests.
- Validate textual wireflows with 5–8 users; produce visual UX specs only after key route and segment assumptions are supported.
- Complete provider, exact-version dependency and transitive licence/security review.
- Obtain jurisdiction-specific legal review for telecommunications, caller notice/consent, recording, personal-data processing, provider contracts and distribution policies.
- Reconcile requirements, traceability, API contract, data model, threat model, privacy inventory, pricing, capacity and UX; verify all README links.
- Resolve brand/positioning and initial segment based on evidence, not preference alone.
- Owner signs off scope, risk acceptance, release gates and explicit implementation start.

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


## Additional discovery gates
- Read and resolve the route implications in ANDROID_CALL_ROUTE_DECISION.md against owner-run carrier/device evidence.
- Send the same VOICE_PROVIDER_RFP.md questionnaire to at least two candidates and retain written responses.
- Review CAPABILITY_GOVERNANCE.md alongside API contract, threat model, data inventory and hospitality API capabilities.
- Use GTM_EXPERIMENT_PLAN.md only after agreeing interview recruitment, route disclosure and success thresholds.
- Review current Android/Google Play policies and India telecom/privacy rules again immediately before product implementation or distribution; this desk review is not legal advice.


- Add VOICE_AGENT_EVALUATION_PLAN.md to the Phase 0 review. Approve measurable thresholds before running tests; any unauthorized action, cross-tenant access or silent call loss is a release blocker, not a trade-off to average away.

## Latest desk-research updates — 2026-10-11
- Provider pricing evidence is now separated from assumptions in `docs/research/PROVIDER_PRICING_EVIDENCE.md`. Public prices remain non-comparable; provider RFP responses are still required.
- Competitor matrix now includes Sharyx AI Call Assistant and clarifies that Equal AI in-app pricing is offer-dependent. These findings do not replace hands-on evaluation or customer interviews.
- No discovery exit criteria have been satisfied by these desk-research updates alone. Owner-supervised route tests, customer evidence, written quotes, legal review, and explicit approval remain outstanding.

## Consistency audit outcome — 2026-10-11
See `docs/governance/BASELINE_CONSISTENCY_AUDIT.md` for the 12 identified P0/P1 gaps. In particular, reconcile the two different workload scenario sets into one canonical low/base/high model; keep published price anchors separate from cost assumptions and written quotes; normalize requirement lifecycle status; and complete end-to-end traceability. This audit is a planning artifact, not evidence that the gates have passed.

## Workload and baseline consistency updates — 2026-10-11
- Added a shared proposed workload table in `docs/architecture/WORKLOAD_SCENARIO_BASELINE.md`; the capacity and pricing models now point to it.
- The alternate 10k/75k/240k-minute sensitivity cases remain distinct and explicitly labelled.
- Normalized core requirement lifecycle wording to DRAFT. Full traceability, route feasibility, customer evidence, provider quotes, counsel review and owner approval remain exit criteria.

## Requirements/scope increment — 2026-10-11
- Expanded the traceability matrix for REQ-001–REQ-015 and NFR-001–NFR-010.
- Added a proposed MVP scope gate matrix that treats route feasibility as a prerequisite and separates core candidates from conditional/deferred features.
- The scope and traceability remain drafts. Customer/route/provider/legal evidence and owner approval remain outstanding.


## Phase 0 evidence workbook increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md` with private participant-record guidance, route-test capture rows, provider quote comparison and evidence-to-decision logging.
- This prepares fieldwork; it does not claim that interviews, telephony tests or provider outreach have occurred. Owner approval and safety checks are required before experiments.
- README now indexes the workbook. Implementation remains unauthorised.


## Experiment governance increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md` to require scope-specific owner approval before interviews, telephony tests, provider outreach that shares project details, or UX validation involving participants.
- The checklist specifies data minimisation, consent, reversible routing, spend caps, stop conditions, result review and sanitised evidence handling. It authorises no activity by itself.
- Fieldwork, provider contact, live tests and implementation remain unapproved until the relevant gates are explicitly cleared.
