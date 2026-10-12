# UX Wireflow Specification — Discovery Draft

**Status:** Textual wireflows only; no visual prototype or implementation created. Flows are hypotheses pending interviews, feasibility and owner approval.

## Proposed navigation
- **Home:** feature state, next action, usage allowance, pause/disable.
- **Calls:** outcomes, caller label, timestamp, short summary, assistant-handled indicator.
- **Call detail:** summary first, uncertainty labels, optional transcript/audio, user actions and deletion.
- **Assistant profile:** purpose, greeting/disclosure, languages, style, allowed actions, prohibited topics, escalation.
- **Call rules:** selected contacts/groups, unknown callers, exclusions, schedules and route state.
- **Usage & plan:** connected minutes, estimated spend, allowance, limits and alerts.
- **Privacy & data:** consent, retention, export/delete status, provider disclosures.
- **Settings/help:** supported device/carrier combinations, route setup, troubleshooting, provider status and account deletion.

## Flow A — Onboarding and feasibility
1. Explain capabilities and limitations in plain language.
2. Choose initial purpose/profile.
3. Check device/OS and explain the actual supported route before asking for permissions.
4. Explain each permission and request only when needed.
5. Configure forwarding/default dialer only if validated for this device/carrier.
6. Place a controlled test call with a consenting test caller.
7. Confirm outcome, caller ID, charges and disable steps.
8. Choose call categories and exclusions.
9. Review audio/transcript/summary processing, retention and providers.
10. Show **Ready**, **Limited** or **Not supported**. Permissions alone never mean Ready.

Failure branches: unsupported route → explain and allow exit; forwarding failure → preserve ordinary handling and show recovery; permission declined → keep unrelated features usable where possible; test call fails → do not activate and restore baseline.

## Flow B — Incoming call
1. Incoming call arrives through validated route.
2. Apply exclusions before AI action.
3. If excluded or route state is uncertain, fail safe and do not autonomously handle where technically possible.
4. Assistant identifies itself as an AI assistant where required by approved policy and asks caller's purpose.
5. Classify intent and extract only minimum useful facts.
6. Sensitive, urgent, uncertain or out-of-scope calls → stop autonomous action and escalate/notify.
7. Within permitted scope → respond with bounded language; never invent promises.
8. Offer takeover only where supported and report actual takeover state.
9. End call; produce concise summary with uncertainty labels.
10. Apply retention and usage ledger; surface needed user action.

## Flow C — Call list and detail
1. Separate handled, missed, failed-route and needs-attention outcomes.
2. Each row shows time, caller label/number as permitted, route status, duration and one-line summary.
3. Detail view leads with summary; transcript/audio appears only if captured and retained.
4. Mark extracted facts with uncertainty; never present inference as confirmed fact.
5. Potential actions: callback, mark important, correct summary, delete/export. Outgoing calls are a separately authorised capability, not assumed in MVP.

## Flow D — Profile setup
1. Select a backend-managed template; configure allowed fields only.
2. Configure purpose, greeting, language, response length and trusted context.
3. Choose allowed actions from a server-side capability catalogue.
4. Review prohibited actions and escalation conditions.
5. Preview synthetic scenarios.
6. Save a versioned profile and show which version applies to new calls.
7. Provide immediate pause/disable and audit profile changes.

Hospitality profile boundary: trusted Antena APIs only. It may answer approved FAQs or capture an enquiry where capability and confirmation rules permit. It must not assert availability, final price, reservation or policy unless confirmed by authoritative Antena data. No direct DB access. Legal/advocate profile is out of MVP and needs separate discovery/safeguards.

## Flow E — Usage and billing
1. Show allowance, minute counting, overage, taxes and hard-limit behavior before activation.
2. Update usage as provider data permits; label estimates.
3. Provisional warnings at 50%, 80% and 100%.
4. At limit, follow user choice: pause AI handling, stop, or continue only with explicit pay-as-you-go permission. Never silently incur uncapped charges.
5. Provide receipt and usage dispute route.

## Flow F — Privacy and deletion
1. List metadata, audio, transcript, summary, profile context, consent, billing and security logs separately.
2. State purpose, providers, retention and deletion behavior by category.
3. Offer minimum available retention; justify defaults through product necessity and legal review.
4. Show deletion state: queued, processing, completed or exceptions.
5. Explain lawful retention and backup expiry honestly.
6. Do not claim full deletion until in-scope systems/providers confirm it.

## Interaction requirements
- High contrast and explicit route state; never use color alone.
- Large touch targets and screen-reader labels.
- No autoplay audio.
- Localized UI must not imply equal model reliability in every language.
- Persistent pause/disable and normal-call recovery.
- Costs, recordings and AI disclosure cannot be hidden in dense legal text.
- Use synthetic calls in UX validation; real recordings require reviewed consent.

## Open UX questions
- Is forwarding/default-dialer setup acceptable?
- Which call categories should be excluded by default?
- Are recordings off by default, optional, or necessary?
- Does the user want transcripts or summaries only?
- What controls belong in onboarding versus advanced settings?
- Is a universal assistant more valuable than task-specific profiles?

## Validation evidence
Test with 5–8 users before visual design freeze. Observe whether users can explain routing, disable service, understand retention, identify uncertain summaries and predict usage-cap behavior. Do not build a prototype until the baseline gate is approved.

## MVP scope alignment note

This wireflow is a discovery model, not a promise that every branch ships in the MVP. Until separately approved:
- Contact/group-based call rules are optional and must not require broad contact-book access by default; the core flow needs a no-contacts fallback.
- Transcript/audio display remains disabled unless the separate feature gate for consent, legal review, retention, provider terms, cost and deletion is passed.
- Takeover is displayed only for a validated route; do not design a universal takeover promise into the base path.
- Follow-up tasks/reminders require user confirmation and must not execute external or consequential actions autonomously.

Keep the final wireflow versioned to the approved MVP and the requirement/acceptance-threshold registers.