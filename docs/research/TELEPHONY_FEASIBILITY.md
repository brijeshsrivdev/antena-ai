# Telephony Feasibility — Android-First AI Call Assistant

**Status:** Preliminary desk assessment; hands-on carrier/device validation required. **Research date:** 2026-10-11. **Implementation gate:** closed.

## 1. Executive assessment

The product appears feasible only with a deliberate call-routing architecture. An ordinary Android app must not be assumed to freely capture or control cellular-call audio. Equal AI's public onboarding describes call-forwarding setup and a flow where the user declines a call so the assistant can step in. This is a useful reference, but does not prove that the same route works across every operator, SIM, device or country.

Separate these capabilities:
- Call-screening metadata: knowing a call is arriving and making allow/block decisions.
- Cellular call audio: access to live audio of a normal carrier call. Screening APIs do not by themselves provide this.
- Call forwarding: carrier/network routes a call to another endpoint where an AI voice service can answer.
- App-based VoIP: calls use an app/SIP/VoIP route, which is different from taking over arbitrary native cellular calls.
- Outgoing redirection: Android has an API for redirecting outgoing calls, not a general API for answering arbitrary incoming calls.

The first feasibility question is: which supported route delivers two-way audio to our AI service while preserving the user's existing number and a reliable fallback?

## 2. Official Android facts

### CallScreeningService

Android documents that a user-selected app implementing CallScreeningService can receive incoming/outgoing call details for screening or identification. Incoming calls require a response within five seconds. The documented call details are limited; this is not a live-audio streaming interface.

Source: https://developer.android.com/reference/android/telecom/CallScreeningService (accessed 2026-10-11).

### CallRedirectionService

Android's CallRedirectionService (API 29+) handles outgoing calls with optional redirection or cancellation. The framework expects a response within five seconds, and user selection/role is part of the flow. It is not a general incoming-call interception/audio-capture API.

Source: https://developer.android.com/reference/android/telecom/CallRedirectionService (accessed 2026-10-11).

### Google Play sensitive permissions

Google Play restricts SMS and call-log permissions. Current guidance says the app must be an eligible default Phone, SMS or Assistant handler for relevant permissions, subject to policy review and use-case restrictions. The app must clearly explain core functionality and follow disclosure/consent requirements. Do not design around broad call-log access without confirming eligibility.

Sources: https://support.google.com/googleplay/android-developer/answer/10208820 and https://developer.android.com/guide/topics/permissions/default-handlers (accessed 2026-10-11).

## 3. Candidate architectures

| Candidate | How it works | Advantages | Risks / unknowns | Initial position |
|---|---|---|---|---|
| A. Carrier forwarding to cloud voice agent | User configures conditional/unconditional forwarding; forwarded call reaches a supported voice endpoint; server runs realtime AI. | May preserve existing public number; cloud service can process audio. | Operator/SIM/region variations, forwarding charges, caller ID, busy/no-answer rules, concurrency, takeover and fallback. | Leading hypothesis to validate. |
| B. Default dialer/assistant | App assumes an Android role and uses permitted telecom APIs. | Potentially richer system integration. | Permission and Play review burden; does not automatically provide raw cellular audio. | Research alternative; don't assume it solves audio. |
| C. VoIP/SIP/app number | User/business uses a VoIP route; AI handles calls through programmable telephony. | Clear media interface and server-side control. | May require a new number or behaviour change; PSTN rates and regional restrictions. | Viable fallback or separate plan. |
| D. Hybrid forwarding + cloud AI + mobile control app | App configures profile/status; network routes calls; backend handles AI and history. | Separates UI from realtime media path. | Onboarding complexity; must prove supported route and live takeover. | Promising if A works. |

## 4. Critical questions

### Carrier and SIM
- Which Indian operators and prepaid/postpaid plans support conditional forwarding to the destination?
- What are the exact activation/deactivation codes and failure modes per operator?
- Does forwarding apply to busy, no-answer, unreachable or all calls? Are there charges or plan restrictions?
- Does caller ID survive? Can the user tell the assistant is handling the call?
- How do dual-SIM and eSIM behave? What about roaming, no coverage or powered-off devices?

### Voice session
- Can the selected provider stream two-way audio in realtime for this route and region?
- Can the assistant handle turn-taking, barge-in, silence, DTMF, noise and code-switching?
- What is end-to-end p50/p95/p99 response latency?
- Can a human take over mid-call, and what does the caller hear?
- What happens if model, STT, TTS, network or provider fails mid-call?
- Are recordings/transcripts default, optional or separately consented? Who hears any notice and when?

