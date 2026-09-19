# Service report

Team: Team 16
Use case: Interactive conversational developer assistant serving chat completions
Service and model: baseline chat engine, Qwen/Qwen2.5-1.5B-Instruct-AWQ, namespace team
Measured requests or tasks: Completed HTTP chat completions through /v1/chat/completions
Indicator and unit: Completed requests throughput in requests/min
SLO target and window: >= 2.0 reqpm over a 5-minute window
Measurement start and end: 2026-09-14 10:02:12 UTC to 2026-09-14 10:05:12 UTC
Workload: 120 requests, 1 to 4 callers, max 64 tokens, generated via traffic.py
Observed result and sample count: 2.5 reqpm (0.03158 req/s) across 120 completed requests
Evidence: deploy/alert-inbox notification logs
Conclusion: met
Limitations: Short 3-minute test workload with idle pauses; fixed 64-token cap does not test variable real-world generation lengths
Follow-up action: Expand load testing to 15-minute continuous concurrent sessions to evaluate behavior under persistent queue pressure

## Measurement query

```promql
60 * sum(rate(vllm:request_success_total{job="serving",finished_reason=~"stop|length"}[5m])) or 60 * sum(rate(vllm_request_success_total{job="serving",finished_reason=~"stop|length"}[5m]))

## Service alert

Condition and unit: sum(rate(vllm:request_success_total[5m])) is below 0.033 req/s (equivalent to 2.0 reqpm)
Evaluation interval: 1m
Pending period: 1m
Relationship to the SLO: Alerts when the 5-minute throughput rate drops below the minimum acceptable operational floor of 2.0 reqpm during expected usage
First response to a notification: Inspect kubectl describe pod for the serving engine, check Prometheus up metric, and check queue saturation

## Notification test

Firing received at: 2026-09-14T08:45:25+00:00
Resolved received at: 2026-09-14T08:50:25+00:00
What the test establishes: Confirms end-to-end webhook delivery from Grafana alert manager to the alert-inbox service inside the Kubernetes cluster for both state transitions