# Baseline Consistency and Readiness Audit

**Snapshot:** 2026-10-12  
**Repository:** `brijeshsrivdev/antena-ai`, branch `main`  
**Status:** Draft audit of existing documents; not an approval or implementation authorization.

## Executive assessment

The repository has a broad discovery baseline, but it is **not implementation-ready**. The biggest blockers are not missing code; they are unresolved product route feasibility, lack of customer evidence, absent route-specific provider quotes, unapproved legal/privacy decisions, and incomplete cross-document traceability.

This audit records contradictions and decisions that must be resolved before the owner can approve a coherent baseline. It does not claim that external experiments, interviews, legal reviews, or provider conversations have occurred.

## P0 — Must resolve before choosing an MVP architecture

### AUD-001 — Incoming-call route and user control
**Documents:** `ANDROID_CALL_ROUTE_DECISION.md`, `TELEPHONY_FEASIBILITY.md`, `TELEPHONY_VALIDATION_PROTOCOL.md`, `CORE_REQUIREMENTS_DRAFT.md`, `UX_WIREFLOW_SPEC.md`.

The Android APIs reviewed do not establish general cellular-audio capture. Existing-number forwarding, hosted-number/VoIP and any narrower screening-only experience are materially different products.

**Required resolution:** Run owner-supervised controlled tests with consenting test SIMs and a written route-specific provider response. Record operator, plan, device/OS, SIM configuration, forwarding mode, caller-ID behavior, charges, failover, disable/recovery and takeover. Do not mark routing verified from UI actions alone.

**Gate:** No final architecture, UX promise, or MVP parity claim until the route is proven for a stated supported matrix.

### AUD-002 — No customer evidence yet
**Documents:** `CUSTOMER_VALIDATION_PLAN.md`, `CUSTOMER_INTERVIEW_PACK.md`, `GTM_EXPERIMENT_PLAN.md`, `MARKET_DEMAND_AND_SEGMENTATION.md`.

Competitor existence is evidence of a category, not proof that a new product's target users have sufficient pain or will pay.

**Required resolution:** Conduct and record interviews across explicitly selected user segments. Track negative evidence, current workaround, frequency, consequence, trust objections, setup willingness and willingness to pay. Keep stated intent separate from observed behaviour.

**Gate:** Select the initial segment and top use case based on evidence, not a broad “everyone who receives calls” market.

### AUD-003 — Provider prices are not comparable all-in costs
**Documents:** `COST_SCENARIO_MODEL.md`, `PRICING_AND_UNIT_ECONOMICS.md`, `CAPACITY_AND_SCALE_MODEL.md`, `PROVIDER_PRICING_EVIDENCE.md`, `VOICE_PROVIDER_RFP.md`.

The repo contains three different uses of cost numbers:
- ₹4/₹7/₹12 per connected minute are sensitivity assumptions.
- ₹6/min is a published Ringg price anchor, not a confirmed quote for this product.
- Twilio/Exotel and other public figures describe different product components or billing models.

These values are useful for different purposes but must not be blended into a single “expected cost”.

**Required resolution:** Keep assumptions, public price anchors and binding quotes in separate columns. Obtain two comparable written quotes for each plausible route; itemise forwarding/carrier charges, all call legs, streaming, STT/TTS/model, number rental, failure billing, transfer, taxes, minimums and concurrency limits.

**Gate:** No included-minute plan, unlimited promise or margin claim until route-specific costs are reconciled.

### AUD-004 — Usage scenarios differ across cost and capacity documents
**Documents:** `COST_SCENARIO_MODEL.md`, `CAPACITY_AND_SCALE_MODEL.md`, `PRICING_AND_UNIT_ECONOMICS.md`.

The cost scenario model illustrates 10,000 / 75,000 / 240,000 monthly minutes using 10%, 25% and 40% MAU with 10 / 30 / 60 minutes per active user. The capacity and pricing models illustrate 20,000 / 150,000 / 600,000 minutes using different call-frequency and duration assumptions. These are not necessarily contradictions—the assumptions differ—but the scenarios are not directly comparable as currently presented.

**Required resolution:** Establish one canonical low/base/high workload table with registered users, MAU, calls/MAU, average duration, connected minutes, AI-active minutes (if distinct), peak factor and source/confidence. Reference it from both cost and capacity models. Retain extra sensitivity tables only when clearly labelled.

**Gate:** Capacity and commercial forecasts must cite the same canonical workload assumptions or explain why they intentionally differ.

### AUD-005 — Legal and privacy controls depend on the selected route
**Documents:** `PRIVACY_AND_REGULATORY_RISK_REGISTER.md`, `DATA_INVENTORY_AND_LIFECYCLE.md`, `VOICE_PROVIDER_RFP.md`, `CORE_REQUIREMENTS_DRAFT.md`.

Caller disclosure, recording/transcription, data roles, cross-border processing, retention and deletion cannot be finalised without the intended route, provider terms and launch jurisdiction. The existing docs correctly treat these as open legal issues.

