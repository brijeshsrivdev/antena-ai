# Pricing and Unit Economics — Research Framework

**Status:** Research in progress; no plan or price is approved. Research date: 2026-10-11. India/INR is a candidate launch scenario, not a confirmed exclusive market.

## 1. Core pricing question

Can a consumer subscription cover a variable voice cost that may scale with every connected minute, while leaving enough gross margin for support, infrastructure, payment fees, acquisition, taxes, refunds, and failed calls?

Do not price from competitor sticker prices alone. Validate willingness to pay and distinguish a provider's bundled price from a self-managed stack.

## 2. Public price benchmarks reviewed

| Provider / plan | Publicly advertised price | What it appears to include | Limitations / interpretation |
|---|---:|---|---|
| Ringg AI Voice Agents | ₹6 per connected minute | Provider page says proprietary STT, natural TTS, a fine-tuned LLM, telephony and basic analytics are bundled. Number add-on listed at ₹499/month. | Business voice-agent platform, not proof of an equivalent consumer-call-routing offer. Confirm taxes, call direction, country/number constraints, retention, concurrency and overage terms with provider. |
| Twilio India Voice | Example outbound local US$0.0699/min; outbound mobile US$0.0496/min; media streams US$0.0044/min; Conversation Relay US$0.07/min; real-time transcription US$0.027/min. | Different billable product components. | Do not add these blindly: product choices can overlap. Inbound rates and the exact call path need separate confirmation. International USD pricing and product/region restrictions apply. |
| Exotel business phone system | Published packages include ₹9,999, ₹19,999 and ₹49,499 packages with varying validity, rental, credits and features; page says voice streaming is separate. | Business telephony bundle and credits. | Not directly comparable to per-connected-minute consumer AI. Confirm AgentStream/streaming cost and applicable terms. |
| Knowlarity | Public plans include per-agent subscriptions and separate call charges depending on product. | Business phone/contact-centre services. | Not an apples-to-apples consumer AI plan; confirm all telephony and AI components. |
| Equal AI | Terms say some history, live transcript and audio features are paid, with price shown in app and potentially varying by offer. | Consumer call-assistant product. | No single stable price can be inferred from terms. Capture in-app offers only through legitimate hands-on review. |

### Sources (accessed 2026-10-11)
- Ringg AI voice-agent pricing: https://www.ringg.ai/pricing
- Twilio India Voice pricing: https://www.twilio.com/en-us/voice/pricing/in
- Exotel business phone pricing: https://exotel.com/pricing/business-phone-system/
- Knowlarity voice pricing: https://www.knowlarity.com/pricing/voice
- Equal AI terms: https://myequal.ai/terms-and-conditions/

Vendor-published rates are snapshots, not binding quotes. Confirm price basis, GST/tax, currency, call direction, number rental, audio streaming, model usage, retention, concurrency, minimum commitments and failure billing before a commercial decision.

## 3. Illustrative usage scenarios at a ₹6/min bundled benchmark

These are arithmetic scenarios, not a forecast and not our own cost estimate. Assumes the entire listed minute volume is billable connected time and ₹6/min is applicable without extra usage charges.

| Scenario | Monthly active users | Calls / active user / month | Avg connected minutes / call | Connected minutes / month | Benchmark provider spend / month |
|---|---:|---:|---:|---:|---:|
| Low | 1,000 | 10 | 2 | 20,000 | ₹1,20,000 |
| Base | 2,500 | 20 | 3 | 150,000 | ₹9,00,000 |
| High | 5,000 | 30 | 4 | 600,000 | ₹36,00,000 |

At a 10,000 registered-user target, active users and call intensity matter far more than registrations alone. Even the low scenario is ₹1.2 lakh/month at the public benchmark. That makes unlimited usage risky without measured demand and a defensible cost structure.

## 4. Unit-cost formula

- connected_minutes = active_users × calls_per_user_per_month × average_connected_minutes_per_call
- provider_variable_cost = connected_minutes × verified_all_in_cost_per_connected_minute
- gross_profit_before_overhead = net_revenue − provider_variable_cost − other_variable_costs
- gross_margin_before_overhead = gross_profit_before_overhead ÷ net_revenue

The final model must include number rental, media streaming, STT/TTS/model, transfer legs, recording/storage, retries/failures, payment fees, taxes, refunds, support, acquisition, fixed infrastructure and provider minimums. Distinguish connected minutes from AI-active minutes only if provider billing supports that distinction.

## 5. Price sensitivity illustration

At ₹6 per minute, voice cost alone is:
- 20 minutes/user/month = ₹120
- 40 minutes/user/month = ₹240
- 60 minutes/user/month = ₹360
- 100 minutes/user/month = ₹600

This excludes all other costs. A ₹299 plan including 40 minutes would not work at this benchmark because voice cost alone would be ₹240, leaving ₹59 before payment fees, taxes, support and acquisition. A plan with included minutes must be costed at the upper end of expected use, not just average use.

## 6. Pricing hypotheses to test, not offers to publish

- Metered starter plan with a small included minute allowance and transparent top-up/overage.
- Subscription tiers with capped included minutes, clear maximum call duration and alerts near the limit.
- Premium tier only if additional value is clear (e.g. longer history, advanced actions, more profiles), not merely a large unbounded voice allowance.
- Separate business/voice-agent pricing only if the product scope and call-routing economics genuinely differ.

Do not publish these as plans until user research and a verified provider quote exist. Never advertise “unlimited” without a measured abuse model and worst-case margin analysis.

## 7. Required next evidence

1. Obtain current written quotes/price sheets for two or more viable India-capable telephony/voice paths.
2. Confirm exact inbound, forwarding, media stream, recording, STT, TTS, model and transfer charges.
3. Determine whether provider pricing includes taxes, number rental, retries, failed calls, minimum duration rounding and storage.
4. Measure real average and p95 call duration and user call volume through discovery interviews or consented pilot research.
5. Test whether users value live takeover, transcripts, summaries and follow-up enough to pay.
6. Model 10%, 25% and 50% active users among 10,000 registrations, with low/base/high usage and margin sensitivity.
7. Compare build-vs-buy including engineering/operations cost and provider lock-in.
8. Have the owner approve the pricing hypothesis before implementation.

## 8. Decision status

No price, usage allowance, provider or gross-margin target is approved. This document is a starting economic model that must be updated with verified quotes, customer evidence and explicit assumptions.
