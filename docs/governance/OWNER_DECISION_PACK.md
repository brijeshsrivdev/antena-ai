# Owner Decision Pack — Discovery Baseline

**Status:** FOR OWNER REVIEW; no decision is implied by this document. Product implementation remains unauthorised.

## Purpose

Consolidate the choices that must be resolved before the discovery baseline can be approved. The repository's current direction is a working hypothesis, not an approved commercial or technical plan.

## Decisions requiring owner review

| ID | Decision | Current position | Evidence or action needed | Decision status |
|---|---|---|---|---|
| ODP-001 | Initial customer and problem | Personal AI call assistant is the leading hypothesis | Interview target users; identify high-value calls/tasks and willingness to pay | OPEN |
| ODP-002 | First geography | Not approved | Choose launch country; review carrier route, privacy, recording/disclosure, consumer and telecom obligations | OPEN |
| ODP-003 | Initial call route | Android-first candidate; cellular audio path unproven | Run controlled tests on selected SIM/device/operator/plan combinations; get written provider confirmation | BLOCKED BY EVIDENCE |
| ODP-004 | MVP scope | Candidate scope in MVP_SCOPE_AND_FEATURE_GATES.md | Approve only features supported by route, legal and user evidence; decide whether takeover/history/transcript are in scope | OPEN |
| ODP-005 | Architecture and providers | Managed, programmable-telephony and self-hosted options remain open | Compare route-specific quotes, all call legs, model/media, data terms, limits, support and exit costs | BLOCKED BY QUOTES/ROUTE |
| ODP-006 | Data and legal posture | Issue-spotting only; no legal opinion | Select jurisdiction and providers; obtain qualified review of notice, consent, retention, deletion, contracts and store policies | BLOCKED BY REVIEW |
| ODP-007 | Economics and pricing | ₹4/₹7/₹12 per-minute are sensitivity assumptions, not costs | Obtain comparable written quotes; test usage distribution and willingness to pay; model gross margin and spend caps | OPEN |
| ODP-008 | Service thresholds | Candidate values in ACCEPTANCE_THRESHOLD_REGISTER.md | Approve targets only after route/provider capabilities and test evidence are understood | OPEN |
| ODP-009 | Brand and acquisition | Commercial brand not selected or cleared | Screen trademark/domain/store names; run low-cost acquisition experiments after segment selection | OPEN |
| ODP-010 | Implementation authorisation | Explicit owner approval required | Review the completed baseline, risks, open decisions, scope, requirements, UX, architecture and launch gates | NOT AUTHORISED |

## Evidence that must not be represented as complete

- Customer interviews or demand validation.
- Owner-supervised route/device/carrier tests.
- Written, comparable provider quotes for the exact intended route.
- Jurisdiction-specific legal advice or provider contract review.
- Performance, reliability, cost, security or deletion benchmarks.
- Brand clearance, paid acquisition experiments or launch validation.

## Recommended approval sequence

1. Approve the discovery hypotheses and select a narrow interview segment, without authorising product code.
2. Run customer interviews and controlled route feasibility tests as separate, owner-approved experiments.
3. Obtain route-specific written provider quotes and legal issue review for the selected geography.
4. Update requirements, architecture, data lifecycle, UX, pricing and release gates from the evidence.
5. Review the consistency audit and unresolved risks; record explicit decisions in DECISION_LOG.md.
6. Only then decide whether to approve the baseline and separately authorise implementation.

## Owner decision record template

For each ODP item, record: **Decision / Status / Rationale / Evidence reviewed / Conditions / Date**. Use APPROVED only for an explicit owner decision. A recommendation, draft or test plan is not approval.

## Related documents

- docs/governance/DECISION_LOG.md
- docs/governance/BASELINE_CONSISTENCY_AUDIT.md
- docs/discovery/MVP_SCOPE_AND_FEATURE_GATES.md
- docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md
- docs/research/TELEPHONY_VALIDATION_PROTOCOL.md
- docs/research/VOICE_PROVIDER_RFP.md
- docs/research/PRIVACY_AND_REGULATORY_RISK_REGISTER.md


## Experiment governance update — 2026-10-12
Before any interviews, controlled call-route tests, provider outreach involving project details, or participant-based UX validation, use `docs/discovery/PHASE_0_EXPERIMENT_APPROVAL_CHECKLIST.md` and obtain explicit owner approval for that exact scope. The checklist does not itself approve fieldwork. It does not change decision statuses or authorize product implementation.


## Phase 0 exit review
Use `docs/governance/PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md` as the consolidated gate checklist when reviewing this decision pack. It distinguishes draft documents from observed evidence and makes the baseline approval and implementation authorisation separate decisions. Current status remains incomplete; no decision is implied.
