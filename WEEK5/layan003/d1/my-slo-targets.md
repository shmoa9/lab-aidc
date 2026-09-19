# Service indicators and proposed targets

Team: Team 16
Use case: Interactive conversational AI assistant
Service measured: baseline chat engine, /v1/chat/completions, namespace team
Workload: 120 artificial chat requests across 1 to 4 callers, max_tokens=64, model Qwen/Qwen2.5-1.5B-Instruct-AWQ
Measurement period: 2026-09-14 10:02:12 UTC to 2026-09-14 10:05:12 UTC
Instrumentation gaps: none

## SLI 1

Indicator: Time to first token (TTFT) 95th percentile
Panel: TTFT p95 (5m)
Unit: seconds
Target: <= 0.50 seconds
Window: 5 minutes
Observed: 0.028 seconds under artificial traffic
Evidence: Prometheus histogram_quantile query at 2026-09-14 10:05:12 UTC reporting 28.000 ms
Why it fits: Directly measures conversational responsiveness and initial latency perceived by users
Limitations: Estimated via Prometheus histogram quantile buckets; fixed 64-token generation lengths

## SLI 2

Indicator: Completed requests per minute
Panel: Completed requests / min (5m)
Unit: reqpm
Target: >= 2.0 reqpm under active load
Window: 5 minutes
Observed: 2.5 reqpm across the measurement window
Evidence: Prometheus vLLM request_success_total rate query at 2026-09-14 10:05:12 UTC
Why it fits: Verifies throughput capacity and ensures requests finish with valid stop or length conditions
Limitations: 5-minute rolling rate averages include quiet intervals; does not assess output quality