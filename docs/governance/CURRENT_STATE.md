# Current State

Snapshot: 2026-10-12. Repository: brijeshsrivdev/antena-ai. Default branch: main.

- Product implementation: not started and not authorised.
- Discovery: in progress; charter approval pending.
- Commercial brand: not selected or cleared.
- Owner's process requirement: complete research, product/marketing strategy, pricing, architecture, UX, dependency evaluation, requirements and roadmap before any coding. Owner explicitly approves implementation start.

## Known direction
- First investigate and replicate the core behaviour of a MyEqual.ai-style personal AI call assistant; later extend to domain-specific profiles.
- Android-first is the current client direction, subject to telephony and platform feasibility.
- Hospitality is the first candidate domain and should use existing Antena backend APIs, not direct database access.
- Individual users configure personal context through structured forms.
- A dedicated AI API service is expected to handle orchestration, sessions, configuration and provider abstraction.
- Legal/advocate support is a future candidate, not a first-release dependency.
- Target scale: 10,000 users; model registered, active and concurrent users separately.

## Open questions
Target segment, launch geography, core feature parity, call-routing model, provider stack, cost/minute, pricing, consent/retention, SLOs, acquisition strategy, open-source dependency choices, brand and domain availability.

## Discovery increments recorded
The existing baseline includes initial competitor/market analysis, Android telephony feasibility, customer validation plan, privacy/regulatory issue register, pricing/economics, capacity model, product scope, UX inventory, positioning/GTM hypotheses, open-source/provider review, voice-stack candidate review, requirements draft, architecture options, threat model, data inventory, test strategy, traceability matrix, API contract and data model drafts.

Latest additions:
- docs/research/COMPETITOR_MATRIX.md: feature and business comparison of Equal AI, hiRobin, Truecaller Assistant, native screening, Tring, voice-agent platforms and business telephony vendors.
- docs/business/COST_SCENARIO_MODEL.md: sensitivity analysis at assumed ₹4/₹7/₹12 per connected minute; not provider quotes. Illustrates that ₹249/month can be uneconomic at modest usage depending on actual cost.
- docs/discovery/CUSTOMER_INTERVIEW_PACK.md: neutral interview script, evidence capture and proposed qualitative exit gates. No interviews have occurred.
- docs/research/TELEPHONY_VALIDATION_PROTOCOL.md: owner-run carrier/device test matrix and safety boundaries. No live route tests have occurred.
- docs/discovery/UX_WIREFLOW_SPEC.md: textual onboarding, incoming-call, history, profile, billing and deletion flows. No visual prototype was created.

## Evidence and constraints
- Equal AI is the most direct benchmark found; hiRobin demonstrates a broader task-completion proposition. Public claims/store listings are not independent performance tests.
- Android call-screening/redirection APIs do not establish unrestricted cellular audio capture. Carrier forwarding and cloud voice remain hypotheses until route-specific tests and written provider confirmation.
- Public price anchors differ in scope and are not comparable all-in quotes. The ₹4/₹7/₹12 connected-minute cases are sensitivity assumptions only.
- 10,000 registered users is not a concurrency specification. MAU, minutes, peaks and provider limits need measured evidence.
- Antena hospitality integration must use trusted APIs; never direct database access or client-supplied arbitrary URLs.
- No interviews, carrier/device tests, written route-specific provider quotes, legal opinions, benchmarks, load tests or product implementation have been performed.

## Remaining Phase 0 gaps
1. Conduct customer interviews and preserve negative/contradictory evidence.
2. Run owner-supervised test calls on selected devices/carriers using the documented protocol.
3. Obtain at least two comparable written provider quotes for the exact route.
4. Complete source validation and hands-on competitor review where possible.
5. Set measurable acceptance thresholds and reconcile requirements, UX, API, data model, security and legal controls.
6. Complete exact-version dependency/licence/provider-terms review and jurisdiction-specific legal advice.
7. Validate visual wireflows with users, then complete a consistency audit.
8. Obtain explicit owner approval of the baseline before any implementation.

## Last verified state
README and linked documents must be verified against current main after this increment. Baseline remains a broad draft, incomplete and unapproved. Product implementation remains unauthorised.


