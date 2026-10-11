# Shared Workload Scenario Baseline

**Status:** Proposed planning baseline only; not an approved forecast or capacity commitment.  
**Snapshot:** 2026-10-11. **Owner approval:** Pending.

## Purpose

Provide one reusable low/base/high workload table for capacity and unit-economics discussions. These assumptions are illustrative until replaced by interview evidence, route/provider limits and pilot telemetry. They do not imply that the product can support the route or that users will generate this usage.

## Canonical candidate scenarios

| Input / output | Low | Base | High |
|---|---:|---:|---:|
| Registered accounts | 10,000 | 10,000 | 10,000 |
| Assumed monthly active share | 10% | 25% | 50% |
| Monthly active users (MAU) | 1,000 | 2,500 | 5,000 |
| Calls per MAU per month | 10 | 20 | 30 |
| Average connected minutes per call | 2 | 3 | 4 |
| Calls per month | 10,000 | 50,000 | 150,000 |
| Connected minutes per month | 20,000 | 150,000 | 600,000 |
| 30-day average concurrent calls | 0.46 | 3.47 | 13.89 |
| Illustrative peak concurrency at 10× average | 5 | 35 | 139 |

Formulas:
- `MAU = registered_accounts × MAU_share`
- `monthly_calls = MAU × calls_per_MAU`
- `monthly_connected_minutes = monthly_calls × average_connected_minutes_per_call`
- `average_concurrency = monthly_connected_minutes ÷ 43,200`
- `illustrative_peak = ceil(average_concurrency × 10)`

The 10× peak factor is an arbitrary placeholder inherited from the existing capacity model, not a measured pattern or proposed SLO. Validate a time-of-day burst model before infrastructure sizing. Fractional average concurrency is a monthly average, not a claim that fractional live calls occur.

## Cost sensitivity

The table below applies the same minute scenarios to the broad ₹4/₹7/₹12 per-connected-minute assumptions in `COST_SCENARIO_MODEL.md`. They are sensitivity inputs, not provider quotes.

| Scenario | Monthly minutes | At ₹4/min | At ₹7/min | At ₹12/min |
|---|---:|---:|---:|---:|
| Low | 20,000 | ₹80,000 | ₹1,40,000 | ₹2,40,000 |
| Base | 150,000 | ₹6,00,000 | ₹10,50,000 | ₹18,00,000 |
| High | 600,000 | ₹24,00,000 | ₹42,00,000 | ₹72,00,000 |

A separate ₹6/min public-price anchor (Ringg's advertised bundled voice-agent offer) gives ₹1,20,000 / ₹9,00,000 / ₹36,00,000 for these scenarios. This is a comparison point only; it is not a route-specific quote and must not be treated as the platform's cost forecast. See `PROVIDER_PRICING_EVIDENCE.md`.

These are provider-variable-cost illustrations only. They exclude any non-included number rental, forwarding/carrier charges, extra call legs, taxes, payment fees, app-store fees, retries, support, acquisition, fixed infrastructure and other overhead.

## Important unresolved metric: AI-active time

Connected minutes and AI-active minutes may differ. If billing is based on audio streamed, model session time, token/audio usage or a subset of the call, this table is insufficient for invoicing. Provider RFPs must state each billable unit, and pilot instrumentation must capture both connected duration and each billable component where available.

## Do not infer concurrency from monthly minutes alone

Before a capacity decision, collect:
- per-hour and 5-minute call arrival distributions;
- call-duration distribution and long-call tail;
- concurrent session limits and calls-per-second limits by provider;
- transfer/takeover call legs and reconnect behaviour;
- AI-active versus connected duration;
- failed attempts, retries and webhook duplication;
- latency and failure rates at peak load.

Use measured p95/p99 peak concurrency and a burst scenario to approve capacity and spend limits. Do not use the illustrative 10× multiplier as a release acceptance target.

## Reconciliation rule

- Use this document as the shared planning table for cost and capacity calculations while its assumptions are in force.
- Keep the older 10k/75k/240k-minute cases in `COST_SCENARIO_MODEL.md` only as an alternate usage sensitivity set; label them explicitly as a separate set, not directly comparable with the canonical low/base/high workload.
- Do not silently replace these assumptions after interviews or tests. Record evidence, version, change rationale and owner decision.
- Recalculate every cost table when provider quote scope, billing units or scenario assumptions change.

## Evidence and approval required

1. Customer interviews that capture call frequency and duration without leading respondents.
2. Written route-specific provider quotes and concurrency/CPS limits.
3. Controlled end-to-end route tests.
4. A stated target for 10,000 registered users with MAU, minute and peak distributions.
5. Owner approval of the planning assumptions before they are used as committed budget or SLO inputs.

No product or infrastructure choice is made by this scenario document.
