# Service indicators and proposed targets

Team: Team 2 (RFP AI) - t16
Use case: This is the standard lab chat engine, used here as a baseline before we deploy our own model for the RFP project (extracting requirements from English/Arabic RFP documents). Once our project model is running, TTFT and output validity numbers will likely change.
Service measured: Qwen/Qwen2.5-1.5B-Instruct-AWQ, job "serving" (instance team-serving:8000), namespace team
Workload: traffic.py — one caller for 60s, a 30s pause, then four callers at once for 60s, max 64 output tokens, 120 requests total
Measurement period: 2026-09-13T11:52:40Z to 2026-09-13T11:55:40Z (UTC)
Instrumentation gaps: there's no HTTP status counter (http_requests_total) on the engine, so we can only measure request success through vllm:request_success_total, not real end-to-end HTTP outcomes

Complete two SLI sections. Copy one section if you choose a third. Use the exact
stat-panel title for Panel. Keep the field labels so the verifier can read them.
Support each target with observed measurements.

## SLI 1

Indicator: p95 time to first token
Panel: TTFT p95 (5m)
Unit: milliseconds
Target: keep p95 TTFT under 100 ms (this is just a diagnostic threshold for now, not a confirmed SLO)
Window: 5 minutes (the rate() query window), same for the SLO window
Observed: about 39 ms while under load from four callers, dropping to 28-30 ms during the quiet gaps, and steady around 37-38 ms during the single-caller phase
Evidence: histogram_quantile(0.95, sum by (le) (rate(vllm:time_to_first_token_seconds_bucket{job="serving"}[5m]))), checked on 2026-09-13 around 13:52 local time on the "Team service" dashboard
Why it fits: first-token speed matters for any chat-style interaction, and it gives us a baseline to compare against once our own RFP model is running
Limitations: this is based on one short (~3 min) synthetic test with only 64 output tokens, so it doesn't reflect real RFP-document-length prompts. Histogram percentiles are also just estimates based on bucket ranges, not exact numbers. Needs to be retested with realistic prompt sizes.

## SLI 2

Indicator: completed requests per minute (requests that finished with reason stop or length)
Panel: Completed requests / min (5m)
Unit: requests/min
Target: sustain at least 20 req/min under load (diagnostic only — the test was too short to commit to a real SLO)
Window: 5 minutes (the rate() query window), same for the SLO window
Observed: 0 req/min during idle periods, rising to about 25 req/min while four callers were active
Evidence: 60 * sum(rate(vllm:request_success_total{job="serving", finished_reason=~"stop|length"}[5m])), checked on 2026-09-13 around 13:52 local time on the "Team service" dashboard
Why it fits: this shows how many document-processing requests the engine can handle per minute, which matters directly for processing batches of RFP documents
Limitations: this doesn't count aborted or error requests, and it doesn't tell us if the output was actually correct (e.g. valid JSON). Zero during idle time isn't a failure, just no traffic. Needs retesting with load levels closer to what the actual project will see.