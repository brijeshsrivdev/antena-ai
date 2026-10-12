# Cross-Document Consistency Review — Discovery Baseline

**Status:** Desk-only review; not owner-approved and not a baseline approval. Date: 2026-10-12.  
**Scope:** Requirements, UX inventory/wireflows, MVP scope gates, API/data/state contracts, security/privacy, acceptance thresholds, verification mapping, Phase 0 evidence and governance.

## 1. Executive result

The current documents are **more internally aligned, but the discovery baseline is not ready for owner approval or implementation**. This review found several semantic distinctions are now represented consistently in draft contracts and UX guidance. A small remaining traceability gap for platform permissions and notifications was corrected in the traceability matrix during this pass.

No product code or executable prototype was created. No interviews, live route tests, provider outreach, quotes, legal opinions, benchmarks, load tests, deletion exercises or security tests are claimed complete. Documentation consistency cannot prove route feasibility, market demand, provider economics, legal sufficiency, runtime behavior or release readiness.

## 2. Review method and limits

Reviewed the current branch versions of:
- `CORE_REQUIREMENTS_DRAFT.md`, `TRACEABILITY_MATRIX.md`, `ACCEPTANCE_THRESHOLD_REGISTER.md`;
- `UX_SCREEN_INVENTORY.md`, `UX_WIREFLOW_SPEC.md`, `MVP_SCOPE_AND_FEATURE_GATES.md`;
- `API_CONTRACT_DRAFT.md`, `DATA_MODEL_DRAFT.md`, `STATE_AND_EVENT_CONTRACTS_DRAFT.md`;
- `THREAT_MODEL.md`, `PRIVACY_AND_REGULATORY_RISK_REGISTER.md`, `CAPABILITY_GOVERNANCE.md`;
- `REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md`, `DELETION_AND_VERIFICATION_RECONCILIATION.md`, `PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md`, `PHASE_0_RESIDUAL_RISK_REGISTER.md`, `OWNER_DECISION_PACK.md`, `DECISION_LOG.md` and related governance records.

Checks included identifier-presence comparison, semantic state/wording review, candidate threshold cross-checks, documentation table-shape checks on the touched reconciliation files, and targeted link/index checks. This is a manual desk review plus bounded consistency checks, not a full automated link crawler, external-source freshness review, formal threat assessment, independent code review or test execution.

## 3. Consistency findings

| ID | Area | Finding | Disposition in this pass | Remaining status |
|---|---|---|---|---|
| CDR-001 | Requirement inventory | REQ-001–REQ-016 and NFR-001–NFR-010 are present in both the core requirement draft and traceability matrix. | Verified by identifier-presence check. | Draft and unapproved; semantic acceptance review still required. |
| CDR-002 | Product scope | SCOPE-001–SCOPE-021 have crosswalk entries. SCOPE-011 (tasks/reminders) and SCOPE-012 (caller/contact rules) have no dedicated requirement. | Existing scope records correctly say defer or draft/review explicit requirements before inclusion. | Must stay out of an approved MVP until decided. |
| CDR-003 | Platform permissions | UX-006 existed in the UX inventory but was not directly mapped in the traceability matrix. | Added conditional mapping to REQ-001/REQ-002. A permission grant does not prove route eligibility or verified routing. | Actual permissions/roles depend on selected platform and route. |
| CDR-004 | Notifications/status | UX-022 needed an explicit requirements trace for stale state, permission/notification status and private notification content. | Added mapping to REQ-001/REQ-015. | Notification delivery is not authoritative route-state evidence; privacy and behavior need later validation. |
| CDR-005 | Route lifecycle | UX, API and state contracts distinguish setup requested, verification pending, verified-active, degraded, disable requested and restoration unverified. | Draft vocabulary is aligned; claims are constrained to authoritative evidence. | Actual state transitions and restoration depend on route/provider tests; route remains unproven. |
| CDR-006 | Call lifecycle | The model distinguishes a user-visible CallSession from ProviderLeg records; API/state drafts discuss duplicate, delayed and out-of-order callbacks. | Conceptual representation is aligned. | Provider event IDs, signature semantics, terminal-state precedence and billable leg mapping remain unknown. |
| CDR-007 | Disclosure and consent | Account-holder choices, caller disclosure events and legal consent are distinguished across the data model, API, privacy and UX docs. | Conceptual distinction is consistent. | Route-specific disclosure and lawful processing require selected geography/route and qualified review. No legal conclusion is made. |
| CDR-008 | Deletion | DeletionRequest is separate from per-target outcomes; UX and API avoid equating primary-row removal with full deletion. | Added a data-class target map, candidate target outcomes, role model and future evidence plan in `DELETION_AND_VERIFICATION_RECONCILIATION.md`. | Retention, provider deletion, backup expiry, exceptions, SLA and named owners remain open. |
| CDR-009 | Usage and billing | Usage corrections are intended as linked immutable events; internal ledger and provider invoice reconciliation are separate. | State, data and verification docs align on the principle. | Billable units, rounding, multiple legs, failed-call charges, provider quotes and invoice evidence remain open. |
| CDR-010 | Account vs tenant | Personal account ownership is not treated as hospitality tenant authority; future connector execution is server-authorized and scoped. | Architecture/capability drafts align on this boundary. | Hospitality connector membership/delegation matrix remains future scope and must not be part of the personal-assistant critical path. |
| CDR-011 | Threshold source of truth | The acceptance threshold register is the canonical place for candidate numeric thresholds and their status. | Verification crosswalk now names applicable AT IDs and records current statuses without inventing values. | No threshold is owner-approved; proposed values require explicit decisions and predeclared evidence. |
| CDR-012 | Verification claims | Documents distinguish prepared plans from executed tests and evidence. | Full REQ/NFR verification crosswalk added; no run evidence is claimed. | All tests, benchmarks, restore/deletion exercises and security tests remain NOT RUN. |
| CDR-013 | Phase gates | Phase 0 baseline approval, implementation authorization and pilot approval are separate decisions. | Roadmap, exit map, owner pack and handover retain separate gates. | Phase 0 remains incomplete; implementation and fieldwork remain unauthorized without activity-specific approval. |
| CDR-014 | Brand and launch geography | Repository name is not a commercial brand decision; launch geography remains open. | Consistent with decision log and owner decision pack. | Brand clearance and jurisdiction selection remain open. |

