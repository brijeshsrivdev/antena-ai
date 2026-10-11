# Decision Log

| ID | Topic | Status | Position | Next action |
|---|---|---|---|---|
| DEC-001 | Documentation before implementation | APPROVED | Complete discovery and specifications before product code. | Enforce gate. |
| DEC-002 | Product direction | PROPOSED | Personal AI call assistant core first; domain extensions later. | Confirm after research. |
| DEC-003 | Initial client | PROPOSED | Android-first. | Validate telephony/platform feasibility. |
| DEC-004 | Hospitality integration | PROPOSED | Use trusted Antena APIs, not direct database access. | Audit API coverage and scopes. |
| DEC-005 | Individual context | PROPOSED | Structured user-provided context/configuration. | Define fields, consent and deletion. |
| DEC-006 | Advocate/legal profile | DEFERRED | Future candidate; not a first-release dependency. | Revisit after core validation. |
| DEC-007 | Dedicated AI API | PROPOSED | Shared orchestration/configuration/session/provider layer. | Resolve via architecture research. |
| DEC-008 | 10,000-user target | RESEARCH_REQUIRED | Model active users, minutes, peak arrivals and concurrency. | Define workload scenarios. |
| DEC-009 | Commercial brand | RESEARCH_REQUIRED | No brand approved or cleared. | Trademark, domain, app-store and competitor screening. |
| DEC-010 | Repository name | DECIDED | Repository name is antena-ai; this does not approve the commercial brand. | None. |
| DEC-011 | Domain access security | PROPOSED | Trusted server-selected connectors; scoped domain APIs only. | Ratify in security baseline. |
| DEC-012 | Product implementation | APPROVED | No coding until owner explicitly approves baseline. | Owner approval required to lift gate. |

Do not mark a decision APPROVED unless explicitly approved by the owner or directly specified by them. Link detailed architecture decisions to ADRs when created.

## Research notes added 2026-10-11 (not product decisions)

- Public Ringg pricing advertises ₹6/connected minute for a bundled voice-agent service. It is a benchmark only, not a quote for the proposed consumer routing path.
- Android call-screening/redirection APIs do not establish unrestricted cellular audio access. Carrier forwarding to a cloud voice agent remains a hypothesis to validate, not an approved architecture.
- LiveKit Agents, Pipecat and Vocode Core are candidate frameworks only. Repository-level licence files were inspected; dependency trees, model terms and exact versions remain unaudited.
- India DPDP Rules 2025 and TRAI requirements are included in issue-spotting documents; no legal conclusion is made.