**Required resolution:** After route/provider shortlist, obtain jurisdiction-specific counsel review; create a processing/data-flow map and decision table for audio, transcripts, summaries, caller metadata, model-provider transfers, retention, consent/notice and deletion.

**Gate:** No real-call pilot until counsel review, approved notices and retention defaults are documented.

### AUD-006 — MVP scope is not yet bounded
**Documents:** `PRODUCT_SCOPE_AND_FEATURE_CATALOG.md`, `CORE_REQUIREMENTS_DRAFT.md`, `UX_SCREEN_INVENTORY.md`, `COMPETITOR_MATRIX.md`.

The discovery set includes live transcripts, audio, summaries, follow-up tasks, contact rules, takeover, outgoing calls and domain profiles. Shipping all of these in a first release increases route, privacy, cost and support risk.

**Required resolution:** Choose a route-dependent MVP slice with must-have, later, excluded and route-contingent features. A candidate minimal slice to evaluate—not an approved decision—is: route setup/disable, caller disclosure, bounded answering, safe termination, concise summary, usage caps and privacy controls. Treat transcript/audio retention, outgoing calls, contacts import and external actions as separate opt-in scope decisions.

**Gate:** Every MVP feature has a user problem, evidence, cost/risk rationale and measurable acceptance criteria.

## P1 — Must resolve before baseline approval

### AUD-007 — Requirement status language is ambiguous
**Documents:** `CORE_REQUIREMENTS_DRAFT.md`, `REQUIREMENTS_INDEX.md`, `DECISION_LOG.md`.

The core draft header says “DRAFT / IN_REVIEW not started,” while the index says detailed requirements are not baselined and the IDs/priorities are provisional.

**Required resolution:** Use one explicit state consistently: `DRAFT` until an actual review begins; `IN_REVIEW` only when named reviewers are actively reviewing a version. Keep “implementation not authorised” separate from requirement lifecycle status.

### AUD-008 — Traceability is partial and contains provisional mappings
**Documents:** `TRACEABILITY_MATRIX.md`, `UX_SCREEN_INVENTORY.md`, `THREAT_MODEL.md`, `API_CONTRACT_DRAFT.md`, `DATA_MODEL_DRAFT.md`.

The matrix maps requirements to screens, risk IDs and tests, but some references are broad ranges and acceptance criteria remain incomplete. Some entities and API operations are conceptual.

**Required resolution:** Create a canonical requirement register with stable IDs and per-requirement links to evidence, UX flow, architecture decision, API/data entity, threat/privacy control, positive and negative test, operational metric, owner and release gate. Validate every referenced ID exists.

### AUD-009 — Data lifecycle promises are not yet implementable
**Documents:** `DATA_INVENTORY_AND_LIFECYCLE.md`, `DATA_MODEL_DRAFT.md`, `API_CONTRACT_DRAFT.md`, `UX_WIREFLOW_SPEC.md`.

The UX promises deletion states and provider/backup caveats, but retention durations, provider-side deletion, backup expiry and legal exceptions remain undecided.

**Required resolution:** Do not publish fixed deletion promises until storage/provider architecture is known. Define per-data-class retention and deletion SLAs, residual-copy inventory, failure state, retry owner and user-facing completion semantics.

### AUD-010 — Brand and initial market are not approved
**Documents:** `PROJECT_CHARTER.md`, `POSITIONING_AND_GO_TO_MARKET.md`, `GTM_EXPERIMENT_PLAN.md`.

The repo name is `antena-ai`, but the commercial brand is intentionally unapproved. India is a candidate launch scenario, not a final geographic decision.

**Required resolution:** Select a provisional market/segment for discovery experiments; conduct trademark/domain/app-store checks before brand investment. Do not infer commercial brand approval from repository naming.

### AUD-011 — Domain integration must remain out of core dependency
**Documents:** `CAPABILITY_GOVERNANCE.md`, `API_CONTRACT_DRAFT.md`, `DATA_MODEL_DRAFT.md`, `DECISION_LOG.md`.

The intended extensibility model is sound as a proposal: server-managed capability allowlists and trusted domain APIs, with Antena as the hospitality system of record. But no Antena capability audit has established which actions are safely exposed.

**Required resolution:** Keep hospitality integration out of the first personal-assistant critical path. Later, map each Antena operation to tenant scope, read/write class, confirmation, idempotency, audit and authoritative response requirements.

### AUD-012 — Evaluation gates need owner approval and a common source of truth
**Documents:** `VOICE_AGENT_EVALUATION_PLAN.md`, `VERIFICATION_AND_TEST_STRATEGY.md`, `TELEPHONY_VALIDATION_PROTOCOL.md`, `CORE_REQUIREMENTS_DRAFT.md`.

Candidate thresholds are proposed, not approved; no benchmark or load test has run.

**Required resolution:** Create one release-gate table for route success, unexpected call loss, takeover (if in scope), disclosure, latency, summary factuality, safety violations, tenant isolation, deletion, cost and peak capacity. Mark each value as proposed, owner-approved, measured or release-blocking. Do not change thresholds after seeing test results without recording the decision.

