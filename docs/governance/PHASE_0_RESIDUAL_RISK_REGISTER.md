# Phase 0 Residual Risk Register

**Status:** DRAFT — owner review required. This register records risks and required evidence; it does not accept risks on the owner's behalf.  
**Snapshot:** 2026-10-12.  
**Boundary:** Documentation only. No fieldwork, implementation or deployment is authorised by this register.

## Scoring guidance

- **Severity:** Critical / High / Medium / Low based on potential product, user, legal, financial or operational consequence.
- **Likelihood:** Unknown / Likely / Possible / Unlikely. Use Unknown where there is insufficient evidence; do not imply a measured probability.
- **State:** OPEN / BLOCKED / MITIGATION PREPARED / OWNER ACCEPTANCE REQUIRED / CLOSED.
- A risk is not CLOSED because a document or proposed control exists. Closure needs evidence and an explicit review outcome.

## Active risks

| ID | Risk / consequence | Severity | Likelihood | State | Existing mitigation / reference | Evidence or decision required to reduce risk | Owner decision / stop condition |
|---|---|---|---|---|---|---|---|
| RSK-001 | Proposed call route cannot deliver usable two-way audio or reliable incoming-call handling on intended devices/operators; product premise may fail | Critical | Unknown | BLOCKED | ANDROID_CALL_ROUTE_DECISION.md; TELEPHONY_VALIDATION_PROTOCOL.md; PHASE_0_EVIDENCE_WORKBOOK.md | Controlled, scoped route tests; caller-ID/failure/disable evidence; written provider support | Stop route-specific architecture and product promises if unsupported, unsafe or not reversible |
| RSK-002 | Calls are lost, forwarded unexpectedly or remain forwarded after user believes assistant is off | Critical | Unknown | OPEN | REQ-001/002; route test protocol; experiment approval checklist | Prove disable/recovery for every supported configuration; define failure and manual recovery UX | No real-call pilot if deactivation cannot be verified or normal calling cannot be restored |
| RSK-003 | Target users do not have frequent/severe enough pain or will not complete setup/pay | High | Unknown | OPEN | CUSTOMER_INTERVIEW_PACK.md; MARKET_DEMAND_AND_SEGMENTATION.md; GTM_EXPERIMENT_PLAN.md | Interview evidence on recent incidents, alternatives, trust, setup willingness and price | Pivot or stop if no segment demonstrates material need and credible adoption path |
| RSK-004 | Actual variable costs exceed feasible pricing, causing negative contribution margin or unbounded spend | Critical | Unknown | BLOCKED | COST_SCENARIO_MODEL.md; WORKLOAD_SCENARIO_BASELINE.md; VOICE_PROVIDER_RFP.md | Comparable written quotes, measured billable legs, usage distribution, caps and failed-call billing | No included-minute/unlimited promise or paid pilot without reviewed spend cap and unit economics |
| RSK-005 | Product route or call handling breaches telecom, privacy, recording/disclosure, consumer or app distribution requirements | Critical | Unknown | BLOCKED | PRIVACY_AND_REGULATORY_RISK_REGISTER.md; ANDROID_CALL_ROUTE_DECISION.md; DPDP/TRAI source notes | Select geography/route/provider; qualified jurisdiction-specific legal review and contract review | No real-call customer pilot or public distribution before required review and controls |
| RSK-006 | Call audio, transcripts, summaries or personal context are retained, exposed or used outside user expectations | Critical | Unknown | OPEN | DATA_INVENTORY_AND_LIFECYCLE.md; THREAT_MODEL.md; CORE_REQUIREMENTS_DRAFT.md | Confirm provider retention/training terms; data-flow and deletion proof; least privilege and incident plan | Do not collect real call content until purpose, access, retention, deletion and disclosure are reviewed |
| RSK-007 | AI fabricates facts, makes commitments, mishandles urgent/sensitive calls or performs actions beyond scope | Critical | Possible (unvalidated) | OPEN | CAPABILITY_GOVERNANCE.md; VOICE_AGENT_EVALUATION_PLAN.md; MVP_SCOPE_AND_FEATURE_GATES.md | Adversarial/synthetic evaluation, bounded policy, refusal/escalation tests, disclosure and safety review | Any unauthorised external action or unsafe routing is a stop/release-blocking event |
| RSK-008 | Caller believes they are speaking to the user or misunderstands AI disclosure/recording | High | Unknown | OPEN | REQ-004; PRIVACY_AND_REGULATORY_RISK_REGISTER.md; UX_WIREFLOW_SPEC.md | User-tested disclosure and counsel-approved wording for actual jurisdiction/use | No live pilot until disclosure and notice are approved and tested |
| RSK-009 | Provider outages, webhook replay/order, transfer failure or latency degrade or silently terminate calls | High | Unknown | OPEN | API_CONTRACT_DRAFT.md; VOICE_AGENT_EVALUATION_PLAN.md; ACCEPTANCE_THRESHOLD_REGISTER.md | Provider semantics, fault-injection/controlled tests, measured p50/p95/p99, recovery and duplicate-event handling | No SLA/reliability claims until measured; silent call loss blocks release |
| RSK-010 | Cross-user/tenant data leakage or untrusted profile/caller prompt injection invokes forbidden capability | Critical | Possible (design risk; not measured) | MITIGATION PREPARED | THREAT_MODEL.md; CAPABILITY_GOVERNANCE.md; TRACEABILITY_MATRIX.md | Threat review, authorization matrix, isolation and adversarial tests before release | Zero tolerance for unauthorized cross-tenant access or actions outside allowlist |
| RSK-011 | Proposed concurrency and capacity estimates understate peaks or provider limits | High | Unknown | OPEN | WORKLOAD_SCENARIO_BASELINE.md; CAPACITY_AND_SCALE_MODEL.md | Validate actual traffic distribution, peak multiplier, provider CPS/concurrency and load test plan | No capacity promise until assumptions and provider limits are confirmed |
| RSK-012 | Data deletion claims are inaccurate because provider copies, backups, logs or legal retention remain | High | Unknown | OPEN | DATA_INVENTORY_AND_LIFECYCLE.md; AT-008 | Provider written terms, per-store deletion workflow, backup expiry, audit evidence and counsel review | Do not promise a deletion SLA until each data store and exception is mapped |
| RSK-013 | Public competitor claims or prices are misread as verified capabilities or comparable total costs | Medium | Possible | MITIGATION PREPARED | COMPETITOR_MATRIX.md; PROVIDER_PRICING_EVIDENCE.md; RESEARCH_REGISTER.md | Verify current source dates/terms and label vendor claims vs observed tests/quotes | No comparative “cheaper/better/reliable” claim without like-for-like evidence |
| RSK-014 | Commercial brand conflicts with existing marks, domains, stores or products | Medium | Unknown | OPEN | DEC-009; OWNER_DECISION_PACK.md | Trademark/domain/app-store screening in intended geography | Do not treat repository name as a cleared commercial brand |
| RSK-015 | Scope expands to hospitality or legal/professional profiles before core route and capability governance are validated | High | Possible | MITIGATION PREPARED | MVP_SCOPE_AND_FEATURE_GATES.md; CAPABILITY_GOVERNANCE.md; DEC-006 | Keep domain profiles deferred; audit trusted Antena APIs and per-action permissions before any connector work | No unvalidated domain action or direct database access |
| RSK-016 | Proposed requirements/thresholds are mistaken for approved release gates or implemented inconsistently | High | Possible | MITIGATION PREPARED | CORE_REQUIREMENTS_DRAFT.md; TRACEABILITY_MATRIX.md; ACCEPTANCE_THRESHOLD_REGISTER.md; PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md | Reconcile lifecycle wording, validate ID coverage and approve each applicable threshold before testing | No implementation from draft requirements; owner approval and traceability required |
| RSK-017 | Open-source/provider licence, transitive dependency, model terms or data-processing restrictions are discovered after design commitment | High | Unknown | OPEN | OPEN_SOURCE_AND_PROVIDER_EVALUATION.md; VOICE_STACK_CANDIDATE_REVIEW.md | Exact version/SBOM review, transitive licences, model and provider terms, security/maintenance review | No dependency approval based on repository licence file alone |
| RSK-018 | Support, incident response, urgent disable, billing dispute, backup/restore or rollback is not operable at pilot time | High | Unknown | OPEN | VERIFICATION_AND_TEST_STRATEGY.md; UX_SCREEN_INVENTORY.md; AT-009 | Assign operational ownership; define support path, recovery targets, audit and runbooks; test before pilot | No external pilot without tested disable, support and incident response |

