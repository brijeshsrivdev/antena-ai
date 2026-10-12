# MVP Scope and Feature Gate Matrix

**Status:** Proposed scope-control draft; not owner-approved. Implementation is not authorised.

## Why this document exists

Do not copy every competitor feature into the first release before proving the call route, target segment, legal controls and unit economics. The matrix below narrows discovery decisions; it does not approve features.

## Gate 0 — Route feasibility

Before promising an incoming-call assistant, establish one supported route, the exact operator/device/plan matrix, caller-ID behaviour, failure handling, disable/recovery steps, written provider approval for the use case and itemised cost for all call legs and AI components.

**Stop condition:** If a safe, reliable and contractually supported route cannot be proven, do not build around an assumed route. Reconsider a hosted-number/VoIP-first or narrower screening/notification proposition as a separate product decision.

## Candidate core slice

| Capability | Scope / requirement mapping (draft) | Candidate disposition | Required evidence before release |
|---|---|---|
| Account, authentication and recovery | SCOPE-001; REQ-016, REQ-011 | Core candidate | Threat review, account isolation and recovery tests |
| Structured assistant profile/context | SCOPE-002/003; REQ-003 | Core candidate | Bounded schema, versioning, edit/delete and injection tests |
| Route setup, test, status and disable | SCOPE-004; REQ-001/002/014 | Mandatory for any route-based product | Controlled route tests and verified recovery |
| Caller AI disclosure and bounded conversation | SCOPE-006; REQ-004/010 | Mandatory for live calls | Approved policy and jurisdiction-specific legal review |
| Safe failure and escalation | SCOPE-005/006; REQ-004/006/014/015 | Mandatory for live calls | Tests for silence, media loss, urgent/out-of-scope requests and provider outage |
| Concise post-call summary | SCOPE-008; REQ-008 | Core-value candidate | Labelled factuality and uncertainty evaluation |
| Usage metering and hard spend/concurrency limits | SCOPE-013; REQ-009; NFR-006/007 | Mandatory for variable-cost service | Provider invoice reconciliation and quota-exhaustion tests |
| Privacy, data minimisation and deletion controls | SCOPE-014; REQ-010/013; NFR-005 | Mandatory foundation | Approved data-flow map and per-data-class lifecycle |
| Help, issue reporting and urgent disable | SCOPE-015; REQ-014/015 | Mandatory foundation | Recovery drill and incident escalation |
| Operational monitoring and response | REQ-015; NFR-004/009 | Mandatory foundation | Alerts, runbooks and safe diagnostics without raw content by default |

These are candidates, not permission to implement them.

## Conditional features

| Capability | Scope / requirement mapping (draft) | Default treatment | Gate |
|---|---|---|
| User takeover/transfer | SCOPE-007; REQ-007 | Conditional | Include only if end-to-end tests prove it on the advertised route |
| Expanded call history | SCOPE-009; REQ-013 | Limited initially | Validate user value and define retention |
| Full transcript | SCOPE-010; REQ-010/013 | Off unless separately approved | Privacy, retention, provider and cost decisions |
| Audio recording/playback | SCOPE-010; REQ-010/013 | Off unless separately approved | Legal review, clear notice and verified deletion |
| Contact-book sync | SCOPE-012; no direct REQ yet | Defer unless needed | User research and data-minimisation review; defer or add a requirement before inclusion |
| Follow-up reminders | SCOPE-011; no direct REQ yet | Later candidate | Begin with user-confirmed reminders; no autonomous external actions; defer or add a requirement before inclusion |
| Additional languages | SCOPE-016; REQ-006 | Evidence-gated | Advertise only combinations passing end-to-end tests |
| Paid plans/included minutes | SCOPE-013; REQ-009 | After quote and demand evidence | Route-specific cost and willingness-to-pay validation |

## Deferred or excluded from initial release

- Assistant-initiated outbound calling and outbound campaigns.
- Voice imitation of a real person.
- Autonomous payments, refunds, purchases or consequential commitments.
- Arbitrary client-defined connectors or executable tools.
- Legal/advocate profile.
- Hospitality actions before the corresponding Antena API capability is audited.
- Unlimited calling claims before cost tails and abuse controls are measured.
- International launch before country-specific route, provider, legal and store-policy review.

## Feature decision record

Every feature decision must record user problem/evidence, persona, route dependency, cost per use, data and privacy implications, failure behaviour, acceptance tests, disposition, decision owner and revisit trigger.

## Exit gate

Publish one versioned MVP list with included features, exclusions, supported route matrix, user-visible promises, usage limits, legal gates and measurable acceptance criteria. Map every item to the requirements and traceability matrix.

No feature is approved merely because it appears in this document.