### Product and operations
- Can setup be verified, or must users make a test call?
- How can users disable forwarding immediately and confirm normal calling is restored?
- How does the system fail safely if backend services are down?
- How are duplicate callbacks, retries and disconnect races handled?
- What are provider limits for duration, concurrency, region, number and throughput?
- What is all-in cost per connected minute, including telephony, media, STT, model, TTS, storage, failed attempts and transfers?

## 5. Preliminary cost signal

Twilio's India pricing page currently shows example rates including US$0.0699/min for local outbound calls, US$0.0496/min for mobile calls, US$0.004/min for some browser/app or SIP/BYOC legs, and US$0.027/min for real-time transcription. These are not a complete cost estimate; product applicability, direction, number type, streaming charges, model/TTS cost, taxes and route can materially change the bill.

Source: https://www.twilio.com/en-us/voice/pricing/in (accessed 2026-10-11). Recheck current rates and applicability before modelling prices.

**Implication:** minute-based cost may dominate a low-price consumer plan. Build low/base/high all-in cost-per-connected-minute scenarios before choosing limits or advertising unlimited usage.

## 6. Proposed validation experiment (after owner approval)

1. Select 2–3 candidate Indian operators and representative prepaid/postpaid SIMs and Android versions.
2. Test forwarding on busy, no-answer and unreachable; document exact setup/removal steps.
3. Confirm destination receives calls, caller ID behaviour and audio/media integration.
4. Measure connection success, setup time, caller experience, interruption handling, takeover, disconnect and fallback.
5. Measure end-to-end latency and speech quality in English/Hindi and code-switching only where supported.
6. Test backend/provider outage, poor network, silence, noise, simultaneous calls and duplicate webhook events.
7. Record costs and carrier-specific caveats.
8. Set acceptance thresholds before testing; repeat enough to quantify reliability.

## 7. Proposed feasibility-gate criteria

Thresholds are placeholders for owner review, not commitments.
- At least one lawful and commercially viable route works end-to-end on every target carrier/SIM combination selected for launch.
- Setup, verification and deactivation are clear and recoverable in common failure cases.
- No unsupported claim of native cellular audio capture is made.
- Calls fail back safely according to the chosen route.
- Human takeover and termination behaviour are demonstrated and understood.
- p95 response latency and speech quality meet agreed thresholds.
- Cost per connected minute supports a plausible paid plan with margin buffer.
- Recording, transcription, consent, retention and deletion receive legal review for launch jurisdictions.

## 8. Risks

| Risk | Severity | Mitigation / evidence needed |
|---|---|---|
| Forwarding inconsistent or unavailable | Critical | Operator/SIM matrix, setup verification, manual fallback; avoid universal-support claims. |
| No live cellular audio through ordinary app APIs | Critical | Use a supported carrier/VoIP/media route; validate end-to-end audio early. |
| Play rejects permissions/role use | High | Minimise permissions; map each permission to official policy and approved core functionality. |
| Call missed or forwarded unexpectedly | High | Explicit opt-in, test call, clear status, quick disable and fallback. |
| High variable cost | High | Meter minutes, compare providers, set quotas and cost-aware routing. |
| Poor latency or language quality | High | End-to-end benchmarks and graceful fallback; advertise only measured languages. |
| Privacy/recording compliance gap | Critical | Data map, notice/consent, retention controls, legal review and incident plan. |
| Takeover unreliable | High | Design and test transfer/bridge before making takeover a core promise. |

## 9. Sources

- Android CallScreeningService: https://developer.android.com/reference/android/telecom/CallScreeningService
- Android CallRedirectionService: https://developer.android.com/reference/android/telecom/CallRedirectionService
- Android default-handler permissions: https://developer.android.com/guide/topics/permissions/default-handlers
- Google Play SMS/call-log policy: https://support.google.com/googleplay/android-developer/answer/10208820
- Equal AI setup: https://myequal.ai/assistant-setup/
- Equal AI account FAQ: https://myequal.ai/my-account/
- Twilio India Voice pricing: https://www.twilio.com/en-us/voice/pricing/in

## 10. Recommendation

Continue discovery with carrier-mediated forwarding to a cloud realtime voice agent as the leading hypothesis, not a committed architecture. Validate it against a VoIP/SIP alternative. Do not select providers, design around unrestricted cellular audio capture, commit to pricing, or start product coding until the owner reviews the feasibility experiment and gate criteria.

## Additional official Android audio guidance

Android's audio-input sharing documentation states that during a voice call, an ordinary app generally does not receive the call's audio; privileged pre-installed apps with CAPTURE_AUDIO_OUTPUT are a special case, and accessibility services have specific platform treatment. This reinforces that unrestricted cellular-call audio capture is not a safe design assumption. The intended media path must be validated end-to-end.

Source: https://developer.android.com/media/platform/sharing-audio-input (accessed 2026-10-11).