## Latest discovery increment — 2026-10-11
- Added Android route decision analysis grounded in official CallScreeningService, CallRedirectionService and Google Play permissions guidance. It reinforces that screening/redirection APIs do not themselves provide unrestricted cellular audio access.
- Added a provider RFP and scorecard covering exact route eligibility, all call legs, model/media components, pricing, data terms, security, support and exit requirements. No provider has been contacted and no quote has been received.
- Added capability governance for profile allowlists, tenant-scoped Antena APIs, confirmation rules, audit, idempotency and prompt-injection boundaries.
- Added low-cost GTM experiments for consumer and hospitality segments. No marketing experiment has run.
- Updated README index. The baseline remains a draft; no coding or deployment is authorised.


## Quality evaluation increment — 2026-10-11
- Added docs/quality/VOICE_AGENT_EVALUATION_PLAN.md with synthetic-corpus design, consented controlled-call guidance, candidate latency/accuracy/route gates, security zero-tolerance cases, reproducibility metadata and pilot approval requirements.
- The numeric thresholds are proposed starting points only. No benchmark or load test has run, and no threshold is approved.

## Provider pricing evidence increment — 2026-10-11
- Added `docs/research/PROVIDER_PRICING_EVIDENCE.md` and indexed it from README.
- Public desk research found Ringg advertises ₹6/connected minute for a bundled voice-agent product; this does not establish support for the existing-number personal call-assistant route.
- Exotel's published business-phone packages exclude Voice Streaming, which requires a separate quote; Exotel's documentation also says mobile-carrier forwarding charges are separate.
- Truecaller's carrier-specific forwarding setup is evidence that this pattern exists in-market, not proof that our product can use the same route or terms.
- Updated the cost model to clarify non-comparable price scopes. No provider has been contacted, no quote received, and no call-route test performed.
- The baseline remains documentation-only, incomplete and unapproved. Implementation remains unauthorised.

## Competitor evidence increment — 2026-10-11
- Updated `docs/research/COMPETITOR_MATRIX.md` with Sharyx AI Call Assistant as an adjacent Android-listed product that describes forwarding to a dedicated AI number.
- Clarified that Equal AI's public terms describe variable paid-feature pricing; App Store ₹149/₹249 entries are not a universal subscription quote.
- README currently indexes 40 unique documentation links, including the provider pricing evidence document. The linked docs are still drafts and the baseline is not approved.

## Baseline consistency audit increment — 2026-10-11
- Added `docs/governance/BASELINE_CONSISTENCY_AUDIT.md`, a cross-document readiness review covering 12 P0/P1 gaps.
- Key findings: call-route feasibility and customer evidence remain unproven; provider pricing references have different scopes; cost/capacity scenarios use different workload assumptions; legal/privacy controls depend on route/provider/jurisdiction; requirement status language and traceability need normalization.
- The audit makes no product decisions and does not authorise implementation. README indexes the audit.

## Cross-document normalization increment — 2026-10-11
- Added `docs/architecture/WORKLOAD_SCENARIO_BASELINE.md` as a shared proposed low/base/high workload table: 20k / 150k / 600k monthly connected minutes, with explicit MAU, calls/user, duration and illustrative concurrency assumptions.
- Linked the shared scenario reference from capacity and pricing documents. The separate 10k / 75k / 240k minute set remains labelled as alternate sensitivity analysis, not directly comparable.
- Normalized the core requirements header to `DRAFT`, because formal review has not started. This does not approve any requirement.
- Added `docs/governance/BASELINE_CONSISTENCY_AUDIT.md` and linked it from README. Baseline remains incomplete; no coding or deployment is authorised.

## Requirements and MVP scope increment — 2026-10-11
- Expanded `docs/requirements/TRACEABILITY_MATRIX.md` to map REQ-001–REQ-015 and NFR-001–NFR-010 to evidence state, UX, architecture/data boundaries, risks, verification and proposed release gates.
- Added `docs/discovery/MVP_SCOPE_AND_FEATURE_GATES.md` to distinguish core candidates, conditional features and deferred scope. It is not an approved MVP.
- Updated `REQUIREMENTS_INDEX.md` to point to the traceability and scope-gate artefacts.
- Remaining blockers are unchanged: customer interviews, owner-supervised route tests, comparable provider quotes, jurisdiction-specific legal review, complete measurable acceptance criteria, and owner approval.


