# Roadmap — Discovery to Release

Status: planning baseline only. Dates and implementation milestones are not committed.

## Phase 0 — Governed discovery and evidence collection (current)

Build and reconcile the complete discovery baseline: charter, source-backed competitor/market research, customer validation, telephony route feasibility, provider pricing/terms, product scope, UX, architecture/API/data models, dependency/licence review, threat model/data inventory, privacy/legal issue register, pricing/economics, capacity model, requirements, traceability, acceptance thresholds and verification strategy.

Phase 0 includes both desk research and **non-code evidence collection** where required. Customer interviews, controlled calls on test SIMs, provider outreach, participant UX validation and any activity that collects personal data or incurs cost require their own completed approval record under `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md`. A general instruction to continue or the existence of a protocol does not authorize the activity. Keep evidence private/sanitized as specified; do not put identifiable participant or call data in this public repository.

Do not write product code, prototypes or implementation spikes during Phase 0. If a proposed technical experiment requires product code, record it as a separate implementation activity and leave it blocked until explicit implementation authorization.

### Remaining discovery gaps before Phase 0 exit

- Conduct customer interviews; the interview pack exists but no interviews have occurred. Record negative and contradictory evidence.
- Obtain owner-approved, controlled carrier/SIM/device route evidence using the telephony protocol; no live tests have occurred.
- Obtain at least two comparable written provider quotes for the exact intended route, including every call leg, model/media usage, data terms, taxes, failure billing and limits.
- Complete source validation and hands-on competitor feature/pricing review where possible.
- Reconcile proposed acceptance thresholds before tests; do not change them after seeing results without a documented owner decision.
- Validate textual wireflows with 5–8 users under an approved protocol; produce visual UX specs only after key route and segment assumptions are supported.
- Complete provider, exact-version dependency and transitive licence/security review.
- Obtain jurisdiction-specific legal review for telecommunications, caller notice/consent, recording, personal-data processing, provider contracts and distribution policies.
- Reconcile requirements, traceability, API contract, data model, threat model, privacy inventory, pricing, capacity and UX; verify repository links.
- Resolve brand/positioning and initial segment based on evidence, not preference alone.
- Present the residual-risk register, evidence map, decision pack and consistent baseline for explicit owner review.

**Phase 0 exit gate:** the owner explicitly approves a coherent discovery baseline, including the selected problem/segment and geography (or documented alternatives), evidence-backed route decision, scope, requirements, architecture direction, data/legal posture, economics, acceptance gates and residual risks/conditions. If an essential evidence gate is not met, record a justified stop, pivot or further-validation decision instead of implying it passed.

**Important separation:** Phase 0 baseline approval is not implementation authorization. Product code remains blocked until the owner gives a separate, explicit implementation authorization after reviewing the approved baseline. Phase 0 completion does not itself lift that block.

## Phase 1 — Approved core MVP implementation (only after separate authorization)

Implement only the owner-approved minimum personal call-assistant flow, identity/configuration, call session lifecycle, necessary history/privacy controls, security, metering, observability and support fundamentals. Use TDD and requirement traceability. Start only after:
- Phase 0 baseline approval is recorded;
- the owner explicitly authorizes implementation as a separate decision;
- route, provider, legal/privacy and spend preconditions for the first implementation slice are clear;
- requirements and acceptance criteria for that slice are approved;
- unresolved risks and excluded features are documented.

If a route or provider decision remains blocking, do not code around an assumption. Return to governed discovery or record an explicit scope pivot before proceeding.

## Phase 2 — Controlled pilot (separate approval required)

Use a small invite-only cohort only after the implemented MVP passes its acceptance gates. Verify reliability, user value, support burden, cost, abuse controls, notices, deletion and billing. Require explicit pilot approval, defined participant consent, monitoring, spend caps, incident response and rollback criteria. No production traffic is authorized by MVP implementation approval alone.

## Phase 3 — Hospitality profile (future, separate scope)

Expose selected hospitality actions through trusted Antena APIs with tenant-scoped authorization, confirmation policy, audit and idempotency. The Antena backend remains authoritative. Do not make hospitality integration a dependency of the initial personal-assistant MVP.

## Phase 4 — Scale and expansion

Increase capacity against measured workloads; validate the 10,000-user scenario against actual MAU, connected/AI-active minutes, peak arrivals and provider limits. Consider further professional profiles only after core product and connector governance are validated.

## Release gates

Every phase requires evidence, security/privacy review, operational readiness, acceptance criteria and explicit owner approval appropriate to that phase. Discovery-activity approval, baseline approval, implementation authorization and pilot approval are separate decisions. The legal/advocate profile is deferred and is not a dependency for the initial release.


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


## Phase 0 exit-gate increment — 2026-10-12
- Added `docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md` as a consolidated map of 20 discovery gates, required evidence, current status and exit conditions.
- It separates document preparation from evidence collection, baseline approval and explicit implementation authorisation. Phase 0 remains incomplete; the map is a review aid, not approval.


## Residual risk review increment — 2026-10-12
- Added `docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md` and linked it through the README, exit criteria, owner decision pack, audit, current state and handover.
- The register tracks 18 risks with evidence needs and stop conditions; no risk is considered accepted or closed merely because a mitigation document exists.
- Phase 0 remains incomplete. Route, customer, provider, legal, economics and operational evidence remain outstanding.
