# Service report

Team:10
Use case: AI model serving
Service and model:vLLM — Qwen/Qwen2.5-1.5B-Instruct-AWQ
Measured requests or tasks: 120 requests
Indicator and unit: CTTFT p95 (5m), seconds
SLO target and window:50 ms (0.05 s)
Measurement start and end:2026-09-14T10:33:52Z — during the W5D2 traffic run
Workload:Artificial chat traffic generated using traffic.py
Observed result and sample count: 0.0389 s (38.9 ms), 120 requests
Evidence: Grafana Team service alert 1; notification-evidence.jsonl
Conclusion:Met
Limitations:This was a short artificial workload and does not establish compliance over a longer production SLO window. Traffic volume and Prometheus scrape timing may affect the measurement.
Follow-up action:Repeat the measurement with representative production-like traffic over the full SLO window.

## Measurement query

```promql
histogram_quantile(0.95, sum by (le) (rate(vllm_time_to_first_token_seconds_bucket{job="serving"}[5m])))
```
## Service alert

Condition and unit: TTFT p95 (5m) above 0.05 seconnds
Evaluation interval: 1m
Pending period:1m
Relationship to the SLO:Alert fires when TTFT p95 exceeds the 50 ms SLO target.
First response to a notification: Check the vLLM serving service, recent traffic, and Prometheus metrics.

## Notification test

Firing received at: 2026-09-14T10:20:00Z
Resolved received at: 2026-09-14T10:21:00Z
What the test establishes: The webhook receiver successfully received both firing and resolved notifications for the artificial alert, confirming notification delivery and recovery.