## 4. Acceptance-threshold reconciliation

The current threshold register remains authoritative. The reconciliation artifact references the thresholds without setting competing values:

- **PROPOSED:** AT-001, AT-002, AT-004, AT-005, AT-006, AT-007 and the control aspect of AT-011.
- **OPEN:** AT-003, AT-008, AT-009, AT-010 and AT-012; AT-011 spend amounts are also open.

These statuses are copied from the current register for review, not approved by this document. Do not treat a proposed target as a release gate or an open target as zero, unlimited or implicitly accepted. Record any future owner decision in the canonical register and decision log.

## 5. Current release blockers

The following are evidence/decision blockers, not mere missing documentation:

1. **Route feasibility and user control:** no controlled device/operator/plan/SIM route matrix or verified restoration evidence.
2. **Customer/problem validation:** no interviews or willingness-to-pay evidence.
3. **Provider fit and economics:** no comparable written route-specific quotes or invoice-reconciled cost model.
4. **Jurisdiction, disclosure and privacy:** no selected launch jurisdiction and no qualified legal review for the actual route/provider/data flows.
5. **Data lifecycle:** no approved retention schedule, deletion SLA, backup expiry, provider deletion evidence or exception policy.
6. **Operational readiness:** no named owners/on-call model, runbook exercise, restore drill, approved RTO/RPO or tested disable path.
7. **Threshold and quality evidence:** candidate thresholds remain proposed/open; no runtime, load, reliability, factuality or security evidence.
8. **Owner decisions:** initial segment, geography, route, scope, provider, brand and baseline have not all been approved.

Consult `PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md`, `PHASE_0_RESIDUAL_RISK_REGISTER.md` and `OWNER_DECISION_PACK.md` for the gate-by-gate evidence and decisions.

## 6. Required next steps

### Desk-only, no external activity
- Preserve this review and the new UX traceability clarification in the branch.
- If another documentation pass is requested, focus on requirement acceptance-criteria testability and exact requirement-to-failure-case links; label any unresolved acceptance criteria rather than inventing a target.
- Keep README, current state, handover, traceability and the canonical threshold register synchronized.

### Requires separate owner approval
- Customer interviews and other participant research.
- Live route/device/carrier tests.
- Provider outreach, quotes or commercial negotiations.
- Spending, subscriptions or paid experiments.
- Any legal advice/opinion engagement.
- Product implementation, deployment, pilot or public launch.

## 7. Merge and implementation recommendation

**Recommendation: do not merge this draft as an approved product baseline and do not begin implementation.** The branch contains useful discovery artifacts, but the remaining evidence blockers are material. Any later merge of the documentation branch is a separate owner-controlled review decision; this document does not authorize a merge.

## Related documents

- [Requirement-to-contract coverage audit](REQUIREMENT_CONTRACT_COVERAGE_AUDIT.md)
- [Deletion and verification reconciliation](DELETION_AND_VERIFICATION_RECONCILIATION.md)
- [Phase 0 exit criteria and evidence map](PHASE_0_EXIT_CRITERIA_AND_EVIDENCE_MAP.md)
- [Phase 0 residual risk register](PHASE_0_RESIDUAL_RISK_REGISTER.md)
- [Owner decision pack](OWNER_DECISION_PACK.md)
- [Acceptance threshold register](../requirements/ACCEPTANCE_THRESHOLD_REGISTER.md)
- [Requirements traceability matrix](../requirements/TRACEABILITY_MATRIX.md)