## Acceptance-threshold register increment — 2026-10-12
- Added `docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md` and linked it from README and REQUIREMENTS_INDEX.md.
- The register distinguishes proposed candidate thresholds from open values. No threshold has owner approval; REQ-001 and REQ-006 now reference proposed AT-001/AT-004 values in the canonical requirements; NFR target decisions remain open.
- Candidate controls include a two-action disable path, an exploratory route-verification target, measurable cancellation, and zero-tolerance checks for duplicate charges, cross-tenant access and unauthorised actions. These require review and evidence before use as release gates.
- No interviews, carrier/device tests, written provider quotes, legal opinions, benchmarks, load tests or implementation have occurred. Implementation remains unauthorised.


## Owner decision pack increment — 2026-10-12
- Added `docs/governance/OWNER_DECISION_PACK.md` to consolidate ten discovery decisions, their evidence needs, blocked dependencies and the explicit implementation gate.
- Linked the decision pack from README. It records the current hypotheses without treating them as approved and lists evidence not yet collected.
- Next evidence-led work should prioritize customer interviews, controlled call-route feasibility, comparable written provider quotes and jurisdiction-specific legal review. Experiments require owner approval; product code remains unauthorised.


## Phase 0 evidence workbook increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md` with private participant-record guidance, route-test capture rows, provider quote comparison and evidence-to-decision logging.
- This prepares fieldwork; it does not claim that interviews, telephony tests or provider outreach have occurred. Owner approval and safety checks are required before experiments.
- README now indexes the workbook. Implementation remains unauthorised.


## Experiment approval checklist increment — 2026-10-12
- Added `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md` as a scope-specific approval gate for discovery activities, with separate conditions for interviews, telephony tests, provider outreach and UX validation.
- The checklist covers consent, minimum necessary data, private handling of identifiable evidence, budget ceilings, safe restoration/disable procedures, stop conditions and post-activity review.
- It is a preparation document, not approval to run fieldwork. No interviews, provider outreach, route tests, quotes, legal opinions or benchmarks are claimed complete; implementation remains unauthorised.
- README and roadmap now index/reference the checklist.


## Phase 0 exit criteria increment — 2026-10-12
- Added `docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md`, consolidating 20 gates across customer validation, route feasibility, provider costs, legal/privacy, scope, UX, requirements, architecture, security, operations, brand and owner decisions.
- The map explicitly distinguishes prepared documentation from uncollected evidence and from owner approvals. It records Phase 0 as incomplete and implementation as unauthorised.
- README and roadmap now index/reference the exit map. No external experiment or implementation is claimed complete.


## Residual-risk register increment — 2026-10-12
- Added `docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md` with 18 risks, current evidence state, mitigation references and stop conditions.
- Linked it from README, Phase 0 exit map, owner decision pack and consistency audit. Risks remain open unless evidence and explicit owner disposition support closure; implementation remains unauthorised.


## Repository navigation verification — 2026-10-12
- Parsed the current README Markdown links and compared all 49 local `.md` targets against the recursive Git tree on `main`; all 49 targets exist. No broken local README document links were found in this check.
- This is a repository-link check only; it does not validate external URLs, source freshness, factual claims or the completeness of the research baseline.


## Source and requirement consistency pass — 2026-10-12
- Rechecked official Android CallScreeningService/CallRedirectionService references, Google Play call/SMS policy, MeitY's DPDP Rules index and TRAI's TCCCPR amendments index. Updated RESEARCH_REGISTER.md, ANDROID_CALL_ROUTE_DECISION.md and PRIVACY_AND_REGULATORY_RISK_REGISTER.md with source dates, limitations and recheck requirements.
- Clarified that REQ-001–REQ-015 and NFR-001–NFR-010 are stable IDs within the current draft, while their content, priorities and traceability remain unapproved. The core draft and requirements index no longer imply the IDs themselves are awaiting reconciliation.
- README's 49 local Markdown links were checked against the recursive repository tree; all targets exist. This did not validate external URLs or prove factual completeness.
- No interviews, live route tests, provider quotes, legal opinions, benchmarks, load tests or implementation have occurred. Phase 0 remains incomplete and implementation unauthorised.


