# Android Call Route Constraints and Decision Gates

**Status:** Official-document desk review; no device test performed. Reviewed 2026-10-11. This is technical product research, not a guarantee of Play approval or legal advice.

## Executive finding

The public Android APIs reviewed do not provide a general third-party service that can answer an ordinary carrier call, access its two-way cellular audio stream, and relay it to a cloud AI agent. Android provides call-screening and call-redirection roles for bounded functions. These are not equivalent to unrestricted call answering or audio capture.

The product promise must follow a route proven on actual devices, carriers and provider contracts.

## Relevant official APIs and limits

### CallScreeningService
Official reference: https://developer.android.com/reference/android/telecom/CallScreeningService

- A user-selected screening service can allow, silence or block eligible incoming calls before they ring and can provide caller identification.
- It must respond within five seconds.
- The API supplies limited call details, not a general cellular audio stream.
- The screening flow applies to eligible telephone calls; contact visibility and restricted/unknown presentation have documented limitations.
- **Product implication:** useful for screening/caller-ID experiments, but insufficient by itself to implement a remote conversational AI that speaks to the caller.

### CallRedirectionService
Official reference: https://developer.android.com/reference/android/telecom/CallRedirectionService

- Primarily concerns redirecting or cancelling outgoing calls.
- It must respond within five seconds; timeout can cause the call to be cancelled.
- It does not itself establish a general incoming-call answer/bridge or audio-capture capability.
- **Product implication:** potentially relevant to outgoing-call workflows, not a solution to incoming cellular assistant audio.

### Google Play call/SMS permissions
Official policy: https://support.google.com/googleplay/android-developer/answer/10208820

- Call-log and SMS permissions are restricted to eligible core use cases and default-handler/exception conditions.
- Default-handler status and a policy declaration may be required; losing the role requires stopping access.
- **Product implication:** do not make call-log access a hidden prerequisite. Design permission minimisation and Play policy review into the route decision.

## Route options and trade-offs

| Route | What it may enable | Main risk | Current status |
|---|---|---|---|
| Carrier conditional forwarding to a hosted AI number | A forwarded call can reach a provider-controlled number if carrier and provider support it | Per-carrier setup, forwarding charges, caller-ID changes, takeover complexity, provider eligibility and local rules | Highest-priority hypothesis to test; not validated |
| Default dialer / screening role only | Call screening, limited metadata, caller ID and handling permitted by APIs | Does not itself grant remote two-way cellular audio; role-change friction | Useful supporting feature, not sufficient for full AI conversation |
| VoIP-first app | App-controlled media and AI interaction within the app's calling experience | New calling workflow, reachability and emergency-call considerations | Fallback hypothesis; different product promise |
| Business/hosted number | Controlled routing for a business or public-facing number | Number migration, forwarding and caller-ID constraints | Potential distinct B2B product |
| Carrier/OEM/telephony partnership | Potentially more integrated route if contract supports it | Long sales cycle, commercial minimums and dependency | Not assumed available |

## Decision sequence

1. Specify one exact user-visible promise, such as “when you forward eligible calls to this assistant, it answers and sends you a summary.” Do not promise universal interception.
2. Pick two test devices and two target carrier/plan combinations with owner consent.
3. Obtain written provider confirmation that the exact Indian route and consumer use are supported.
4. Run the validation protocol in TELEPHONY_VALIDATION_PROTOCOL.md, including caller ID, call legs, cost, takeover and failure recovery.
5. Confirm the intended app-store role and permission model against current policy before implementation.
6. Decide whether setup friction is acceptable in customer interviews.
7. Choose a route only if technical reliability, lawful use, unit economics and user acceptance all pass.

## Evidence sources
- Android CallScreeningService: https://developer.android.com/reference/android/telecom/CallScreeningService
- Android CallRedirectionService: https://developer.android.com/reference/android/telecom/CallRedirectionService
- Google Play SMS/call-log permission policy: https://support.google.com/googleplay/android-developer/answer/10208820
- Google Play permissions for default handlers: https://developer.android.com/guide/topics/permissions/default-handlers
- TRAI TCCCPR Third Amendment, published 18 September 2026: https://www.trai.gov.in/release-publication/regulations/amendments-page/7617
- India DPDP Rules 2025 announcement: https://www.pib.gov.in/PressReleasePage.aspx?PRID=2190014&lang=2&reg=3

TRAI's recent amendment is a reason to obtain current specialist advice on the exact telephony and commercial-communications model; its existence alone does not establish that this product is permitted or prohibited.

## No-go conditions
- Required call audio route cannot be demonstrated on target devices/carriers.
- Provider will not confirm the proposed use and route in writing.
- Caller ID, takeover or fallback behavior is unsafe or too confusing.
- Required Play permissions or distribution model cannot be justified.
- Actual cost exceeds validated willingness to pay without a credible change in scope or economics.


## Official-source freshness note — 2026-10-12

The official Android API pages were rechecked for this discovery pass. CallScreeningService remains documented as screening/identification with a five-second response requirement; CallRedirectionService is documented for optional outgoing-call redirection/cancellation. Neither reference establishes unrestricted incoming cellular-audio access for a cloud AI assistant. Sources: https://developer.android.com/reference/android/telecom/CallScreeningService and https://developer.android.com/reference/android/telecom/CallRedirectionService .

Google Play's current SMS/call-log policy continues to restrict sensitive permissions to eligible default-handler functionality and subject to review. The policy page notes a change effective 27 January 2027; check the then-current policy before implementation/distribution: https://support.google.com/googleplay/android-developer/answer/10208820 .

TRAI's amendments index lists the TCCCPR Third Amendment Regulations, 2026 dated 18 September 2026. Its application to this proposed call-routing model is not inferred here and needs qualified review: https://www.trai.gov.in/release-publication/regulations/amendments-page/7617 . This source check is not legal advice and does not replace route/provider tests.

## Google Play policy detail recheck — 2026-10-12

The current policy page contains more specific constraints than a generic statement that call-log/SMS access is restricted:
- It says apps must use sensitive Call Log/SMS permissions only for permitted uses and critical core functionality, with default-handler registration and policy review where applicable.
- It lists call recording among invalid use cases for these sensitive permissions.
- It lists text-to-voice and speech/voice-to-text among invalid uses when the app is not the default handler or an eligible exception.
- It states that phone-call account verification will no longer be an eligible READ_CALL_LOG use case from 27 January 2027.

These restrictions are relevant to permission design and distribution but do not prove that every conditional-forwarding design needs those permissions. Before choosing an architecture, map each proposed feature to its exact permissions, default role, policy category and store declaration. Do not assume the product will qualify for a role or exception.

Source checked: https://support.google.com/googleplay/android-developer/answer/10208820 . No Play Console review, permission declaration or route test has been completed.