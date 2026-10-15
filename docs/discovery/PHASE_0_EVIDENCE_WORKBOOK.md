# Phase 0 Evidence Workbook — Fieldwork Preparation

**Status:** Preparation template only. No interviews, telephony experiments, provider outreach, quotes, legal review or benchmarks have been completed. Do not begin experiments until the owner approves the protocol, participants, safety boundaries and success criteria.

## How to use this workbook

1. Copy the relevant blank record into a private research workspace for each activity; do not store participant identities or real telephone numbers in this public repository.
2. Use pseudonymous IDs and collect only information necessary for the research question.
3. Record negative results, failures, uncertainty and contradictory evidence as carefully as positive results.
4. Keep observations separate from interpretations and product decisions.
5. Update the research register and decision log only after evidence has been reviewed; never convert an assumption to a fact because a test passed once.

## Workstream A — Customer problem interviews

**Recommended first round:** 12–18 qualitative interviews across three or four distinct segments, as proposed in CUSTOMER_INTERVIEW_PACK.md. This is exploratory, not statistically representative.

### Participant record (one row per pseudonymous participant)

| Field | Entry |
|---|---|
| Participant ID | P-___ |
| Segment hypothesis | Small service business / inbound sales / support-intake / hospitality (separate cohort) / other |
| Recruitment source |  |
| Interview date |  |
| Consent for notes | Yes / No — stop if no |
| Recent concrete incident |  |
| Frequency and consequence |  |
| Existing workaround and spend |  |
| Calls that must never be delegated |  |
| Trust/control requirements |  |
| Price reaction (after open-ended questions) |  |
| Willingness to configure a test route | Yes / No / Conditional; reason |
| Contradictory/negative evidence |  |
| Researcher confidence | Low / Medium / High; why |
| Follow-up permission | Yes / No |

Do not record audio by default. Do not put names, phone numbers, contact lists, call contents or identifiable quotes in this workbook. If a quote is useful, de-identify it and obtain permission for that use.

### Segment synthesis (complete after interviews)

| Segment | n | Recent problem examples | Severity/frequency | Existing spend/workaround | Trust/setup blockers | Pilot intent | Evidence quality | Decision implication |
|---|---:|---|---|---|---|---|---|---|
| Segment A | 0 | — | — | — | — | — | Not collected | No conclusion |
| Segment B | 0 | — | — | — | — | — | Not collected | No conclusion |
| Segment C | 0 | — | — | — | — | — | Not collected | No conclusion |

Do not rank segments by enthusiasm alone. Look for repeated recent incidents, material consequences, unsatisfactory alternatives, a credible route to reach the segment and willingness to undertake the setup needed by the actual product.

## Workstream B — Telephony feasibility

**Preconditions:** owner approval; consenting test participants; dedicated test SIMs/numbers; written test plan; baseline call behaviour documented; immediate disable and restoration path confirmed; no sensitive or production calls.

### One test run per row

| Field | Entry |
|---|---|
| Test ID | TEL-___ |
| Date/time and timezone |  |
| Device model / OS build |  |
| Operator / plan class |  |
| SIM slot / network state |  |
| Forwarding type and setup steps |  |
| Provider and destination type |  |
| Expected outcome |  |
| Actual outcome |  |
| Route outcome | Pass / Fail / Ambiguous |
| Caller ID outcome |  |
| Connect / first-audio / takeover timings |  |
| Call duration and each billable leg |  |
| Charges and billing evidence |  |
| Fallback / voicemail interaction |  |
| Disable and normal-call restoration verified | Yes / No |
| Consent and test safety confirmed | Yes / No |
| Evidence reference (sanitised) |  |
| Failure classification / notes |  |

### Route result summary

| Configuration ID | Attempts | Intended route successes | Failures | Ambiguous | Caller ID understood? | Disable verified? | Cost evidence complete? | Provider confirmed in writing? |
|---|---:|---:|---:|---:|---|---|---|---|
| CFG-001 | 0 | 0 | 0 | 0 | No data | No data | No data | No |

Report numerator and denominator for every claimed configuration. Do not pool different carriers, forwarding types or device setups to hide failures. A pass on one setup does not prove general support. Any unexpected call loss, unverified disable or unsafe routing pauses testing pending review.

## Workstream C — Provider quote comparison

Send the same VOICE_PROVIDER_RFP.md questionnaire to each candidate only after owner approval. Record written responses; do not infer consumer-use support from a provider's generic voice-agent product.

| Item | Provider A | Provider B | Provider C |
|---|---|---|---|
| Exact proposed business phone-assistant use expressly supported? | Not requested | Not requested | Not requested |
| Supported operators/forwarding modes | Unknown | Unknown | Unknown |
| Caller ID behaviour | Unknown | Unknown | Unknown |
| Transfer/takeover behaviour | Unknown | Unknown | Unknown |
| Itemised inbound/outbound/forwarding legs | No quote | No quote | No quote |
| Media/STT/TTS/model charges | No quote | No quote | No quote |
| Minimums, pulse, failed-call billing, taxes | No quote | No quote | No quote |
| Concurrency/CPS and rate limits | Unknown | Unknown | Unknown |
| Data locations, subprocessors, retention/deletion | Unknown | Unknown | Unknown |
| Contractual restrictions / termination | Unknown | Unknown | Unknown |
| Quote date / validity | — | — | — |
| Evidence link | — | — | — |

Do not compute a winner until quotes describe comparable components and the intended route. Keep vendor assertions distinct from contract language and observed test results.

## Workstream D — Evidence-to-decision log