## External claim traceability increment — 2026-10-12
- Added `docs/research/EXTERNAL_CLAIM_LEDGER.md` with 17 consequential claims, source classes, evidence scope, exclusions, confidence/status and decision impact.
- Indexed the ledger in README and registered it as RES-024 in the research register.
- The ledger explicitly separates official platform/regulator documentation from vendor assertions, store-reported signals and internal scenario assumptions. It does not turn public pricing into an all-in quote or platform API documentation into route feasibility.
- This is desk-research organisation only. It does not claim every external page was re-opened during this pass, nor does it resolve route feasibility, customer demand, provider terms, legal applicability or performance.
- No interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Phase 0 remains incomplete and implementation remains unauthorised.


## Requirement-reference verification increment — 2026-10-12
- Programmatically compared identifiers across CORE_REQUIREMENTS_DRAFT.md, TRACEABILITY_MATRIX.md, UX_SCREEN_INVENTORY.md, THREAT_MODEL.md, PRIVACY_AND_REGULATORY_RISK_REGISTER.md and ACCEPTANCE_THRESHOLD_REGISTER.md.
- Result: all 15 REQ IDs and 10 NFR IDs appear in both the core draft and traceability matrix; all referenced UX/THR/PRIV IDs were found in their source documents; AT-001 and AT-004 references resolve.
- Recorded the result and its limits in BASELINE_CONSISTENCY_AUDIT.md. This confirms identifier presence only, not requirement quality, semantic coverage, acceptance, legal sufficiency or implementation.
- Added EXTERNAL_CLAIM_LEDGER.md and indexed it in README and RESEARCH_REGISTER.md. Existing README links had previously been checked as 49 valid local paths; the newly added ledger file and README link were separately confirmed, but a fresh full recursive-tree scan has not been run.
- Phase 0 remains incomplete. No interviews, provider outreach, live route tests, legal opinions, benchmarks, load tests or implementation have occurred. Implementation remains unauthorised.

## Policy-source and conditional-UX reconciliation — 2026-10-12
- Rechecked current Google Play SMS/Call Log policy, Exotel's official business-phone pricing and the DPDP Act commencement Gazette. The external claim ledger now records the specific limitations and avoids equating vendor package prices with an all-in route quote or a Rules index date with the Gazette's commencement-notification date.
- Updated Android route and privacy research with explicit Play policy constraints and commencement caveats. No Play review or legal opinion has been obtained.
- Updated UX screen inventory and wireflow to distinguish conditional contact preferences, optional transcript/audio, route-dependent takeover and user-confirmed tasks from a promised MVP. The core experience should not depend on broad contact-book access by default.
- These are desk-research and document-consistency changes only. No customer interviews, provider outreach, route tests, legal opinions, benchmarks, load tests or implementation occurred. Phase 0 remains incomplete; implementation remains unauthorised.
## Threshold and quote-scenario consistency pass — 2026-10-12
- Aligned `VOICE_AGENT_EVALUATION_PLAN.md` with `ACCEPTANCE_THRESHOLD_REGISTER.md`: the threshold register is now explicitly the source of truth for candidate numeric gates, and unregistered numerical latency/intent/summary/takeover/reconciliation targets were removed from the evaluation table. Proposed route gate AT-002 remains unapproved; latency stays baseline-first under AT-003.
- Aligned `VOICE_PROVIDER_RFP.md` with `WORKLOAD_SCENARIO_BASELINE.md` by making 20k/150k/600k monthly connected minutes the default quote comparison set. The 10k/75k/240k-minute set is explicitly optional and separate, not to be blended with the canonical scenario.
- Updated `BASELINE_CONSISTENCY_AUDIT.md`. No thresholds are owner-approved, no provider has been contacted, no tests or interviews have run, and implementation remains unauthorised.
## Workload arithmetic verification — 2026-10-12
- Independently recomputed monthly minutes, average concurrency, illustrative 10× peaks and cost tables at ₹4/₹7/₹12 plus the ₹6/min public benchmark for the canonical and alternate scenario sets. All reviewed arithmetic matches the stated formulas.
- This does not validate scenario inputs, demand, peak multiplier, route support or applicability of a public vendor price. `BASELINE_CONSISTENCY_AUDIT.md` records the verification and limitations.