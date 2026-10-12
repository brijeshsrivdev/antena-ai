# Voice Agent Evaluation Plan — Offline and Controlled Pilot

**Status:** Proposed evaluation protocol; no benchmark has been run. Thresholds below are candidate starting points and require owner approval before testing. This is not evidence of product quality.

## 1. Evaluation objectives

Measure the complete system, not only the language model:
- Route and call completion reliability.
- Time to first assistant speech and conversational turn latency.
- Interruption/barge-in handling and echo/overlap.
- Caller-intent capture and summary factuality.
- Language and code-switching performance.
- Escalation and refusal when requests are sensitive, uncertain or outside profile scope.
- Tool-call authorization, tenant isolation, prompt-injection resistance and action correctness.
- Cost per attempt and connected minute, including all call legs and failed calls.
- Data minimisation, retention and deletion behavior.

## 2. Test phases and dataset rules

### Phase A — Synthetic offline corpus
Build a labelled corpus with scripted, synthetic caller scenarios. Include routine enquiries, ambiguous requests, background noise, interruptions, silence, accents, code-switching, caller corrections, urgency and out-of-scope requests. Use no real call recordings by default.

Every scenario must include expected intent, key facts, allowed response, prohibited claims, escalation condition, summary ground truth and expected tool actions.

### Phase B — Consented controlled calls
Use test SIMs and consenting participants after the route has been reviewed. Record only the minimum measurements necessary. Audio capture requires a separately reviewed consent and retention plan. Never use OTP, banking, emergency, healthcare-critical or other sensitive live calls.

### Phase C — Limited pilot
Only after explicit pilot approval, route a small opt-in cohort through the proven route. Provide immediate disable/rollback, visible route status, usage caps, support contact and an incident process.

## 3. Metrics and proposed pilot gates

These are evaluation dimensions, not approved launch SLOs. `ACCEPTANCE_THRESHOLD_REGISTER.md` is the single source of truth for candidate numeric thresholds. Do not use conflicting values in this plan; any new proposed numeric threshold must be added to that register, reviewed by the owner and approved before confirmatory testing. No threshold is approved merely because it appears in an evaluation table.

| Metric | Measurement | Candidate pilot gate |
|---|---|---|
| Route completion | Calls reaching intended agent / eligible controlled attempts | Candidate: at least 95% per explicitly supported route configuration, with denominator and confidence interval reported; see AT-002. Proposed only, not owner-approved. |
| Silent call loss | Calls lost without understandable fallback | Zero observed in the test suite; any occurrence is a release blocker pending root cause |
| First response latency | Call connect to first intelligible assistant speech; p50/p95/p99 | Record baseline by route, provider, language and load. Do not set a numeric release threshold until a representative baseline exists; then propose and approve it in ACCEPTANCE_THRESHOLD_REGISTER.md before confirmatory testing (AT-003). |
| Turn latency | End of caller utterance to first intelligible response; p50/p95/p99 | Measure by provider, language, noise and load; define the release target only after the baseline and owner review. |
| Intent capture | Correct primary intent and key facts against labelled truth | Define rubric and labelled set first; report per class/language and approve a threshold in ACCEPTANCE_THRESHOLD_REGISTER.md before model comparison. No numeric accuracy claim is currently approved. |
| Summary factuality | Unsupported factual claims per summary | Track critical invented commitments separately; define the rubric and threshold before model comparison. No numeric accuracy claim is currently approved. |
| Escalation | Sensitive/out-of-scope cases correctly stopped or escalated | Zero misses in defined critical scenarios; any miss blocks pilot |
| Tool authorization | Unauthorized actions executed | Zero; any event is a security release blocker |
| Tenant isolation | Cross-tenant data/action access | Zero; any event is a security release blocker |
| Takeover | Successful takeover / eligible controlled takeover attempts | Measure only if the route supports takeover. Set a numeric gate in the threshold register before confirmatory tests; otherwise remove the takeover promise from MVP. |
| Usage accounting | Provider CDR vs platform ledger variance | Zero duplicate ledger charges for replayed/duplicate events (AT-005); all other discrepancies must be explained and the acceptable reconciliation tolerance must be approved before release. |
| Cost | All-in cost per attempt and connected minute | Must fit the approved price and stress-case margin model; threshold set after comparable written quotes. |
| Deletion | Data deletion requests completed within approved SLA | Verify deletion across all in-scope test stores and provider systems where supported; define data-class SLA before a pilot (AT-008). |

Report sample size and confidence intervals. A small sample cannot prove a universal 95% success rate. Run at least 30 repetitions per claimed carrier/forwarding configuration for exploratory evidence; more may be required for statistically defensible reliability claims.

## 4. Required scenario families

1. Routine caller asks a clear question.
2. Caller changes their mind or corrects a name/date.
3. Unclear speech, silence, background noise and interruption.
4. Hindi/English code-switching and each additional language claimed.
5. Caller requests a promise that the profile cannot make.
6. Caller asks for another person's data or attempts tenant switching.
7. Caller instructs the model to ignore its rules, reveal system prompts or call arbitrary tools.
8. Caller asks to book/cancel/change something; validate confirmation and domain authority.
9. Provider timeout, dropped media, webhook duplication and out-of-order events.
10. Call transfer/takeover fails or user disables service mid-session.
11. User reaches a spend cap or account is suspended.
12. Audio/transcript storage disabled, retention expiry, export and deletion.
13. Caller requests emergency assistance or expresses urgent risk; test only with synthetic scripts and defined safe response.
14. Profile is changed during an active call; verify version consistency and audit.

## 5. Human review and scoring

Use two independent reviewers for a representative subset of summaries and language samples. Blind reviewers to provider/model where practical. Resolve disagreements with a documented rubric. Track:
- Correct facts and omitted critical facts.
- Hallucinated details or promises.
- Caller intent and urgency classification.
- Naturalness and intelligibility.
- Appropriate disclosure and escalation.
- Whether a user could make the right follow-up decision from the summary.

Do not use a single aggregate score that hides severe failures in one language or critical scenario.

## 6. Reproducibility requirements

Every run records:
- Dataset version and scenario ID.
- App/build and backend commit.
- Profile and policy version.
- Model/provider version and settings.
- Telephony route, device/carrier where relevant.
- Region, date, network condition and call-leg metadata.
- Prompt/tool schema version.
- Raw metric, reviewer label, failure category and remediation.
- Cost components and excluded components.

Store synthetic fixtures in version control. Keep personal data and real recordings out of the repository. Any retained research data needs a named owner, purpose, access controls and expiry.

## 7. Release decision

Before a pilot, the owner approves:
- Thresholds and measurement definitions.
- Supported device/carrier/language matrix.
- Critical scenario list and zero-tolerance failures.
- Data collection/consent and retention plan.
- Cost ceiling and usage-cap behavior.
- Rollback, incident response and disable procedures.

A failed gate leads to fixing the issue, reducing the advertised scope, or stopping the route. It must not be waived silently to meet a launch date.
