# Phase 0 Exit Criteria and Evidence Map

**Status:** DRAFT — review aid only. Phase 0 has not passed. Product implementation is not authorised.  
**Purpose:** Provide one evidence-led view of what must be ready, what remains unproven, and which owner decisions are required before baseline approval.

## 1. What “Phase 0 complete” means

Phase 0 is complete only when the owner can review one coherent product baseline and make explicit decisions using evidence. It is not complete merely because all documents exist.

Three gates must remain distinct:

1. **Discovery activity approval:** permission to run a particular interview, route test, provider outreach or UX validation activity. Use `PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md`.
2. **Baseline approval:** owner accepts the product direction, target user/problem, launch geography, route, scope, requirements, data/legal posture, economics, architecture options, risks and remaining conditions.
3. **Implementation authorisation:** a separate, explicit owner decision to begin code. Baseline approval alone does not silently authorise implementation unless the owner says so clearly.

## 2. Evidence status vocabulary

| Status | Meaning |
|---|---|
| DOCUMENT PREPARED | A draft plan, analysis or specification exists; it may still need review. |
| DESK RESEARCH | Public/secondary source review exists; it does not prove account-specific or field behaviour. |
| EVIDENCE REQUIRED | A decision depends on evidence not yet collected. |
| OWNER DECISION REQUIRED | Evidence and alternatives must be reviewed and the owner must decide. |
| BLOCKED | A downstream decision should not be frozen until a dependency is resolved. |
| ACCEPTED | The owner has explicitly accepted the item with rationale and any conditions. |

Do not mark an item ACCEPTED merely because a document is linked, a vendor claims support, or a single test succeeds.

## 3. Phase 0 exit matrix

| Gate | Required evidence / deliverable | Current state | Exit condition |
|---|---|---|---|
| G0-01 Governance | Charter, current state, decision log, handover, experiment-approval policy | DOCUMENT PREPARED; charter approval pending | Owner confirms governance and decision authority |
| G0-02 Customer/problem | Segment synthesis from real interviews; recent incidents, frequency, consequence, workaround, trust/setup barriers and willingness-to-pay evidence | EVIDENCE REQUIRED; no interviews claimed | Owner selects an initial segment/problem or explicitly chooses another validation loop |
| G0-03 Market/competition | Source-backed competitor matrix, limitations, differentiation hypotheses and current pricing/source caveats | DESK RESEARCH; hands-on validation incomplete | Claims and gaps reviewed; no competitor capability represented as independently verified without evidence |
| G0-04 Telephony route | Controlled test results by device/OS/operator/plan/SIM/forwarding configuration; caller ID, failure behaviour, disable/recovery and cost; written provider eligibility confirmation | BLOCKED; route unproven | Owner selects a supported route and explicitly records unsupported configurations and residual failure risk |
| G0-05 Provider and stack | Comparable written quotes for the intended route, itemised all call legs/media/STT/TTS/model/number/minimum/failure charges, limits, terms and exit costs | EVIDENCE REQUIRED; no written quotes claimed | Costs are comparable and provider fit/terms have been reviewed |
| G0-06 Privacy, telecom and legal | Actual data-flow map, country/route/provider-specific review of disclosure, consent, recording, retention/deletion, user rights, provider terms and distribution rules | BLOCKED BY JURISDICTION/ROUTE; no legal opinion claimed | Qualified review identifies obligations, controls, residual risks and launch conditions |
| G0-07 Product scope | Feature catalogue, MVP gate matrix, personas, exclusions, abuse cases, route-dependent features | DOCUMENT PREPARED; owner scope decision open | Each MVP feature is justified by user evidence, route feasibility, legal constraints and cost |
| G0-08 UX | Screen inventory, wireflows, error/fallback/disable/deletion paths, accessibility considerations and user feedback | DOCUMENT PREPARED; user validation incomplete | Critical journeys are reviewed with users and match the proven route and approved scope |
| G0-09 Requirements/traceability | Numbered functional/non-functional requirements, trace links, failure paths, privacy/security controls and verification strategy | DOCUMENT PREPARED; DRAFT; target decisions open | Every MVP requirement is testable, scoped, traced and either approved or explicitly deferred |
| G0-10 Acceptance thresholds | Owner-approved values or explicit rationale for non-applicability, supported configurations and measurement method | DOCUMENT PREPARED; proposed/open values remain unapproved | Thresholds are set before evaluation; safety/security zero-tolerance gates are not averaged away |
| G0-11 Architecture/API/data | Selected route-compatible architecture; API/data contracts; tenancy, idempotency, audit, deletion, retention, provider boundaries and failure recovery | DOCUMENT PREPARED; design depends on G0-04–G0-06 | Cross-document consistency review passes and open design choices are recorded |
| G0-12 Security and privacy engineering | Threat model, data inventory/lifecycle, capability allowlist, tenant isolation, abuse prevention, secret handling and incident response | DOCUMENT PREPARED; implementation/verification not done | Controls are mapped to requirements and test evidence planned; unresolved high risks have explicit treatment |
| G0-13 Cost and capacity | Shared workload assumptions, sensitivity analysis, route-specific quotes, peak assumptions, spend caps and unit economics | DOCUMENT PREPARED; economics unvalidated | Owner reviews low/base/high usage, margins, spend limits and a credible stop-loss plan |
| G0-14 Acquisition and pricing | Target segment, positioning hypothesis, pricing/willingness-to-pay evidence and low-cost acquisition plan | DOCUMENT PREPARED; no experiment results claimed | Pricing and acquisition are framed as evidence-backed decisions or clearly labelled pilot hypotheses |
| G0-15 Dependencies and licensing | Exact versions, direct/transitive licences, security/maintenance, model/provider terms, portability and lock-in assessment | FRAMEWORK PREPARED; exact-version review incomplete | Approved dependency/provider list and obligations are recorded before implementation |
| G0-16 Brand and distribution | Name/trademark/domain/app-store screening, country/region distribution constraints and support ownership | EVIDENCE REQUIRED; commercial brand unapproved | Owner approves a candidate after screening or explicitly defers brand selection with a safe working name |
| G0-17 Operating readiness | Support path, urgent disable, monitoring, audit, billing correctness, deletion, backup/restore, incident response, RTO/RPO and rollback criteria | DESIGN OPEN; operational tests not run | Pilot prerequisites, ownership and measurable recovery targets are defined and testable |
| G0-18 Final consistency review | Audit of README links, decision statuses, requirements/UX/API/data/security/pricing/roadmap alignment, assumptions and open risks | PARTIALLY MITIGATED; final audit still required | All P0 blockers resolved or explicitly accepted with rationale and limits; no hidden contradiction remains |
| G0-19 Owner baseline decision | Completed owner decision pack, evidence register, residual-risk list, approved MVP and release gates | OWNER DECISION REQUIRED | Each decision is recorded with status, rationale, evidence, conditions and date |
| G0-20 Implementation gate | Explicit owner message/decision authorising implementation scope, branch/workstream and first deliverable | NOT AUTHORISED | Explicit approval is recorded; otherwise code and deployment remain blocked |

