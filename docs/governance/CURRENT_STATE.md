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
