# Privacy and Regulatory Risk Register — AI Call Assistant

**Status:** Preliminary issue-spotting, not legal advice or a compliance opinion. Research date: 2026-10-11. Launch jurisdiction and exact call-routing model remain undecided.

## 1. Why this is release-critical

The product may process the user's identity and contacts, caller phone numbers, live speech, transcripts, summaries, inferred intent, follow-up tasks and potentially sensitive information spoken by third parties. Callers may not be the account holder and may not have interacted with the app. The design must account for both user expectations and third-party rights.

Do not treat “the user enabled call forwarding” as sufficient consent for every recording, transcription, model-processing, retention or disclosure purpose.

## 2. India-focused issues to investigate

### Digital personal data
India's Digital Personal Data Protection Act, 2023 and Digital Personal Data Protection Rules, 2025 are key primary sources. MeitY announced the Rules on 14 November 2025 and described an 18-month phased timeline; applicability and commencement must be mapped provision-by-provision against the intended launch date rather than assuming every obligation commenced at once.

Sources:
- MeitY Act and Policies: https://www.meity.gov.in/documents/act-and-policies
- Notified DPDP Rules 2025: https://www.meity.gov.in/documents/act-and-policies/digital-personal-data-protection-rules-2025-gDOxUjMtQWa?pageTitle=Digital-Personal-Data-Protection-Rules-2025
- PIB notification summary: https://www.pib.gov.in/PressReleasePage.aspx?PRID=2190014&lang=2&reg=3

Design implications to review with Indian counsel:
- Identify purposes and lawful basis/consent requirements for each data category and each participant.
- Provide understandable notices at the correct time, including for callers whose speech may be processed.
- Minimise collection and avoid ingesting the full contact book unless necessary and justified.
- Set retention periods for raw audio, transcripts, summaries and derived metadata separately.
- Provide appropriate access, correction, deletion and grievance processes as applicable.
- Document processor/subprocessor roles, cross-border transfers, security controls and breach response.
- Review children's data, sensitive disclosures, legal/medical/financial content and profiling risks.

### Telecom and calling rules
TRAI's Telecom Commercial Communications Customer Preference Regulations (TCCCPR) and amendments govern unsolicited commercial communications and related controls. The product's purpose is not assumed to be telemarketing, but outgoing AI calls, automated callbacks, reminders, business outreach or any use of numbers for commercial communication can change the analysis.

Sources:
- TRAI regulations/amendments: https://www.trai.gov.in/release-publication/regulations/amendments-page/7617
- TRAI consumer protection: https://trai.gov.in/telecom/consumer-protection

Do not use the product for automated promotional calling or outbound campaigns without separate telecom-law analysis, consent/registration review and provider approval.

### Recording, interception and caller notice
This research did not establish a single blanket rule that resolves every form of call recording or AI transcription in India. The correct analysis depends on call routing, who records, what notices are given, the parties, purpose and applicable laws. Obtain counsel's opinion before a public pilot. Build caller disclosure, recording/transcription controls, purpose limitation and deletion into the design from the start.

### Android and app-store policy
Android call-screening/redirect APIs are not a general licence to capture cellular audio. Google Play has eligibility and policy constraints around sensitive permissions, default handlers and disclosure. Each permission and role must be justified against current official policy.

Sources:
- Android CallScreeningService: https://developer.android.com/reference/android/telecom/CallScreeningService
- Android CallRedirectionService: https://developer.android.com/reference/android/telecom/CallRedirectionService
- Google Play SMS/call-log permissions: https://support.google.com/googleplay/android-developer/answer/10208820
- Android audio-input sharing: https://developer.android.com/media/platform/sharing-audio-input

### AI provider and voice cloning
Before selecting STT, LLM or TTS providers, review retention, training use, data location, subprocessors, security, abuse monitoring, deletion, incident notification, service availability and commercial rights. Voice cloning or imitation introduces additional identity, impersonation and fraud risks; exclude it from the first release unless there is a compelling, separately reviewed need and robust verification/consent.

## 3. Preliminary risk register

