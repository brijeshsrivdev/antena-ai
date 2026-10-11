# Current State

Snapshot: 2026-10-11. Repository: brijeshsrivdev/antena-ai. Default branch: main.

- Product implementation: not started and not authorised.
- Discovery: in progress; charter approval pending.
- Commercial brand: not selected or cleared.
- Owner's process requirement: complete research, product/marketing strategy, pricing, architecture, UX, dependency evaluation, requirements and roadmap before any coding. Owner explicitly approves implementation start.

## Known direction
- First investigate and replicate the core behaviour of a MyEqual.ai-style personal AI call assistant; later extend to domain-specific profiles.
- Android-first is the current client direction, subject to telephony and platform feasibility.
- Hospitality is the first candidate domain and should use existing Antena backend APIs, not direct database access.
- Individual users configure personal context through structured forms.
- A dedicated AI API service is expected to handle orchestration, sessions, configuration and provider abstraction.
- Legal/advocate support is a future candidate, not a first-release dependency.
- Target scale: 10,000 users; model registered, active and concurrent users separately.

## Open questions
Target segment, launch geography, core feature parity, call-routing model, provider stack, cost/minute, pricing, consent/retention, SLOs, acquisition strategy, open-source dependency choices, brand and domain availability.

## Last verified state
A documentation-only README was committed to main as an initial repository marker. The wider documentation baseline is being added. Product implementation remains unauthorised.