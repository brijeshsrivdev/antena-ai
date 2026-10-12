# Phase 0 Experiment Approval Checklist

**Status:** Governance template only — not an approval to run an experiment.  
**Applies to:** Customer interviews, telephony/device/carrier tests, provider outreach that shares project or business details, external user validation, and any activity that collects personal data or incurs cost.

## 1. Operating rule

No activity may be treated as approved merely because a protocol, interview script, RFP, workbook or roadmap exists. Before each distinct activity, the owner must approve a completed record below. A broad approval does not silently authorize a different participant group, call route, provider, data category, spend level or risk profile.

This checklist governs discovery experiments. It does not authorize product implementation, production traffic, a public pilot or deployment.

## 2. Approval record (complete before execution)

| Field | Required entry |
|---|---|
| Experiment ID / title | EXP-___ |
| Workstream | Customer interview / telephony / provider outreach / UX validation / other |
| Decision this experiment is intended to inform | State the exact open decision in OWNER_DECISION_PACK.md or DECISION_LOG.md |
| Hypothesis and alternatives | Include evidence that would disconfirm the preferred hypothesis |
| Scope and exclusions | Participants, devices/carriers, providers, route, geography and explicit non-goals |
| Owner / operator | Named accountable person and who performs the activity |
| Proposed dates | Start, end and review date |
| Budget ceiling | Rupee cap, including taxes, forwarding, provider minimums and contingency; ₹0 if none |
| Data to be collected | Minimum necessary fields, including whether audio, transcripts, phone numbers or identifiers are involved |
| Data location / access | Where raw notes/evidence live, who can access them and how access is revoked |
| Consent / notices | What participants are told, what they agree to, and how they can withdraw |
| Safety and reversibility | How to stop, disable, restore normal call behaviour and handle failures |
| Success / failure / ambiguity criteria | Measurable criteria agreed before execution; include a result that would stop the idea |
| Stop conditions | Concrete events requiring immediate pause and who is notified |
| Evidence artefacts | Sanitised logs, vendor emails, cost receipts or interview synthesis; no secrets or identifiable call content in this public repository |
| Review and decision owner | Who checks results and records go/no-go, pivot or more evidence needed |
| Owner decision | NOT REQUESTED / PENDING / APPROVED / REJECTED |
| Approval date and scope | Record explicit approval and any limits; do not self-mark APPROVED |

**Approval is valid only for the recorded scope and limits.** Material changes require a new approval.

## 3. Workstream-specific gates

### A. Customer interviews

Before approval:
- State the target segment and why interviewing it can resolve a named decision.
- Use the neutral interview pack; explore recent real behaviour before presenting a product pitch.
- Decide whether notes alone suffice. Do not record audio by default.
- Tell participants the purpose, voluntary nature, intended use of notes, retention approach and whether follow-up will be requested.
- Use pseudonymous participant IDs in the public workbook; keep any contact details separately in a private, access-controlled location.
- Do not collect phone numbers, call contents, contact lists, financial credentials or unrelated sensitive details.
- Define how negative and contradictory evidence will be captured and how findings will be synthesised without treating a small qualitative sample as statistically representative.

Stop if consent is unclear, the participant expects a service commitment, or unexpected sensitive information is being collected. Do not promise features, security properties or launch dates that have not been validated.

### B. Telephony, carrier or device tests

Before approval:
- Use dedicated test numbers/SIMs and consenting participants; never use emergency, OTP, bank-authentication or sensitive production calls.
- Record baseline behaviour and confirm a tested way to disable forwarding and restore ordinary incoming calls before placing the first test.
- Confirm the proposed route is allowed by relevant provider terms to the extent known; unresolved legal/contractual uncertainty must be disclosed in the approval record.
- Define a small initial test matrix, expected result, caller-ID checks, billing evidence, failure fallback and the exact expansion gate.
- Set a maximum number of attempts and maximum spend.
- Confirm how the test avoids silent call loss, unwanted forwarding and unexpected charges.
- Stop immediately on an unexpected lost call, inability to restore normal routing, unclear consent, material privacy exposure, unanticipated charges or route behaviour outside the approved scope.

A successful test proves only the tested configuration. Do not generalise across operators, devices, plans, forwarding types or regions without separate evidence.

### C. Provider outreach and quotes

