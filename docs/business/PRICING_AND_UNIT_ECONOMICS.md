# Pricing and Unit Economics — Research Framework

Status: RESEARCH_REQUIRED. No price or plan is approved. India/INR is a candidate scenario, not a confirmed exclusive launch geography.

## Questions
- Who pays: individual, professional, small business or hospitality property?
- Subscription, usage-based, bundled minutes or hybrid?
- Plan limits for numbers, minutes, concurrency, languages, history, transcripts, recordings, integrations and retention?
- What counts as billable time? How are failed, transferred, retried and forwarded calls charged?
- How will free trials, overages and abuse be controlled?
- What margin covers fixed infrastructure, support, acquisition and taxes?

## Cost categories
Telephony number rental and minutes; media transport; speech recognition; model inference; TTS; recording/transcript storage; networking; failed calls/retries/fallbacks; monitoring/security/backups/support; fixed provider minimums and infrastructure; payment fees/taxes/currency conversion; customer acquisition and onboarding.

Normalise units before comparison. Verify whether prices include telephony, streaming, taxes, minimum commitments, region and plan restrictions.

## Required low/base/high scenarios
Registered, active and paying users; calls per active user; average and p95 duration; AI-active fraction; transfer/fallback rate; provider mix; retention; monthly concurrency and peak arrivals; source/confidence for prices; revenue, discounts, variable cost, gross profit/margin, break-even and sensitivity to minutes/user, price and paid conversion.

## Simplified model
- monthly_minutes = monthly_active_users × calls_per_user_per_month × average_minutes_per_call
- voice_variable_cost = monthly_minutes × blended_variable_cost_per_minute
- total_variable_cost = voice_variable_cost + other_variable_costs
- gross_profit = recognised_revenue − total_variable_cost
- gross_margin = gross_profit ÷ recognised_revenue

The complete model must add fixed costs, refunds, taxes, payment fees, support and acquisition economics. These formulas are not a forecast.

## Pricing gate
Do not finalise price until willingness-to-pay has evidence, realistic costs are verified or transparently scenario-modelled, limits map to value and cost, abuse/overage are considered, downside margin is acceptable, billing/dispute flows are specified, and the owner approves the hypothesis.