| ID | Risk | Severity | Required control/evidence | Gate |
|---|---|---|---|---|
| PRIV-001 | Caller is unaware that AI is answering | Critical | Prominent caller disclosure; user-facing explanation; counsel review by jurisdiction. | Before real-call pilot |
| PRIV-002 | Recording/transcription lacks a valid basis or notice | Critical | Per-feature data map, legal opinion, notice/consent design, recording default decision. | Before real-call pilot |
| PRIV-003 | Raw audio/transcripts retained longer than necessary | High | Separate retention policies; deletion workflow; provider deletion verification. | Before pilot |
| PRIV-004 | Contact book is over-collected or reused unexpectedly | High | Data minimisation, optional contact access, purpose-specific access and deletion. | Before beta |
| PRIV-005 | Provider uses call content for training or retains beyond expectation | High | Contract/settings review; DPA/subprocessor inventory; provider fallback plan. | Before provider selection |
| PRIV-006 | Call content leaks across users/tenants | Critical | Tenant isolation, authorization tests, least privilege, audit and penetration review. | Before pilot |
| PRIV-007 | AI discloses personal data or commits user to actions | Critical | Restricted tool permissions, confirmation for consequential actions, redaction and adversarial tests. | Before pilot |
| PRIV-008 | Outbound/automated calling violates telecom or anti-spam requirements | Critical | Separate outbound scope; TRAI/provider/legal review and consent controls. | Before outbound feature |
| PRIV-009 | Android permission/Play policy rejection | High | Permission-by-permission policy mapping and current Play-rule review. | Before store submission |
| PRIV-010 | Voice clone enables impersonation or fraud | High | Exclude from MVP or require strong identity/consent checks and misuse controls. | Scope decision |
| PRIV-011 | Cross-border processing conflicts with customer promises or rules | High | Region and transfer review; provider/subprocessor map; truthful disclosures. | Before launch |
| PRIV-012 | Children or highly sensitive calls lack safeguards | High | Explicit age/scope policy, minimisation, restricted profiles and counsel review. | Before public launch |
| PRIV-013 | User cannot stop routing or delete data reliably | Critical | Immediate deactivation, verifiable status, deletion workflow, support escalation and test evidence. | Before pilot |
| PRIV-014 | Breach/provider outage has no response process | High | Incident response, access revocation, notification analysis, recovery exercise. | Before production |

## 4. Minimum privacy-by-design requirements

- Explain call routing and AI handling before activation; require affirmative opt-in.
- Make recording/transcription choices explicit and separate where feasible; legally review whether any feature may be on by default.
- Give callers a clear AI disclosure and an appropriate alternative or end-call path where feasible.
- Keep raw audio, transcripts, summaries and profile context separate with independent retention/deletion rules.
- Do not train on customer call content by default; contractually verify provider behaviour and disclose exceptions.
- Restrict profile context and tools to the authenticated user/tenant. Context must never grant permissions.
- Redact content from operational logs; use access controls, encryption, audit trails and secret rotation.
- Allow user export/deletion where applicable; verify provider deletion and backup schedules.
- Keep a subprocessor register and explain data location/transfer practices truthfully.
- Prohibit arbitrary client-provided URLs, SQL and unrestricted tools.
- Provide incident handling, abuse reporting, account recovery and clear support.

## 5. Required legal questions

1. Who is the data fiduciary/controller for each purpose, and which vendors are processors?
2. Which provisions/rules are in force on the intended launch date under the phased commencement timeline?
3. What notice/consent is needed from the account holder and each caller for routing, AI processing, recording and transcript retention?
4. Are there telecom-provider, number provisioning, call-forwarding or automated-call restrictions for the chosen architecture?
5. How should emergency calls, financial/medical/legal disclosures, minors and highly sensitive content be handled or excluded?
6. What transfer, deletion, grievance, security and breach-notification obligations apply?
7. Which country-specific rules apply before international expansion?

## 6. Decision status

No legal compliance conclusion is approved. Before live-call experiments, the owner must approve a test protocol with participant consent, disclosure, data minimisation, retention/deletion and counsel review appropriate to the actual architecture.

## Official-source freshness note — 2026-10-12

MeitY's current official Act and Policies index lists the Digital Personal Data Protection Rules, 2025 dated 14 November 2025 and related implementation documents: https://www.meity.gov.in/documents/act-and-policies and https://www.meity.gov.in/documents/act-and-policies/digital-personal-data-protection-rules-2025-gDOxUjMtQWa?pageTitle=Digital-Personal-Data-Protection-Rules-2025 . Some PIB summaries use 13 November 2025; for legal work, use the official Gazette instrument, corrigenda and commencement provisions rather than resolving the discrepancy from summaries alone. The Rules provide for phased commencement, so do not assume every provision applies at the same time. TRAI's TCCCPR Third Amendment Regulations, 2026 are listed on its amendments page dated 18 September 2026: https://www.trai.gov.in/release-publication/regulations/amendments-page/7617 . Applicability to the actual call route remains a question for qualified counsel.

This is source maintenance, not a legal opinion or compliance conclusion. Launch geography, route, data flows, provider terms and applicable dates must be confirmed before any real-call pilot or public release.
