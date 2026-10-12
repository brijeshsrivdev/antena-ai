# Research Register

Use primary sources where possible and record access dates. Separate official documentation, vendor claims, independent tests, reviews, estimates and inferences. Do not claim trademark clearance from exact-name searches alone.

| ID | Research question | Priority | Status | Deliverable |
|---|---|---|---|---|
| RES-001 | What is MyEqual.ai's documented feature set, platform support, routing, pricing and limitations? | P0 | IN_PROGRESS | Initial competitor profile; hands-on verification remains |
| RES-002 | Which direct/adjacent products cover personal AI calls, AI receptionists and voice agents? | P0 | IN_PROGRESS | Competitor matrix added; independent tests remain |
| RES-003 | Which segments have frequent, painful call-handling problems? | P0 | IN_PROGRESS | Market review and interview pack; interviews remain |
| RES-004 | Which telephony providers support routing and real-time media in target regions? | P0 | IN_PROGRESS | Feasibility review and test protocol; carrier tests/quotes remain |
| RES-005 | Which speech/model providers meet latency, quality, language, privacy and cost goals? | P0 | OPEN | Benchmark plan and future controlled tests |
| RES-006 | What is all-in variable cost per connected minute? | P0 | IN_PROGRESS | Cost scenarios and public anchors; written quotes remain |
| RES-007 | What laws/rules apply to recording, interception, transcription, consent and personal data? | P0 | IN_PROGRESS | Preliminary India issue-spotting; legal advice and jurisdiction matrix remain |
| RES-008 | What Android APIs and app-store rules constrain call routing? | P0 | IN_PROGRESS | Official API/policy desk review; hands-on route validation remains |
| RES-009 | Which open-source voice/media/orchestration/observability dependencies are commercially suitable? | P1 | IN_PROGRESS | Initial framework/licence review; exact versions/transitive audit remain |
| RES-010 | What pricing supports gross margin and acquisition economics? | P1 | IN_PROGRESS | Price sensitivity and cost model; customer evidence/quotes remain |
| RES-011 | What workload does 10,000 users represent under low/base/high usage? | P1 | IN_PROGRESS | Initial model; measured peaks/provider limits remain |
| RES-012 | Which brands have acceptable trademark, domain, app-store and product-conflict risk? | P1 | OPEN | Brand screen |
| RES-013 | Which hospitality actions can safely be exposed through Antena APIs? | P1 | OPEN | Connector permission matrix |
| RES-014 | Which low-cost acquisition channels have evidence for this product? | P1 | IN_PROGRESS | Positioning/GTM hypotheses; experiments remain |
| RES-015 | How do direct competitors compare on user-visible features, setup friction and price? | P0 | IN_PROGRESS | COMPETITOR_MATRIX.md; hands-on test still required |
| RES-016 | What is the plausible variable cost and contribution margin at realistic usage? | P0 | IN_PROGRESS | COST_SCENARIO_MODEL.md; exact quotes and observed usage needed |
| RES-017 | Can target carrier/device combinations support the required call route safely and reliably? | P0 | EXPERIMENT_REQUIRED | TELEPHONY_VALIDATION_PROTOCOL.md; not executed |
| RES-018 | Can target users understand onboarding, route state, privacy and usage caps? | P1 | EXPERIMENT_REQUIRED | UX_WIREFLOW_SPEC.md; user validation not conducted |

| RES-019 | Which Android APIs and Play policies actually support the proposed incoming-call experience? | P0 | IN_PROGRESS | ANDROID_CALL_ROUTE_DECISION.md; device/provider test remains |
| RES-020 | Which voice provider supports the exact India route with transparent all-in costs and acceptable data terms? | P0 | EXPERIMENT_REQUIRED | VOICE_PROVIDER_RFP.md; no providers contacted or quotes received |
| RES-021 | How should profile capabilities, tenant access, confirmation and audit be governed? | P0 | IN_PROGRESS | CAPABILITY_GOVERNANCE.md; owner review and tests remain |
| RES-022 | Which low-cost GTM experiment identifies a segment with pain, setup willingness and plausible economics? | P1 | IN_PROGRESS | GTM_EXPERIMENT_PLAN.md; no experiments run |

## Source record template
Research ID; claim/question; title and organisation; URL; access date; publication/update date; source type; finding; limitations/conflicts; confidence; affected decision/requirement; follow-up.