| Evidence ID | Observation (fact) | Interpretation (hypothesis) | Counter-evidence / uncertainty | Requirement or decision affected | Next test / owner | Status |
|---|---|---|---|---|---|---|
| EV-001 | No evidence collected | None | All major assumptions remain open | ODP-001 / ODP-003 / ODP-005 | Owner to approve fieldwork | OPEN |



## Workstream E — Business workflow discovery and segment comparison

Use only after owner approval of the interview scope. Do not put participant identities or raw customer data in this public repository.

| Evidence ID | Segment hypothesis | Participant role (buyer/operator) | Recent workflow incident | Calls per day/week (range + basis) | Current workaround/system | Consequence/cost evidence | Candidate bounded workflow | Buyer/budget signal | Trust/privacy constraints | Route/connector dependencies | Counter-evidence | Confidence / next action |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| BIZ-001 | TBD | TBD | Not collected | TBD | TBD | TBD | TBD | TBD | TBD | TBD | TBD | OPEN |

For each candidate workflow, record the start event, required fields, protected data, verification need, authorized action, success condition, failure/unknown states, human fallback and system of record. Do not assume ticket creation, missed-call coverage or transfer support.

## Workstream F — Business route, event coverage and connector contract

Complete only after separate owner approval, a selected candidate segment/workflow and provider shortlist. No provider outreach or live route testing is authorized by this template.

| Evidence ID | Route/provider candidate | Number/route model | Call connection/media evidence | Provider/carrier event coverage | Caller-ID behavior | Missed-before-connection observability | Handoff support/evidence | Disable/recovery evidence | Connector/action dependency | Written terms/quote | Unknowns / stop condition | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| ROUTE-BIZ-001 | TBD | TBD | Not tested | Unknown | Unknown | Unknown | Unknown | Not tested | TBD | No quote | Do not promise coverage or activate route | BLOCKED |

For any connector proposed by the workflow, record operation name/version, typed input/output, organization scope, permission source, required confirmation, idempotency key, timeout/retry behavior, authoritative success source, ambiguous-result reconciliation, data retained and cost basis. A connector timeout is not automatically a failure or success.

## Suggested sequencing and stop conditions

1. Confirm the first interview segment and recruitment approach. Conduct interviews without selling the concept until recent behaviour has been explored.
2. Separately approve a small, reversible telephony test using controlled test numbers and consenting participants.
3. If the call route is unsupported, unreliable, not reversible, or not contractually allowed, stop and reassess the product promise before investing in the chosen stack.
4. Request comparable written quotes from at least two providers for the route that passed initial feasibility.
5. Recalculate cost using measured usage and all billable legs; keep assumptions labelled until invoices/quotes validate them.
6. Review jurisdiction and data-flow questions with qualified counsel before any real-call pilot.
7. Record explicit go/no-go decisions in DECISION_LOG.md and OWNER_DECISION_PACK.md.

## Related repository documents

- docs/discovery/CUSTOMER_INTERVIEW_PACK.md
- docs/research/TELEPHONY_VALIDATION_PROTOCOL.md
- docs/research/VOICE_PROVIDER_RFP.md
- docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md
- docs/governance/OWNER_DECISION_PACK.md
- docs/governance/DECISION_LOG.md

## Provider outreach email template (draft; send only after owner approval)

**Subject:** Request for written feasibility and pricing — AI business phone assistant

Hello,

We are evaluating a potential AI business phone assistant during discovery only. No production deployment or customer traffic is planned at this stage, and no provider has been selected.

The current product hypothesis is a business-configured inbound call workflow: callers interact with an AI assistant over a supported business-number route, and authorized business users review call outcomes and any confirmed actions. The first business segment/workflow and any ticket/CRM connector remain undecided. We need to understand whether your terms and platform support the specific route and workflow we may select.

Could you please provide written answers to the following, separating contractual commitments from general product capabilities?

1. Which business-number models are supported for inbound calls (hosted number, forwarding, SIP/PBX or other), in which countries/operators, and under what KYC/contract restrictions?
2. For each supported route, which call lifecycle/media events are exposed (ringing/offered, connected, abandoned, failed, missed before assistant connection, transfer/handoff, disconnected), with event IDs, timestamps, retries, ordering and reconciliation behavior?
3. What caller-ID information is preserved and what are the known limitations? Can missed-call visibility be guaranteed for calls that never connect to the assistant? If not, please state the precise coverage boundary.
4. What real-time media/streaming capabilities, codecs, latency characteristics, concurrency/CPS limits and failover behavior are contractually supported?
5. What transfer/handoff mechanisms exist, and what authoritative events confirm success, failure or timeout?
6. Please provide itemized pricing for numbers, inbound/forwarding/bridge/transfer legs, media streaming, STT/TTS/model usage, recording/transcription, failed calls, billing pulse/rounding, taxes, minimum commitments, overages and support.
7. What data locations, subprocessors, retention/deletion behavior, training use, security documentation, incident notification and contractual data-processing terms apply?
8. What typed APIs/connectors, authentication scopes, idempotency controls, webhook security and authoritative action-result/reconciliation interfaces are available? Please do not assume a generic ticket/CRM connector is in scope.
9. Are sandbox/test numbers available for a small, controlled feasibility test using consenting test participants, and what approval or spend limits apply?
10. Please state quote validity, cancellation/exit terms, service/support commitments and all excluded charges.

Please include example pricing for a clearly stated low/base/high workload only if each scenario's assumptions and excluded costs are shown. We do not yet have approved business workload values, so do not treat 10,000 registered users as a concurrency specification.

Thank you,
Product Discovery Team

---

Do not send this email or share project/business details until the owner approves the provider shortlist and exact outreach scope. A response is evidence of a vendor statement, not proof of capability; contract review and controlled tests remain necessary.
