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