## Current evidence state
This is a question register, not a completed fresh market study. Mark an item complete only after sources are inspected and findings documented. Desk research is not equivalent to independent product testing, legal advice, customer validation, or controlled performance measurements.

## Research updates — 2026-10-11
- Equal AI remains the closest direct benchmark in this review; hiRobin presents a task-completion proposition; Truecaller Assistant and native screening are adjacent substitutes.
- Publicly visible feature lists, app-store metadata and vendor price pages were used as starting points. They do not establish actual call success, language quality, latency, user willingness to pay or unit economics.
- Added a competitor matrix, voice cost sensitivity model, customer interview pack, carrier/device validation protocol and textual UX wireflow spec.
- Cost cases of ₹4/₹7/₹12 per connected minute are assumptions only. Twilio, Exotel, Ringg and MyOperator figures have different scopes and must not be compared as equivalent all-in quotes.
- No interviews, live route tests, provider quotes, legal opinions, benchmarks, load tests or implementation have been performed.
- Next: obtain customer evidence, run consented owner-supervised route tests, obtain comparable written quotes, and then reconcile measurable requirements and architecture.


## Research updates — additional desk review, 2026-10-11
- Android official docs describe CallScreeningService as a bounded call-screening/identification API that must respond within five seconds; they do not document a general cellular-audio relay to a cloud AI agent. Source: https://developer.android.com/reference/android/telecom/CallScreeningService
- CallRedirectionService is for redirecting/cancelling outgoing calls and is not an incoming audio-bridge solution by itself. Source: https://developer.android.com/reference/android/telecom/CallRedirectionService
- Google Play's call/SMS permission policy restricts sensitive permissions and ties them to eligible core functionality/default-handler requirements. Source: https://support.google.com/googleplay/android-developer/answer/10208820
- TRAI lists the TCCCPR Third Amendment, 2026, released 18 September 2026. Exact applicability to this product needs specialist review: https://www.trai.gov.in/release-publication/regulations/amendments-page/7617
- Added a route decision document, provider RFP, capability governance and GTM experiment plan. No provider requests, interviews, campaigns, device tests or implementation have occurred.

| RES-023 | Which Indian voice-provider public prices apply to the exact consumer forwarding + real-time AI route? | P0 | IN_PROGRESS | PROVIDER_PRICING_EVIDENCE.md; public pricing remains non-comparable and written quotes are outstanding |
| RES-024 | Which consequential external claims are supported by official docs, vendor assertions, store listings or internal assumptions? | P0 | IN_PROGRESS | EXTERNAL_CLAIM_LEDGER.md; desk claims are classified, but freshness, legal applicability and route-specific confirmation remain open |

## Provider pricing evidence update — 2026-10-11
- Added `docs/research/PROVIDER_PRICING_EVIDENCE.md` to distinguish public price anchors from route-specific all-in costs.
- Ringg advertises ₹6 per connected minute for a bundled voice-agent offer; this is not evidence that existing-number consumer forwarding, original caller ID, and takeover are supported.
- Exotel's public business phone packages exclude Voice Streaming (Agent Stream), which is priced separately by contacting sales. Exotel documentation also states that carrier forwarding charges are separate from the Exotel bill.
- Truecaller's India activation instructions show a forwarding-based assistant pattern and carrier-specific setup, but do not establish our product's route eligibility or provider terms.
- No provider was contacted, no quote received and no route tested. Public prices must not be presented as comparable all-in offers.

## Competitor evidence update — 2026-10-11
- Added Sharyx AI Call Assistant as an adjacent Android-listed product; its listing describes forwarding calls to a dedicated AI number. The listing showed 500+ downloads and an initial release date in July 2026 at review time. These are store-reported signals, not active-user or quality measurements. Source: https://play.google.com/store/apps/details?id=com.sharyx.call_assistant
- Clarified Equal AI price interpretation: official terms state paid Android features may be offered as one-time unlocks or subscriptions and displayed prices may vary by offer and purchase point. App Store ₹149/₹249 entries are not a universal subscription quote. Sources: https://myequal.ai/terms-and-conditions/ and https://apps.apple.com/in/app/equal-ai-call-assistant/id6757906431
- The competitive picture supports testing both the exact call route and differentiated user value; it does not establish willingness to pay or a defensible moat.


## Official-source freshness check — 2026-10-12

