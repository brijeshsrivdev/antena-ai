# Initial Voice-Stack Candidate Review

**Status:** Early desk review only; no technology/provider is selected. Date: 2026-10-11. This review does not authorise implementation.

## 1. Executive summary

Three open-source realtime voice orchestration frameworks merit further evaluation: LiveKit Agents, Pipecat and Vocode Core. They are orchestration frameworks, not turnkey proof of a supported consumer cellular-call-routing path. None removes the need to validate carrier forwarding, PSTN/SIP integration, caller disclosure, live takeover, regional availability, provider contracts and all-in cost.

A reasonable next step after the owner approves experiments would be a small, non-production proof-of-feasibility comparison of one framework against a minimal direct provider integration. No framework should be selected from GitHub stars or a quickstart alone.

## 2. Candidate comparison

| Candidate | Official positioning | Licence evidence checked | Potential fit | Risks / open questions |
|---|---|---|---|---|
| LiveKit Agents | Realtime voice/video agent framework; supports multiple STT/LLM/TTS providers, dispatch/job scheduling, testing and telephony integrations. | Repository LICENSE is Apache-2.0. MODEL_LICENSE separately restricts LiveKit's turn-detection models to use with the LiveKit Agents framework and not standalone/other frameworks. | Strong candidate if we need a realtime media/session layer and want provider choice. | Confirm whether the required India PSTN route is supported by the chosen telephony product; cloud costs and model/provider fees; model licence and each plugin's own licence; deployment and operations burden. |
| Pipecat | Open-source Python framework for realtime voice and multimodal pipelines, with integrations for transport and AI services. | Repository LICENSE is BSD 2-Clause (checked from main at research time). | Potentially flexible pipeline orchestration with lower framework coupling. | Verify current maintenance, plugin/dependency licences, telephony integrations and production patterns; no guarantee that PSTN routing is included in framework licence or price. |
| Vocode Core | Open-source library for voice-based LLM agents; repository describes phone-call and other integrations. | Repository LICENSE is MIT (checked from main at research time). | Potentially useful reference or lightweight alternative. | Verify current release cadence, compatibility with current provider APIs, issue/maintenance state, dependencies and operational suitability before considering it production-ready. |
| Direct managed realtime API | Use a hosted realtime voice/model API behind a thin server-side adapter. | Commercial API terms and pricing apply; no open-source licence for the hosted service. | May reduce orchestration code and time-to-first-experiment. | Model usage is only one part of total cost; telephony/media, storage, tools and usage terms remain. Avoid provider lock-in with explicit contracts and measured exit cost. |

## 3. Official sources checked

- LiveKit Agents repository: https://github.com/livekit/agents
- LiveKit Agents license: https://raw.githubusercontent.com/livekit/agents/main/LICENSE
- LiveKit Model License: https://raw.githubusercontent.com/livekit/agents/main/MODEL_LICENSE
- LiveKit Agents documentation: https://docs.livekit.io/agents/
- Pipecat repository: https://github.com/pipecat-ai/pipecat
- Pipecat licence: https://raw.githubusercontent.com/pipecat-ai/pipecat/main/LICENSE
- Vocode Core repository: https://github.com/vocodedev/vocode-core
- Vocode licence: https://raw.githubusercontent.com/vocodedev/vocode-core/main/LICENSE
- OpenAI API pricing: https://developers.openai.com/api/docs/pricing
- Ringg voice-agent pricing: https://www.ringg.ai/pricing

Accessed 2026-10-11. Branch-main licence links are mutable; record exact commit/tag and re-check the licence before any dependency approval. These source checks cover repository-level licences only, not all transitive dependencies, plugins, model weights, datasets or hosted-provider terms.

## 4. Cost comparison cautions

OpenAI's current API pricing page lists GPT-Live sessions at US$0.05/minute and states backend model/tool usage is charged separately. This is not an all-in telephony call price and should not be compared directly with a bundle that includes PSTN, speech, model and basic analytics.

Ringg advertises ₹6/connected minute for a voice-agent bundle that includes telephony, proprietary STT, natural TTS, a fine-tuned LLM and basic analytics. This is a useful market benchmark, not a verified quote for the exact personal-call routing path.

Sources:
- https://developers.openai.com/api/docs/pricing
- https://www.ringg.ai/pricing

Any cost model must identify included/excluded legs and prevent double-counting. Model at least:
- carrier/PSTN inbound or forwarded call leg;
- media streaming/SIP/WebRTC;
- STT input audio;
- LLM input/output or realtime session;
- TTS output audio;
- tool/API usage;
- recording, storage and transcript indexing;
- human takeover/transfer legs;
- failures, retries, minimum billable duration, taxes and currency conversion.

## 5. Preliminary evaluation hypothesis

- Keep the media and orchestration boundary explicit so providers can be compared.
- Prefer the smallest architecture that meets measured latency, routing and reliability requirements.
- Do not self-host speech/model components until quality, cost and operational trade-offs are measured against managed options.
- If using LiveKit, review the separate model licence rather than assuming Apache-2.0 covers all associated models.
- If using Pipecat or Vocode, audit every integration and transitive dependency before production.
- Treat frameworks as implementation candidates only after telephony feasibility; a good framework cannot solve unsupported carrier routing.

## 6. Required evaluation experiment (after explicit owner approval)

1. Use a controlled synthetic/test audio scenario first; no real customer calls.
2. Implement the same narrow conversation loop in two candidate paths only after the owner approves the experiment.
3. Measure end-to-end p50/p95/p99 time to first response audio, interruption handling, barge-in, disconnect recovery, memory/CPU, session concurrency and cost.
4. Test English/Hindi and code-switching only where providers claim support.
5. Test provider outage, malformed input, long silence, noisy audio and tool timeout.
6. Verify logs contain no raw audio/transcript by default and user/session boundaries are enforced.
7. Compare operational burden, data terms, licences and migration cost.
8. Record results and make a recommendation; do not implement product features or deploy to production.

## 7. Decision status

No framework, model, provider, media server or licence approach is approved. Next work is to validate the actual call path, collect provider quotes, inspect exact versions/licences and define measurable test criteria.