# Provider Pricing Evidence — India Voice Routes

**Evidence snapshot:** 2026-10-11  
**Status:** Public desk research only. No provider contacted, no written quote received, no route tested.  
**Decision affected:** provider shortlist, architecture, pricing, gross-margin gate.

## Executive conclusion

Public price pages do **not** establish an affordable, supported all-in cost for a consumer AI call assistant that receives a call forwarded from a user's existing mobile number, streams audio to an AI agent, and supports caller-ID preservation and takeover.

The strongest practical conclusion is not that any provider is selected. It is that price comparisons must be route-specific and must include all call legs, voice streaming, model/speech components, forwarding charges, number rental, taxes, and failed-call billing.

## Evidence table

| Provider/source | Publicly stated evidence | What it may help with | What it does not prove |
|---|---|---|---|
| Ringg India voice-agent pricing | Advertises ₹6 per connected minute for a voice-agent bundle including proprietary STT, TTS, fine-tuned LLM, telephony and basic analytics; phone number listed as ₹499/month. Source: https://www.ringg.ai/pricing | A useful published bundled voice-agent price anchor and a candidate for a written quote | Eligibility for consumer personal-call screening, compatibility with conditional forwarding from target SIMs, original caller-ID preservation, takeover, exact exclusions, negotiated terms, or a production SLA for this use case |
| Exotel Business Phone System pricing | Public packages include ₹9,999, ₹19,999 and ₹49,499 options with different validity, rental and credit allocations. Source: https://exotel.com/pricing/business-phone-system/ | Business telephony/number and call-flow exploration | A directly comparable per-connected-minute consumer AI price. Exotel explicitly says Voice Streaming (Agent Stream) is excluded from the listed plans and priced separately by contacting sales |
| Exotel call-forwarding guidance | Exotel says forwarding is performed by the customer's service provider and is paid separately, not included in the Exotel bill. Sources: https://docs.exotel.com/business-phone-system/call-forwarding-charges and https://support.exotel.com/support/solutions/articles/3000019643-who-do-i-pay-call-forwarding-charges-for-my-customer-facing-number-to-my-service-provider-or-exotel | Identifies a potentially separate cost and dependency for calls forwarded from an existing customer-facing number | The amount charged by each user's mobile operator, whether the exact route is available on target SIMs, or the total cost of a complete AI session |
| Truecaller Assistant India activation | Official help documents describe activation using call forwarding and list Airtel, Jio, Vodafone Idea and BSNL, with carrier-specific instructions. Sources: https://support.truecaller.com/support/solutions/articles/81000412918-assistant-activation-in-india and https://support.truecaller.com/support/solutions/articles/81000419841-assistant-activation | Evidence that a forwarding-based assistant model exists in the Indian market and that carrier-specific setup matters | Any third-party provider's commercial/technical permission to offer the same route, our route's reliability, or transferable commercial terms |
| RinggVoice public pricing | A separately branded public page lists USD subscription tiers and included minutes for inbound/outbound call-team use. Source: https://ringgvoice.com/pricing | A secondary voice-agent pricing reference for business workflows | A comparable Indian rupee price or consumer SIM-forwarding offer; do not conflate this page with Ringg's India ₹6/min pricing without written clarification |
| Twilio India voice pricing | Public route-specific prices vary by call type and destination. Source: https://www.twilio.com/en-us/voice/pricing/in | A price component to investigate if route and account eligibility are confirmed | An all-in price including forwarding, media streaming, model/speech, local regulatory constraints and all call legs |

## Interpretation and confidence

- **High confidence:** The public sources describe different commercial products and billing units; headline numbers are not directly comparable.
- **High confidence:** Exotel's public business phone package page says Voice Streaming is excluded and requires separate pricing; its forwarding documentation says the carrier forwarding charge is separate.
- **Medium confidence:** Ringg's ₹6/connected-minute figure is a useful comparison anchor for a bundled voice agent, subject to the provider's exact billing definition and terms.
- **Low confidence / unknown:** Whether any provider will contractually support the exact personal-call-assistant route, original caller ID, immediate takeover, consumer scale, and acceptable privacy terms.

## Required next step

Send the same request in `VOICE_PROVIDER_RFP.md` to at least two candidates. Require written answers for these three separate routes:

1. **Existing-number conditional forwarding:** busy/no-answer/unreachable, with caller ID, setup/disable instructions, and mobile operator charges stated.
2. **Hosted-number/VoIP route:** inbound call, live media streaming, transfer/takeover and fallback behaviour.
3. **Alternative if route 1 is unsupported:** provider-recommended lawful and contractually supported design, with the user-visible trade-offs.

For each route, use the shared canonical workload scenarios in `../architecture/WORKLOAD_SCENARIO_BASELINE.md` as the default quote comparison: 20,000 / 150,000 / 600,000 connected minutes per month. If useful, request the alternate 10,000 / 75,000 / 240,000-minute sensitivity set in `../business/COST_SCENARIO_MODEL.md` separately and label it as a different scenario set. Request a sample invoice that itemises every call leg and AI component. Ask the provider to state unsupported capabilities explicitly rather than marking them "custom".

## Decision rule

Do not select a provider or publish an included-minutes plan from these public pages alone. Require two comparable written quotes, successful owner-supervised route tests, contract/privacy review, and a margin model that includes GST, payment/app-store fees, support, retries, and fixed platform costs.