- **Android CallScreeningService:** The current official API reference describes a call-screening/identification service receiving call details and requiring a response within five seconds. It does not document a general cellular-audio streaming API for a cloud conversational agent. Source: https://developer.android.com/reference/android/telecom/CallScreeningService . This supports the existing feasibility caveat, not a conclusion about every possible carrier/VoIP route.
- **Android CallRedirectionService:** The official reference describes optional redirection/cancellation of outgoing calls. It is not evidence of unrestricted incoming cellular audio capture. Source: https://developer.android.com/reference/android/telecom/CallRedirectionService .
- **Google Play permissions:** The current policy continues to restrict call-log/SMS permissions to eligible default Phone/SMS/Assistant-handler functionality, subject to policy review. The policy page also announces a change effective 27 January 2027 concerning phone-call account verification and READ_CALL_LOG; this is a future policy date and must be rechecked before release. Sources: https://support.google.com/googleplay/android-developer/answer/10208820 and https://support.google.com/googleplay/android-developer/answer/16558241 .
- **India DPDP Rules:** MeitY's current official index lists the Digital Personal Data Protection Rules, 2025 with a publication date of 14 November 2025 and also lists related implementation documents. A PIB page uses 13 November in its description; use the Gazette/MeitY instrument and its commencement provisions for legal analysis rather than relying on a press summary. Sources: https://www.meity.gov.in/documents/act-and-policies and https://www.meity.gov.in/documents/act-and-policies/digital-personal-data-protection-rules-2025-gDOxUjMtQWa?pageTitle=Digital-Personal-Data-Protection-Rules-2025 . The rules include phased commencement; this desk check does not determine which provisions apply to a future launch date.
- **TRAI TCCCPR:** TRAI's amendments page lists the TCCCPR Third Amendment Regulations, 2026 with release date 18 September 2026. A separate TRAI consultation page records the earlier draft consultation. The final instrument must be read and counsel must assess applicability; the title/date alone does not establish a restriction on this product. Sources: https://www.trai.gov.in/release-publication/regulations/amendments-page/7617 and https://trai.gov.in/release-publication/consultation .

**Classification:** Official-source desk verification only. No legal opinion, provider confirmation, Play review, device/carrier test or product permission is established. Recheck source versions and commencement dates immediately before any real-call test, implementation or distribution.


## External claim ledger update — 2026-10-12
- Added `docs/research/EXTERNAL_CLAIM_LEDGER.md` to separate what official platform/regulator pages, vendor claims, app-store listings and internal models actually support from what they do not establish.
- The ledger records 17 claims, source classes, limitations, status and decision impact, including Android route constraints, Play policy, DPDP/TRAI source limits, vendor pricing scope and workload/cost assumptions.
- This is a traceability aid, not proof that every source was reopened in this pass or independently tested. Product-specific route support, provider quotes, customer demand and legal applicability remain unverified.
- No interviews, provider outreach, live calls, legal opinions, benchmarks, load tests or implementation have occurred. No new activity is authorised.

## Targeted official-source recheck — 2026-10-12

- Reopened Google Play's current SMS/Call Log policy. It explicitly lists call recording among invalid uses of sensitive permissions and restricts speech-to-text/text-to-voice when the app is not the default handler or eligible for an exception; it also notes a 27 January 2027 change for READ_CALL_LOG account verification. Product-specific permission mapping and Play eligibility remain unverified.
- Reopened the DPDP Act commencement notification in the Gazette. Its masthead is dated 13 November 2025 and the notification groups provisions into commencement on publication, one year later and eighteen months later. MeitY's index separately lists the DPDP Rules as published 14 November 2025. Counsel must map the Act and Rules separately to a proposed launch date.
- Reopened Exotel's official business-phone pricing page. Listed packages exclude Voice Streaming/Agent Stream, which is separately priced. This reinforces that the public package figures are not an all-in route quote.
- Updated ANDROID_CALL_ROUTE_DECISION.md, PRIVACY_AND_REGULATORY_RISK_REGISTER.md and EXTERNAL_CLAIM_LEDGER.md. Sources: https://support.google.com/googleplay/android-developer/answer/10208820 ; https://www.meity.gov.in/static/uploads/2025/11/c56ceae6c383460ca69577428d36828b.pdf ; https://next.exotel.com/pricing/business-phone-system/ .
- No legal opinion, provider outreach, Play review, interview, live call, benchmark, load test or implementation occurred. These are source checks only.