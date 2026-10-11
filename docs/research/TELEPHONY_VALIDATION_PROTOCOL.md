# Telephony Validation Protocol — Owner-Run Experiments

**Status:** Planned, not executed. No carrier, SIM, device, or end-to-end routing test has been performed for this project. Android APIs and marketing pages do not substitute for end-to-end evidence.

## Purpose
Establish whether the personal cellular-call experience is reliable and commercially supportable on target Indian devices and carriers before architecture selection.

## Safety boundaries
- Use only test SIMs and consenting participants; never route unsuspecting third-party calls into AI.
- Do not record or retain audio unless all required parties are appropriately informed and the process is reviewed for applicable law/provider terms.
- Never test with bank, OTP, emergency, healthcare-critical or other sensitive calls.
- Preserve a way to disable forwarding and restore baseline configuration immediately.
- No production numbers, live customer traffic, broad distribution or deployment during discovery.

## Test matrix

| Case | Procedure | Evidence to capture |
|---|---|---|
| Baseline incoming | Call test SIM with forwarding disabled | Normal ring, answer, caller ID and missed-call behavior |
| No-answer forwarding | Configure carrier-supported no-answer forwarding to controlled destination | Routing, timeout, caller ID, charges |
| Busy forwarding | Call while line is busy | Whether forwarding triggers consistently |
| Unconditional forwarding | Enable then disable forwarding | Routing and reversible rollback |
| Caller ID | Call from second consented test number | Original, forwarded or masked ID across route |
| Takeover | Use supported mechanism to join/take over | Time, audio quality, failure modes |
| Failure/fallback | Make controlled destination unavailable | Clear fallback, notification, no silent disconnect |
| Voicemail conflict | Repeat with carrier voicemail settings where permitted | Which service captures the call first |
| DTMF / IVR | Use test IVR with non-sensitive options | Navigation reliability if in scope |
| Language/code-switching | Fixed script in English, Hindi and one mixed-language case | Transcript, intent and response correctness |
| Network change | Change connectivity if route depends on app data | Recovery and visible state |
| Disable / recovery | Turn feature off and restore normal handling | No residual routing; confirmation |

Record device model, OS/build, carrier, plan type if relevant, SIM slot, network state, forwarding mode, destination provider, test language and timestamp. Avoid putting real numbers, recordings or credentials in the repository.

## Measurements
- Setup time and manual steps.
- Route success per condition; failed and ambiguous cases.
- Call connect, first assistant speech, notification and takeover latency.
- Caller ID and call-leg count.
- Cost per attempt and connected minute; billing pulse/rounding.
- Audio quality, drops, repeated prompts and incorrect summaries.
- Urgent/non-urgent classification and fallback behavior.
- Ability to disable quickly and verify normal handling.

Report raw counts; do not claim statistical reliability from a handful of calls.

## Proposed go/no-go gates
Approve thresholds before running tests. Provisional pilot gates:
- At least 95% of controlled calls follow intended route in each supported condition, with at least 30 repetitions per claimed carrier/forwarding configuration before generalising.
- Caller ID behavior is understood and documented.
- Takeover and fallback have explicit user-visible outcomes; no silent call loss in tested cases.
- Provider confirms route and intended use in writing, including compliance and billing.
- Reversible disable is demonstrated.
- Unit economics fit candidate pricing under realistic usage and stress case.

A result for one device/carrier cannot be generalised to all Android phones or Indian operators.

## Evidence form
Test ID | Date | Device/OS | Carrier/plan | Forwarding mode | Provider | Expected | Actual | Caller ID | Latency | Duration | Cost | Takeover | Fallback | Consent status | Evidence link | Notes

## Alternative route if cellular forwarding fails
Compare VoIP-first calling (different promise/adoption friction), business-number/hosted-number routing for a distinct business product, device-level screening without claiming full cellular audio access, or a partner-led route. No alternative is automatically selected; the product promise must match validated capability.
