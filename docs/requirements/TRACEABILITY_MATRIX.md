# Initial Requirements Traceability Matrix

**Status:** Partial draft. IDs and priorities are provisional; full traceability is required before baseline approval.

| Requirement | Customer/product evidence | UX screen / flow | Architecture boundary | Risk references | Verification |
|---|---|---|---|---|---|
| REQ-001 Activation/routing state | Telephony feasibility; customer interviews pending | UX-007–UX-010; activation/deactivation | Android client, AI API, telephony adapter | THR-011, PRIV-013 | Routing-state and recovery tests |
| REQ-002 Route eligibility | Telephony feasibility; carrier tests pending | UX-007–UX-009 | Telephony adapter / routing status | THR-011 | Carrier/device/plan matrix |
| REQ-003 Profile/context | Product scope; interview evidence pending | UX-004–UX-005 | AI API/profile store | THR-005, THR-018 | Schema/versioning and injection tests |
| REQ-004 Disclosure/bounded conversation | Privacy/legal review pending | UX-002, UX-012 | Realtime worker, policy gateway | PRIV-001, PRIV-002, THR-013 | Scenario and legal-policy tests |
| REQ-005 Session lifecycle | Architecture draft | UX-012–UX-013 | Webhook adapter, session worker | THR-003, THR-004 | Replay/idempotency/state-machine tests |
| REQ-006 Realtime quality | Telephony feasibility; benchmarks pending | UX-012 | Media and speech/model adapters | THR-017 | Latency, interruption and fault tests |
| REQ-007 Takeover | Competitor review; route feasibility pending | UX-013 | Telephony/media adapter | THR-011, THR-017 | Transfer success/failure tests |
| REQ-008 Summary | Product scope; user value validation pending | UX-015 | Summary worker, persistence | THR-013, THR-008 | Factuality/uncertainty evaluation |
| REQ-009 Usage/cost | Pricing model; provider quotes pending | UX-018 | Usage ledger, billing adapter | THR-012 | Idempotency/reconciliation/limit tests |
| REQ-010 Privacy/retention | Privacy register; legal advice pending | UX-002, UX-019 | Data stores, deletion worker, providers | PRIV-001–PRIV-005, PRIV-011, PRIV-013 | Consent and end-to-end deletion tests |
| REQ-011 Tenant isolation | Architecture/threat model | UX-014–UX-020 | Auth/API/storage/tool gateway | THR-001, THR-002, THR-007 | Cross-tenant negative tests |
| REQ-012 Domain connectors | Antena API audit pending | Future domain-profile flow | Connector registry, Antena APIs | THR-006, THR-007 | Scope/tenant/idempotency tests |
| REQ-013 History/transcript/audio | Product scope; privacy/cost decision pending | UX-014–UX-016 | Data store/media store | PRIV-003, PRIV-005, THR-008, THR-010 | Access/retention/deletion tests |
| REQ-014 Support/urgent disable | Customer interviews pending | UX-009–UX-010, UX-021 | Control plane/support tools | THR-011, THR-015, THR-017 | Recovery and incident drills |
| REQ-015 Observability/recovery | Capacity model; SLOs pending | UX-010, UX-021 | Operations plane | THR-003, THR-012, THR-017 | Load, alert and recovery tests |

## Known traceability gaps

- Customer evidence is not yet available; interview plan exists, but interviews have not been conducted.
- Telephony/carrier feasibility is desk research only; no hands-on tests have been performed.
- UX inventory is not a validated wireflow or visual design.
- Architecture options are not decisions and provider choices are not approved.
- Acceptance criteria and non-functional thresholds remain incomplete.
- Legal/privacy conclusions require counsel review for selected jurisdictions and architecture.
- Detailed API schemas, data model, error taxonomy, threat mitigations and operational runbooks remain to be produced.
- Requirements IDs must be reconciled against the index and versioned before approval.

## Approval gate

The matrix is complete only when every requirement traces to evidence or a labelled hypothesis, UX, architecture/data/API, risks, test cases, release milestone and operational owner.