# Voice Unit Economics and 10,000-User Scenario Model

**Status:** Scenario analysis only; no provider selected and no price approved. **Date:** 2026-10-11. Figures are planning assumptions unless identified as published vendor prices; they are not quotes.

## 1. Cost stack
Model each item separately: (1) telephony and all call legs, forwarding/bridge, numbers, recording, transfer, carrier fees and taxes; (2) STT, model input/output, TTS, turn detection and orchestration; (3) storage, summaries and search; (4) retries, failed calls, monitoring, support and abuse; (5) app distribution, billing, security, backups and platform overhead.

A per-minute quote excluding telephony, an extra call leg, model usage, failed attempts or taxes is not all-in.

## 2. Public price anchors (not like-for-like)

| Source | Published anchor | Caveat |
|---|---|---|
| Ringg | Advertises ₹6 per connected minute for a bundled voice-agent offer | Not a confirmed consumer SIM-forwarding quote; caller-ID preservation, takeover and exact route eligibility remain unknown. See [provider pricing evidence](../research/PROVIDER_PRICING_EVIDENCE.md) |
| Twilio India Voice | Pricing page lists US$0.0496/min for outbound mobile calls and US$0.0699/min for local calls; SDK/SIP rates differ | Route eligibility, currency conversion, taxes and call path matter |
| Exotel public business phone plans | Published package prices/credit allocations; Voice Streaming (Agent Stream) is explicitly excluded and separately priced by sales | Not an all-in consumer assistant rate. Exotel says mobile-carrier forwarding charges are separate. See [provider pricing evidence](../research/PROVIDER_PRICING_EVIDENCE.md) |
| MyOperator | ₹5,000/month Sedan and ₹15,000/month SUV, billed annually; AI plans custom | Business CPaaS, not equivalent to consumer per-user service |
| OpenAI Realtime | Published model/session rates are one component | Telephony and other model/tool usage may be additional |

Sources:
- https://www.ringg.ai/pricing
- https://www.twilio.com/en-us/voice/pricing/in
- https://exotel.com/pricing/business-phone-system/\n- https://docs.exotel.com/business-phone-system/call-forwarding-charges\n- https://support.truecaller.com/support/solutions/articles/81000412918-assistant-activation-in-india
- https://myoperator.com/pricing
- https://developers.openai.com/api/docs/pricing

## 3. Planning assumptions
Use these broad all-in connected-minute cost cases for sensitivity analysis; replace them with quotes and test measurements.

| Case | Assumed variable cost / connected minute |
|---|---:|
| Optimistic | ₹4 |
| Base planning | ₹7 |
| Stress | ₹12 |

These exclude fixed platform cost, payment fees, support labour, acquisition, GST/tax effects and app-store commissions. They are not vendor prices.

## 4. Cost per active user / month

| Connected minutes per active user | ₹4/min | ₹7/min | ₹12/min |
|---:|---:|---:|---:|
| 10 | ₹40 | ₹70 | ₹120 |
| 30 | ₹120 | ₹210 | ₹360 |
| 60 | ₹240 | ₹420 | ₹720 |
| 120 | ₹480 | ₹840 | ₹1,440 |

A ₹249/month tax-inclusive plan at 18% GST yields approximately ₹211.02 before GST, prior to payment/app-store fees. At 30 minutes/month, the base variable-cost assumption of ₹210 leaves almost no contribution. At 60 minutes, even the optimistic case costs ₹240. Unlimited plans are therefore not justified until actual usage and route costs are measured.

## 5. 10,000 registered-user scenarios

10,000 registered accounts is not 10,000 concurrent calls. MAU, call minutes and peak concurrency are separate metrics.

| Scenario | Registered | Assumed MAU | Active users | Minutes / active user | Monthly connected minutes |
|---|---:|---:|---:|---:|---:|
| Early usage | 10,000 | 10% | 1,000 | 10 | 10,000 |
| Moderate usage | 10,000 | 25% | 2,500 | 30 | 75,000 |
| Heavy usage | 10,000 | 40% | 4,000 | 60 | 240,000 |

| Scenario | At ₹4/min | At ₹7/min | At ₹12/min |
|---|---:|---:|---:|
| Early usage (10,000 min) | ₹40,000 | ₹70,000 | ₹1,20,000 |
| Moderate usage (75,000 min) | ₹3,00,000 | ₹5,25,000 | ₹9,00,000 |
| Heavy usage (240,000 min) | ₹9,60,000 | ₹16,80,000 | ₹28,80,000 |

Sensitivity model only, not a forecast.

## 6. Peak concurrency
First-order average concurrent calls = connected call minutes per hour / 60. This is not enough for capacity design. Measure 1-minute and 5-minute peaks, p95/p99 concurrency, call-duration distribution, failure rate and transfer rate before selecting infrastructure or autoscaling thresholds.

## 7. Pricing hypotheses
- Free trial with a strict connected-minute allowance and hard spend cap.
- Subscription with included minutes plus transparent overage.
- Usage-based pricing with a minimum charge and user-configured limit.
- Separate business-profile pricing where support and integrations differ.
- No “unlimited” claim until cost tails, abuse and fair-use policy are proven.

## 8. Written quote template
Ask each provider about: supported Indian operators; forwarding modes and charges; inbound/outbound rates, billing pulse, failed-call charges, transfer legs, recording, transcription, number rental, minimums, taxes and currency; real-time streaming, codecs, latency, concurrency/CPS caps, webhook security/retries, residency, subprocessors, retention, deletion, SLA and support; caller ID and takeover; permitted use for personal call screening and disclosure requirements; quote validity and cancellation terms.

**Gate:** no architecture or consumer pricing decision until at least two comparable written provider quotes and one controlled end-to-end route test exist.
