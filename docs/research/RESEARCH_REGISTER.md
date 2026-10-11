# Research Register

Use primary sources where possible and record access dates. Separate official documentation, vendor claims, independent tests, reviews, estimates and inferences. Do not claim trademark clearance from exact-name searches alone.

| ID | Research question | Priority | Status | Deliverable |
|---|---|---|---|---|
| RES-001 | What is MyEqual.ai's documented feature set, platform support, routing, pricing and limitations? | P0 | IN_PROGRESS | Initial competitor profile added; hands-on verification and pricing research remain |
| RES-002 | Which direct/adjacent products cover personal AI calls, AI receptionists and voice agents? | P0 | OPEN | Competitor landscape |
| RES-003 | Which segments have frequent, painful call-handling problems? | P0 | IN_PROGRESS | Interview plan added; interviews and evidence matrix remain |
| RES-004 | Which telephony providers support routing and real-time media in target regions? | P0 | IN_PROGRESS | Android/call-forwarding feasibility assessment added; carrier tests and provider comparison remain |
| RES-005 | Which speech/model providers meet latency, quality, language, privacy and cost goals? | P0 | OPEN | Benchmark plan |
| RES-006 | What is all-in variable cost per connected minute? | P0 | IN_PROGRESS | Public provider benchmarks and scenarios added; written quotes and route-specific cost validation remain |
| RES-007 | What laws/rules apply to recording, interception, transcription, consent and personal data? | P0 | IN_PROGRESS | Preliminary India issue-spotting register and data inventory added; legal opinion and jurisdiction matrix remain |
| RES-008 | What Android APIs and app-store rules constrain call routing? | P0 | OPEN | Android feasibility assessment |
| RES-009 | Which open-source voice/media/orchestration/observability dependencies are commercially suitable? | P1 | IN_PROGRESS | Framework evaluation and repository-level licence review added; exact version pins, transitive licences and test results remain |
| RES-010 | What pricing supports gross margin and acquisition economics? | P1 | OPEN | Pricing hypotheses |
| RES-011 | What workload does 10,000 users represent under low/base/high usage? | P1 | IN_PROGRESS | Initial low/base/high model added; user evidence, provider limits and measured peaks remain |
| RES-012 | Which brands have acceptable trademark, domain, app-store and product-conflict risk? | P1 | OPEN | Brand screen |
| RES-013 | Which hospitality actions can safely be exposed through Antena APIs? | P1 | OPEN | Connector permission matrix |
| RES-014 | Which low-cost acquisition channels have evidence for this product? | P1 | OPEN | Go-to-market plan |

## Source record template
Research ID; claim/question; title and organisation; URL; access date; publication/update date; source type; finding; limitations/conflicts; confidence; affected decision/requirement; follow-up.

## Current evidence state
This is a question register, not a completed fresh market study. Mark an item complete only after sources are inspected and findings documented.

## First research increment — 2026-10-11

- RES-001: `docs/research/COMPETITIVE_ANALYSIS.md` captures Equal AI's public feature baseline, platform-information inconsistencies, differentiation hypotheses and next research tasks. This is desk research, not a full competitor landscape.
- RES-004 and RES-008: `docs/research/TELEPHONY_FEASIBILITY.md` distinguishes Android screening metadata, outgoing redirection, carrier forwarding and VoIP; it proposes validation criteria. It is not proof of carrier compatibility.
- Official sources reviewed: Android CallScreeningService and CallRedirectionService API docs; Google Play sensitive permission guidance; Equal AI official pages/store listings; Twilio India Voice pricing.
- Next: add more competitors, inspect terms/privacy in detail, define user interviews, and validate carrier/device combinations before architecture commitment.


Additional research increment (2026-10-11):
- Updated pricing and unit economics with public Ringg, Twilio, Exotel, Knowlarity and Equal AI references; ₹6/min is treated only as a public benchmark, not a confirmed cost quote.
- Added preliminary India-focused privacy/regulatory issue register referencing MeitY DPDP materials, TRAI regulations, Android API docs and Google Play policy.
- Added 10,000-registration low/base/high workload scenarios with explicit active-user and peak-factor assumptions.
- All three workstreams remain IN_PROGRESS. No provider, price, legal conclusion, concurrency target or architecture is approved.


Product definition increment (2026-10-11):
- Added proposed product scope/feature catalogue and Android-first UX screen inventory; these are hypotheses, not owner-approved requirements.
- Added preliminary positioning/go-to-market hypotheses and open-source/provider evaluation framework.
- Still needed: detailed competitor source validation, customer interviews, provider quotes, visual wireflows, numbered requirements/acceptance criteria, API contracts, security threat model, country-specific legal review and final baseline audit.


Further increment (2026-10-11):
- Added `VOICE_STACK_CANDIDATE_REVIEW.md` with initial LiveKit Agents, Pipecat, Vocode Core and managed realtime API comparison; licence conclusions are limited to repository-level licence files inspected and require version pinning/transitive audit.
- Added `CORE_REQUIREMENTS_DRAFT.md` with 15 provisional requirements and non-functional areas; unresolved thresholds are explicitly marked for later baseline review.
- Added `SYSTEM_ARCHITECTURE_OPTIONS.md` to compare managed, custom, self-hosted and VoIP-first system shapes without committing to one.


Security/privacy increment (2026-10-11):
- Added `docs/security/THREAT_MODEL.md` with initial threat scenarios, trust boundaries and controls.
- Added `docs/security/DATA_INVENTORY_AND_LIFECYCLE.md` with candidate data classes and deletion lifecycle; no retention durations are approved.
- Added `docs/research/VOICE_STACK_CANDIDATE_REVIEW.md` using official repository licence files and pricing pages; no framework/provider selected.


Architecture/verification increment (2026-10-11):
- Added initial threat model and data inventory/lifecycle, requirements traceability matrix, and verification/test strategy.
- Added product scope/feature catalogue, UX screen inventory, positioning/GTM hypotheses, architecture options and 10,000-user capacity scenarios.
- All remain discovery drafts. No user interviews, carrier tests, provider quotes, legal opinion, benchmark runs, load tests or implementation have been performed.
