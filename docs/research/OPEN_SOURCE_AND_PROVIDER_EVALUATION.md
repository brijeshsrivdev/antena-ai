# Open-Source and Provider Evaluation Framework

**Status:** Evaluation framework; no dependency or provider selected. Date: 2026-10-11. No implementation authorised.

## 1. Goal

Choose the smallest reliable set of dependencies and providers that can deliver the validated call-assistant experience in the launch region. Do not select a stack based on popularity alone. Evaluate licence, commercial rights, maintenance, security, latency, data terms, regional support, total cost and exit cost.

## 2. Candidate layers to evaluate

| Layer | Candidate categories | Key questions |
|---|---|---|
| Telephony / routing | Carrier forwarding, programmable PSTN, SIP, hosted voice API | Does it support the actual incoming-call route, region, number type, two-way media, transfer/takeover, caller ID, concurrency and fallback? |
| Media streaming | Provider media streams, SIP media, WebSocket streaming gateway | Codec, jitter, packet loss, reconnection, backpressure, per-minute fee, data residency, security and observability. |
| Speech recognition | Managed streaming STT, self-hosted open-source STT | Supported languages/code-switching, latency, WER under noise, GPU/CPU cost, commercial licence and model weight terms. |
| Conversation model | Hosted LLM APIs, self-hosted models | Time to first token, tool-call reliability, multilingual performance, context limits, provider retention/training terms, regional processing and price. |
| Speech synthesis | Managed TTS, self-hosted TTS | Naturalness, language/voice rights, streaming latency, interruption support, cost per character/audio second, model/voice licence. |
| Realtime orchestration | Provider-specific SDKs, open-source realtime/voice frameworks, custom minimal orchestrator | Maturity, release cadence, concurrency semantics, retries, observability, dependency tree, licence and upgrade risk. |
| Storage | Managed relational database, object storage, search/index | Tenant isolation, encryption, deletion, backup lifecycle, regional placement, cost and operational burden. |
| Queue/events | Managed queue, event bus, durable workflow | Idempotency, ordering, replay, delay, cost, operations and recovery. |
| Observability | OpenTelemetry-compatible metrics/traces/logs, managed telemetry | Redaction, high-cardinality cost, retention, alerting, security and exportability. |
| Authentication | Managed identity, standards-based OIDC/OAuth, self-hosted identity | Account recovery, MFA/passkeys, mobile support, tenant boundaries, pricing and lock-in. |
| Payments | Region-appropriate subscription/payment provider | Recurring billing support, refunds, tax invoices, failed payment handling, webhook security and regional availability. |

These are categories to compare, not a stack recommendation.

## 3. Required evaluation scorecard

Score each candidate 1–5 and record evidence/confidence. Suggested weights are provisional and must be approved before final scoring.

| Criterion | Suggested weight | Required evidence |
|---|---:|---|
| Core technical fit and required media/call features | 20% | Official docs plus end-to-end test plan |
| End-to-end latency and quality | 15% | Representative benchmark, not vendor marketing alone |
| Total cost at low/base/high usage | 15% | Current pricing, usage assumptions, quote where needed |
| Commercial licence and usage rights | 10% | Exact licence text, model/voice terms, legal review if ambiguous |
| Security and privacy/data-processing terms | 10% | Privacy policy, DPA, retention and training settings |
| Regional availability and regulatory fit | 10% | Official region/number/call support and provider confirmation |
| Maintenance and security history | 5% | Release cadence, advisories, issue response and maintainer activity |
| Operational complexity and support | 5% | Runbook/incident analysis and support terms |
| Portability and exit cost | 5% | Data export, API abstraction feasibility, migration estimate |
| Ecosystem and integration maturity | 5% | Docs, examples, SDK support and community signals |

Do not let a weighted score hide a hard blocker. Licence incompatibility, unsupported call routing, inadequate privacy terms or unacceptable latency should reject a candidate regardless of score.

## 4. Licence review checklist

For every code library, server, SDK, model weights, voice, dataset and sample:
- Identify exact version and source repository/model card.
- Record licence identifier and link to the licence text.
- Check commercial use, redistribution, modification, attribution, notice, patent, copyleft/network-copyleft and source disclosure obligations.
- Review dependencies and transitive licences; maintain an SBOM.
- Check model/voice/dataset-specific terms separately from code licence.
- Check acceptable-use restrictions, output restrictions, territory and user-count limits.
- Review trademark, brand and voice likeness rights where relevant.
- Record security advisories, end-of-life status and maintainer response.
- Define upgrade policy, vulnerability SLA and replacement strategy.
- Obtain counsel review when licence terms are ambiguous or product distribution creates material obligations.

Never label a model “open source” merely because weights are downloadable. Distinguish OSI-approved open-source software, open weights, source-available models and commercial hosted APIs.

## 5. Provider due diligence

Ask providers for written confirmation of:
- inbound and forwarded call support in launch geography;
- number provisioning and caller-ID behaviour;
- real-time bidirectional media, codecs, streaming limits and transfer/takeover;
- concurrency, calls-per-second, maximum duration and rate limits;
- exact prices for call legs, media streaming, STT, TTS, model, recording, storage and failures;
- GST/tax, currency, minimum commitment and price-change terms;
- data location, subprocessors, retention, deletion, training use and breach notification;
- uptime/SLA, support response, incident communication and disaster recovery;
- contractual rights to use output and restrictions on call content/voice;
- account closure and migration/export.

## 6. Build-vs-buy rule

Buy or use managed services when they materially reduce telecom complexity, latency or operational risk and their total cost is acceptable. Consider self-hosting only after quality/latency benchmarks show the benefit outweighs GPU, scaling, patching, observability, security and on-call costs. Avoid building custom realtime infrastructure before the product's core routing path and usage pattern are proven.

## 7. Required output

Create a versioned candidate matrix with:
- candidate and exact version/plan;
- official source links and access date;
- feature fit and hard blockers;
- licence and commercial rights;
- quality/latency evidence;
- low/base/high cost model;
- data/security/regional constraints;
- maintenance and operational burden;
- score, confidence, decision status and rationale;
- migration/exit plan and next validation step.

## 8. Decision status

No library, model, voice, telephony provider, database, queue, hosting service or authentication provider is approved. Provider selection follows telephony feasibility, privacy review and cost validation.