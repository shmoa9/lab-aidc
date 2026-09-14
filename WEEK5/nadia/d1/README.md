# AIDC Bootcamp - W5D1

## Monitoring Dashboard and SLI/SLO

### Overview

Built a Grafana monitoring dashboard for the AI serving service using Prometheus metrics.

The dashboard provides service visibility through SLI indicators and performance monitoring panels.

---

## Components

- vLLM AI Serving
- Prometheus Metrics
- Grafana Dashboard

---

## Dashboard Panels

### Time Series Panel

- Service Metrics Trend

### Stat Panels

- Completed Requests Per Minute
- Scrape Success Percentage
- P95 Time To First Token

---

## SLI Indicators

### Completed Requests Per Minute

Measures completed service requests over time.

### Scrape Success Percentage

Measures Prometheus metric collection reliability.

### P95 Time To First Token

Measures the 95th percentile latency before the first generated token.

---

## Validation

Command:

```bash
bash verify.sh
```

Result:

```
GREEN CHECK: PASS
```

---

## Status

```
✅ W5D1 Completed Successfully
```
