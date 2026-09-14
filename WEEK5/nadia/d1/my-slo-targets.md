# Service indicators and proposed targets

Team: Nadia
Use case: AI chat service using vLLM model
Service measured: vLLM serving endpoint in team namespace
Workload: Chat requests generated using traffic.py
Measurement period: Test run during lab execution
Instrumentation gaps: none

## SLI 1

Indicator: P95 Time To First Token
Panel: P95 Time To First Token
Unit: seconds
Target: Less than 2 seconds
Window: 5 minutes
Observed: 1.2
Evidence: Prometheus vLLM histogram query
Why it fits: Measures user waiting time and responsiveness
Limitations: Limited test duration and sample size

## SLI 2

Indicator: Completed Requests Per Minute
Panel: Panel Title
Unit: requests/min
Target: More than 10 requests/min
Window: 5 minutes
Observed: 25
Evidence: Prometheus vllm request_success_total query
Why it fits: Measures service throughput
Limitations: Requires longer workload testing

## SLI 3

Indicator: Scrape Success Percentage
Panel: Scrape Success %
Unit: percent
Target: More than 99%
Window: 1 hour
Observed: 100
Evidence: Prometheus up query
Why it fits: Confirms monitoring availability
Limitations: Does not measure user request success
