# Research Register

Use primary sources where possible and record access dates. Separate official documentation, vendor claims, independent tests, reviews, estimates and inferences. Do not claim trademark clearance from exact-name searches alone.

| ID | Research question | Priority | Status | Deliverable |
|---|---|---|---|---|
| RES-001 | What is MyEqual.ai's documented feature set, platform support, routing, pricing and limitations? | P0 | IN_PROGRESS | Initial competitor profile added; hands-on verification and pricing research remain |
| RES-002 | Which direct/adjacent products cover personal AI calls, AI receptionists and voice agents? | P0 | OPEN | Competitor landscape |
| RES-003 | Which segments have frequent, painful call-handling problems? | P0 | OPEN | Segment/problem evidence |
| RES-004 | Which telephony providers support routing and real-time media in target regions? | P0 | IN_PROGRESS | Android/call-forwarding feasibility assessment added; carrier tests and provider comparison remain |
| RES-005 | Which speech/model providers meet latency, quality, language, privacy and cost goals? | P0 | OPEN | Benchmark plan |
| RES-006 | What is all-in variable cost per connected minute? | P0 | OPEN | Unit economics model |
| RES-007 | What laws/rules apply to recording, interception, transcription, consent and personal data? | P0 | OPEN | Jurisdiction matrix/legal review |
| RES-008 | What Android APIs and app-store rules constrain call routing? | P0 | OPEN | Android feasibility assessment |
| RES-009 | Which open-source voice/media/orchestration/observability dependencies are commercially suitable? | P1 | OPEN | Licence and maintenance matrix |
| RES-010 | What pricing supports gross margin and acquisition economics? | P1 | OPEN | Pricing hypotheses |
| RES-011 | What workload does 10,000 users represent under low/base/high usage? | P1 | OPEN | Capacity model |
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