## Top risk priority order

1. **RSK-001 / RSK-002 — Route feasibility and user control.** They can invalidate the product premise or create direct user harm.
2. **RSK-004 / RSK-005 — All-in economics and legal/telecom posture.** They can make the service commercially or legally non-viable.
3. **RSK-003 — Customer/problem validation.** Avoid investing in a technically feasible but unwanted product.
4. **RSK-006 / RSK-007 / RSK-008 / RSK-010 — Privacy, AI safety, disclosure and authorization.** These require design controls plus evidence, not just policy text.
5. **RSK-009 / RSK-011 / RSK-012 / RSK-018 — Reliability and operations.** These need route/provider evidence and later controlled verification.
6. Remaining market, brand, dependency and scope risks must be resolved before final baseline acceptance or explicitly deferred with rationale.

## Review protocol

For each risk at review, record: evidence inspected; current likelihood/severity and rationale; affected requirements/decisions; mitigation owner; due condition; residual risk; and explicit owner disposition (accept, mitigate, transfer, avoid, or keep blocked). Do not mark risk accepted without an owner decision. Do not mark risk closed on the strength of a plan alone.

## Known limits

This is a structured discovery risk register, not a quantitative risk model, legal opinion, security certification or proof that any control has been implemented or tested. Likelihood values are mostly Unknown because the relevant field evidence has not been collected.

## Related documents

- docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md
- docs/governance/BASELINE_CONSISTENCY_AUDIT.md
- docs/governance/OWNER_DECISION_PACK.md
- docs/governance/DECISION_LOG.md
- docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md
- docs/requirements/TRACEABILITY_MATRIX.md
- docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md
- docs/research/PRIVACY_AND_REGULATORY_RISK_REGISTER.md
