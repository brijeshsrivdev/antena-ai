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