## 4. Evidence that can be produced without experiments

These are documentation/research tasks that can continue without pretending field evidence exists:

- Audit source dates, URLs, claims, limits and confidence in the research register.
- Reconcile requirement, UX, API, data, threat-model, privacy, capacity and pricing references.
- Identify unresolved assumptions and show which decision each assumption affects.
- Review public product documentation, provider terms, official platform rules and exact dependency metadata where accessible.
- Prepare interview, route-test, quote-comparison and review templates.
- Improve accessibility, error-state, data-lifecycle, operational-readiness and support specifications.
- Validate repository links, stable IDs and status consistency.

These activities cannot establish actual demand, route success, all-in provider cost, legal advice, production latency, deletion behaviour or willingness to pay.

## 5. Evidence requiring separately approved external activity

- Customer interviews and concept/user validation with participants.
- Controlled telephony tests on explicitly scoped devices, SIMs, operators, plans and forwarding modes.
- Provider outreach that discloses project details, requests terms or seeks quotes.
- Any paid test, provider commitment, consultation or account activation that incurs cost.
- Counsel engagement and jurisdiction-specific legal review.
- Benchmarks, load tests, real-call pilots or collection of actual audio/transcripts.

Use the experiment approval checklist before each activity. A general “continue” instruction does not replace the scope, safety, consent and spend record required by that checklist.

## 6. Required owner review packet

Before baseline approval, present these items together:

1. One-page recommendation with the problem, initial user, use case and alternatives.
2. Evidence ledger that separates observed facts, source-backed claims, vendor statements, assumptions, hypotheses and unresolved unknowns.
3. Route decision with tested matrix, failure modes, disable/recovery evidence and supported-scope statement.
4. Comparable provider quotes and a fully scoped unit-economics model.
5. Jurisdiction-specific privacy/telecom/legal findings and open counsel questions.
6. Proposed MVP and explicit deferred/excluded features.
7. Approved or deliberately open requirements, acceptance thresholds, UX, API/data/security design and verification strategy.
8. Workload scenarios, peak assumptions, provider limits, spend caps and operating readiness.
9. Brand/acquisition/pricing hypotheses with the limits of current evidence.
10. Residual risk register, conditions, decision log and explicit choice: go, pivot, stop, or collect more evidence.

## 7. Current overall assessment

**Phase 0 status: INCOMPLETE.** The repository contains a broad draft discovery baseline and useful templates, but key decisions remain blocked by missing customer, telephony, provider, legal and cost evidence. Requirements and acceptance thresholds remain drafts, and the commercial brand and launch geography are not approved.

No interviews, live route tests, provider outreach/quotes, legal opinions, benchmarks, load tests or product implementation are claimed complete by this document.

## Related documents

- docs/governance/PHASE_0_RESIDUAL_RISK_REGISTER.md
- docs/governance/OWNER_DECISION_PACK.md
- docs/governance/BASELINE_CONSISTENCY_AUDIT.md
- docs/governance/DECISION_LOG.md
- docs/discovery/DISCOVERY_PLAN.md
- docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md
- docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md
- docs/discovery/MVP_SCOPE_AND_FEATURE_GATES.md
- docs/requirements/CORE_REQUIREMENTS_DRAFT.md
- docs/requirements/TRACEABILITY_MATRIX.md
- docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md
- docs/roadmap/ROADMAP.md