## Recommended order of work

1. Route/provider feasibility and customer interviews in parallel, with no implementation.
2. Reconcile product scope and canonical workload/cost scenarios.
3. Complete jurisdiction and provider privacy review.
4. Normalise requirement statuses and build full traceability.
5. Finalise API/data model and UX only for the evidence-backed MVP.
6. Run a consistency audit and present an owner approval pack.

## Owner decision record

No new product decision is made by this audit. Existing proposed directions remain proposed. The owner retains approval authority. Implementation remains **not authorised** until the baseline is complete and the owner explicitly approves the next phase.


## Follow-up mitigation — experiment governance (2026-10-12)
- Added `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md` to operationalise scope-specific approval, consent, data minimisation, safety/reversibility, spend limits, stop conditions and evidence review for discovery activities.
- This partially mitigates the process/documentation risk that prepared protocols could be mistaken for permission to run experiments. It does not resolve the underlying P0/P1 evidence gaps: customer discovery, route feasibility, comparable written quotes, legal review, measured performance/economics and owner decisions remain outstanding.
- No experiment is authorised by the checklist. No product implementation is authorised.


## Consolidated exit criteria follow-up — 2026-10-12
- Added `docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md` to make Phase 0 evidence requirements and owner gates explicit across 20 workstreams.
- This improves visibility and cross-document review but does not close the substantive gaps identified in this audit. Customer evidence, route feasibility, comparable quotes, legal review, validated economics, final traceability and owner approval remain outstanding.


## Residual-risk consolidation — 2026-10-12
- Added `docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md` with 18 open or partially mitigated risks, explicit evidence needs and stop conditions.
- The register improves risk visibility but does not resolve route, demand, provider cost, legal, privacy, reliability or security evidence gaps. Risk acceptance remains an owner decision.


## README link validation — 2026-10-12
- Checked all 49 local Markdown document links in README against the repository's recursive tree on `main`; all targets exist and none were missing.
- Scope limitation: external links, link destinations' factual validity, research freshness, and non-README cross-document links were not validated by this check. The substantive P0/P1 evidence gaps remain open.


## Source freshness and requirement-ID follow-up — 2026-10-12
- Rechecked the official Android call API pages, Google Play sensitive call/SMS permission policy, MeitY DPDP Rules index and TRAI TCCCPR amendments index; recorded scope limits and date/commencement caveats in the research documents.
- Resolved a wording inconsistency: requirement IDs are stable within the working draft and referenced by the traceability matrix, but the requirements themselves remain DRAFT and unapproved. This does not close the substantive coverage/evidence gaps.
- Verified all 49 local Markdown links in README resolve to tracked files. External link validity, source freshness beyond the checked pages and all non-README links remain unverified.
- These checks improve source/status hygiene but do not resolve customer, route, provider quote, legal advice, cost validation or owner-decision blockers.


## External claim ledger and identifier-reference check — 2026-10-12
- Added `docs/research/EXTERNAL_CLAIM_LEDGER.md` and registered it as RES-024. It distinguishes official documentation, vendor claims, app-store signals, internal model assumptions and inference, including limitations and decision impact.
- Ran a programmatic lexical cross-check over the current core requirements, traceability matrix, UX screen inventory, threat model, privacy risk register and acceptance-threshold register:
  - REQ identifiers: 15 in the core draft and 15 in traceability; no missing IDs in either direction.
  - NFR identifiers: 10 in the core draft and 10 in traceability; no missing IDs in either direction.
  - Referenced UX, THR and PRIV identifiers resolve to IDs found in their respective source documents.
  - AT-001 and AT-004 references in the core draft both exist in the acceptance-threshold register.
- **Scope limitation:** This was an ID/reference-presence check, not semantic proof that each requirement is complete, correctly prioritized, testable, legally sufficient or implemented. It did not validate every cross-document link or external URL.
- The remaining blockers are unchanged: customer evidence, supported-route proof, comparable written quotes, counsel review, validated cost/performance, operational ownership and explicit owner decisions. Phase 0 remains incomplete; implementation remains unauthorised.

## Targeted policy and UX-scope reconciliation — 2026-10-12
- Reopened the current Google Play SMS/Call Log policy, Exotel's official business-phone pricing page and the DPDP Act commencement Gazette. Recorded the specific Play restrictions (including call recording and speech-to-text/text-to-voice use-case limits), the 2027-01-27 account-verification policy change, Exotel's separate Agent Stream pricing, and the difference between the MeitY Rules index date and Gazette commencement-notification date in the research ledger and related documents.
- Clarified that UX-011 contact preferences and UX-016 transcript/audio playback are conditional candidates rather than implied MVP commitments; wireflow notes now state the no-contact-permission path, transcript/audio gate, route-dependent takeover and user-confirmed follow-ups.
- These changes reduce ambiguity in the documents but do not resolve store eligibility, legal applicability, route feasibility, customer demand, pricing or provider terms. No Play review, counsel review, interviews, provider outreach, live calls or implementation occurred.