Before approval:
- Select a shortlist and use the same RFP questions for each provider so responses are comparable.
- Decide what company/project information may be disclosed and use a role-based contact identity where practical.
- Do not send secrets, participant details, phone numbers, recordings or sensitive architecture details.
- Request written confirmation of exact use-case eligibility, technical limits, all billable legs/components, data terms, retention/deletion, subprocessors, contractual restrictions and quote validity.
- Set a spending cap of ₹0 unless a paid test or consultation is separately specified and approved.
- Treat marketing material and salesperson statements as vendor claims, not contractual commitments or demonstrated capability.

A provider response is not permission to test or evidence that the route works. Contract review and controlled validation remain separate gates.

### D. UX / concept validation

Before approval:
- Use clearly labelled concept flows, not a functioning service or simulated capability presented as real.
- Explain what is hypothetical and avoid collecting real call content or account credentials.
- Define which usability questions are being tested and what would materially change the design.
- Capture confusion, trust concerns, accessibility issues and negative reactions, not just preference scores.

## 4. Data handling and evidence hygiene

- Collect the minimum data needed for the named question.
- Keep names, contact details, raw recordings, transcripts, provider account credentials and unredacted bills out of this public repository.
- Use a private, access-controlled workspace for any identifiable material; assign an owner and a deletion/review date before collection.
- Do not upload confidential vendor responses or personal data into public issues, commits or pull requests.
- Sanitise screenshots and logs before attaching them to research records.
- Document retention and deletion limitations honestly; do not promise deletion from backups or providers without evidence.
- If a privacy incident or unintended disclosure occurs, stop collection, restrict access, preserve only what is necessary for incident handling and escalate to the owner.

This is an operational checklist, not legal advice. Required notices, consent, lawful basis, retention and telecom obligations must be reviewed for the actual jurisdiction and route before tests involving real communications.

## 5. Results review (complete after execution)

| Field | Required entry |
|---|---|
| Experiment ID | EXP-___ |
| Approved scope followed? | Yes / No; explain deviations |
| Actual spend | Amount, currency, invoice/receipt reference |
| Completed / stopped early | Status and reason |
| Observations | Facts only; reference sanitised evidence |
| Failures and ambiguous results | Include denominator and configuration |
| Interpretation | Hypothesis, confidence and limitations |
| Contradictory evidence | Explicitly state what weakens the hypothesis |
| Safety/privacy issues | None observed / details in private incident record |
| Decision impact | Which decision/requirement changed, if any |
| Recommendation | Go / No-go / Pivot / More evidence required |
| Follow-up | Owner and next step |
| Decision log updated? | Yes / No |
| Evidence register updated? | Yes / No |

Do not report only successful attempts. Distinguish planned, attempted, completed, failed and ambiguous cases. Keep raw observations separate from conclusions.

## 6. Minimum approval sequence

1. Draft this record and link the relevant protocol, interview pack or RFP.
2. Check participant consent, data handling, reversibility, stop conditions and spend cap.
3. Obtain explicit owner approval for this specific scope.
4. Execute only the approved activity; stop when a stop condition occurs.
5. Record results and deviations in the private evidence workspace, then publish only sanitised summaries.
6. Update the evidence workbook, research register, decision log and owner decision pack as appropriate.
7. Decide whether to stop, repeat, pivot or request approval for a new activity.

## 7. Non-approval statement

The existence of this checklist, the evidence workbook, a provider email draft, or any proposed acceptance threshold does **not** mean fieldwork is approved or has occurred. As of this document's creation, no interviews, live telephony tests, provider outreach, quotes, legal opinions, benchmarks or load tests are claimed as completed. Product implementation remains unauthorised.

## Related documents

- docs/governance/OWNER_DECISION_PACK.md
- docs/governance/DECISION_LOG.md
- docs/governance/BASELINE_CONSISTENCY_AUDIT.md
- docs/discovery/PHASE_0_EVIDENCE_WORKBOOK.md
- docs/discovery/CUSTOMER_INTERVIEW_PACK.md
- docs/research/TELEPHONY_VALIDATION_PROTOCOL.md
- docs/research/VOICE_PROVIDER_RFP.md
- docs/requirements/ACCEPTANCE_THRESHOLD_REGISTER.md
- docs/roadmap/ROADMAP.md
