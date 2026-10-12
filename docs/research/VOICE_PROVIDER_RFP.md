# Voice Provider RFP and Evaluation Scorecard

**Status:** Request template only. No request has been sent and no quote received. Published price pages do not establish supplier approval.

## Purpose
Collect comparable written responses for the exact intended route, rather than comparing headline prices that include different components. Send the same questions to each candidate.

## A. Proposed use case
We are evaluating an India-first AI call assistant. Depending on route feasibility, calls may arrive via conditional forwarding or a hosted number. The service may stream audio to a real-time AI agent, disclose its AI role, capture caller intent, and deliver a summary to the account holder. Any business/hospitality use will be separately scoped. We are not requesting support for emergency, OTP, financial authentication or deceptive impersonation use cases.

Provider must explicitly state whether this use is supported under its service terms and applicable local rules.

## B. Mandatory route questions
1. Which Indian mobile operators and prepaid/postpaid combinations are supported?
2. Which forwarding types work: unconditional, busy, no-answer, unreachable? Are there carrier restrictions or separate charges?
3. Can the provider accept forwarded calls and preserve original caller ID? If not, what number is shown?
4. Can the assistant transfer/take over a call to the account holder or another destination? Describe exact call legs and caller experience.
5. What happens if the destination, media stream, model or provider is unavailable?
6. Is consumer personal-call-assistant use expressly allowed? Cite relevant contractual terms.
7. Are numbers, KYC, telecom resources or business registration required? Are hosted-number restrictions relevant?

## C. Commercial pricing worksheet
Provide itemised prices and currency:
- Inbound call leg and outbound leg by destination.
- Forwarded call, bridge, conference and transfer legs.
- Number rental, setup, KYC, deposits and minimum monthly commitment.
- Billing pulse and rounding; minimum billable duration.
- Failed, unanswered, busy, rejected and short calls.
- Recording, streaming, transcription, speech generation, model orchestration and storage.
- Concurrent sessions, calls-per-second, overage and rate-limit fees.
- Taxes, currency conversion and pass-through carrier charges.
- Quote the shared canonical workload scenarios from `../architecture/WORKLOAD_SCENARIO_BASELINE.md`: 20,000 / 150,000 / 600,000 connected minutes per month. Separately, if useful, quote the alternate 10,000 / 75,000 / 240,000-minute sensitivity set in `../business/COST_SCENARIO_MODEL.md`; label the two sets distinctly and do not mix them.
- Price validity, termination, notice and committed-spend terms.

For each scenario, return an estimated invoice and state excluded items. Do not bundle unpriced components into “included” without limits. The canonical shared workload scenario is the default comparison set across providers; retain the alternate sensitivity set only as a separately labelled comparison.

## D. Technical and operational questionnaire
- Real-time media protocol, codec, sample rate, echo cancellation and DTMF support.
- Media setup latency, p50/p95 latency, jitter/drop metrics and published SLOs.
- Webhook signing, timestamp/replay protection, retries and idempotency.
- Regional media locations and data residency options.
- Concurrency/CPS limits and process for increasing them.
- Status page, incident communication, support hours and escalation.
- Call detail records, per-leg correlation IDs and export format.
- Sandbox, test numbers and controlled calls without real customers.
- SLA, credits, maintenance and termination assistance.

## E. Privacy, security and legal questions
- Controller/processor roles for audio, transcript, caller metadata, summaries and telemetry.
- Processing locations, subprocessors, cross-border transfers, retention defaults and deletion timelines.
- Whether data is used to train or improve models; opt-out or contractual guarantees.
- Encryption, access controls, audit logs, vulnerability disclosure, certifications and incident notification.
- Consent/disclosure responsibilities for all call parties and the customer's role.
- Assistance with telecom, privacy and commercial-communications obligations.
- Data export and deletion verification, including backups and logs.
- DPA, terms, privacy policy, subprocessor list and security documentation before production.

## F. Evaluation scorecard

| Criterion | Weight | Evidence required |
|---|---:|---|
| Exact route and use-case support | 20% | Written contractual confirmation plus successful controlled call |
| All-in cost and billing transparency | 20% | Itemised quote for all legs/components |
| Caller ID, transfer and failure recovery | 15% | Test results on target route |
| Real-time media and latency | 10% | Technical docs plus measurement |
| Privacy/security/deletion | 15% | Contract, DPA and provider evidence |
| Reliability/support/SLO | 10% | SLA, incident path and status evidence |
| Integration effort and lock-in | 5% | API/webhook docs and export options |
| Commercial flexibility | 5% | Minimums, terms and scale tiers |

A missing answer is Unknown, not a neutral score.

## G. Approval gate
Before selection, require two comparable written quotes, one successful end-to-end test on a representative route, contract and privacy/security review, realistic and stress-case contribution margin, documented fallback/disable/migration plan, and owner approval.

## H. Candidate tracking table

| Candidate | Route confirmed? | Quote received? | Test completed? | Privacy pack reviewed? | Status |
|---|---|---|---|---|---|
| Candidate A | No | No | No | No | Not contacted |
| Candidate B | No | No | No | No | Not contacted |
| Candidate C | No | No | No | No | Not contacted |
