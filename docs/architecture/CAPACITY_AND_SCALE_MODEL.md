# Capacity and Scale Model — 10,000 Registered Users

**Status:** Initial workload hypothesis, not a sizing commitment. Research date: 2026-10-11. Product implementation remains unauthorised.

## 1. Why registered users are not a capacity target

10,000 registrations do not tell us how many calls will happen at once. Capacity depends on monthly active users, calls per active user, connected duration, peak-hour distribution, streaming sessions, provider concurrency limits, retries, and whether each call uses one or multiple media legs.

This model is a planning instrument. Replace all assumptions with interview evidence, provider limits and measured pilot telemetry before production sizing.

## 2. Illustrative scenarios

Assumptions: 30-day month (43,200 minutes), all listed minutes are billable connected minutes, and a provisional 10× peak-to-average concurrency multiplier. The 10× multiplier is deliberately only a placeholder; actual call arrivals may be more bursty.

| Scenario | Registered users | Monthly active share | MAU | Calls/MAU/month | Avg min/call | Minutes/month | Avg concurrent calls | Illustrative peak at 10× |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Low | 10,000 | 10% | 1,000 | 10 | 2 | 20,000 | 0.46 | 5 |
| Base | 10,000 | 25% | 2,500 | 20 | 3 | 150,000 | 3.47 | 35 |
| High | 10,000 | 50% | 5,000 | 30 | 4 | 600,000 | 13.89 | 139 |

Formula:
- monthly_minutes = MAU × calls_per_MAU_per_month × average_connected_minutes
- average_concurrency = monthly_minutes ÷ 43,200
- illustrative_peak_concurrency = average_concurrency × assumed_peak_factor

The peak factor is not evidence. Validate with expected calling patterns and pilot measurements; also model a flash peak, such as a concentrated time-of-day or post-event burst.

## 3. Provider-cost sensitivity using public ₹6/min benchmark

Using Ringg's public voice-agent pricing as a reference only—not a quote for this product and not proof of identical routing support:

| Scenario | Minutes/month | Illustrative provider spend |
|---|---:|---:|
| Low | 20,000 | ₹1,20,000 |
| Base | 150,000 | ₹9,00,000 |
| High | 600,000 | ₹36,00,000 |

Source: https://www.ringg.ai/pricing (accessed 2026-10-11). Confirm price applicability, tax, number rental, included components, rounding, concurrency and regional terms directly with the provider. Cost model excludes any items not included in that rate.

## 4. Capacity dimensions to measure

### Telephony and media
- Concurrent live sessions and calls/second at peak.
- Per-account, per-number and per-region concurrency limits.
- WebSocket/media connection count, bandwidth, packet loss, jitter and reconnect rate.
- Audio chunk size, encoding/transcoding CPU and memory.
- Call setup time, connect rate, disconnect rate, transfer legs and retries.
- Maximum call duration and long-call behaviour.

### AI pipeline
- Speech recognition latency and error rate by language/noise condition.
- Model time-to-first-token and turn-completion latency.
- TTS first-audio latency and interruption/barge-in responsiveness.
- Tokens or audio seconds per minute, tool calls per call, retries and fallback rate.
- Provider quotas, rate limits, regional availability and failure behaviour.
- p50/p95/p99 end-to-end response latency, not just per-provider benchmarks.

### Backend
- API requests per call/session and events per second.
- Concurrent stateful sessions, queue depth and backpressure behaviour.
- DB connection count, hot records, retention size and query latency.
- Transcript/audio storage volume, retention and deletion workload.
- Webhook retries/idempotency, duplicate events and out-of-order disconnects.
- Tenant isolation, abuse quotas and noisy-neighbour controls.

### Operations
- SLOs for successful routing, call connection, response latency, unexpected termination and data durability.
- Dashboards and alerts for provider health, spend, concurrency, errors, latency and safety incidents.
- Graceful degradation if model/STT/TTS/media provider fails.
- Backup/restore, incident response, key rotation and provider failover exercises.
- Load test, soak test, burst test and recovery test before a public launch.

## 5. Architecture implications

- Do not hold a request/worker slot for an entire call unless the runtime and cost model explicitly support that design.
- Separate call control from media streaming and AI orchestration where the chosen provider requires it.
- Use asynchronous events, bounded queues, idempotent webhook handlers, explicit session state and deadline-aware retries.
- Enforce concurrency and spend limits per user, tenant, provider and global pool.
- Apply admission control and safe fallback when capacity is exhausted; never silently drop or misroute a call.
- Separate low-latency realtime traffic from batch transcript summarization and analytics.
- Measure and limit retained audio/transcript volume; apply deletion and lifecycle policies.
- Keep provider adapters replaceable, but do not abstract away provider-specific realtime semantics that affect reliability.

These are design principles, not a final architecture or technology selection.

## 6. Load-test acceptance targets to decide later

Before implementation, the owner and engineering lead should approve explicit targets for:
- Peak simultaneous calls and call arrivals/second.
- Successful setup and session completion rates.
- p95/p99 time to first response audio and interruption handling.
- Provider failover/recovery time.
- Maximum monthly spend and per-user cost guardrails.
- Data isolation, deletion and audit correctness under concurrent load.
- Sustained-load duration and burst profile.

Targets must come from customer expectations, carrier/provider constraints and economics, not arbitrary round numbers.

## 7. Next evidence

1. Collect user call-volume and duration distributions through discovery interviews.
2. Get written provider limits and quotes for concurrent sessions, streaming and call setup.
3. Build low/base/high scenarios for AI-active minutes, not only connected minutes, if billing differs.
4. Confirm whether human takeover creates extra billable legs.
5. Measure pilot traffic by hour/day and fit a peak factor.
6. Recompute infrastructure and operations cost, then define test scenarios and SLOs.
7. Update this model after any architecture or provider decision.

## 8. Decision status

10,000 is a registration target only. No production concurrency target, provider, SLO, infrastructure shape or budget is approved.