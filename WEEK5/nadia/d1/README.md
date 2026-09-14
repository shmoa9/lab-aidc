# AIDC Bootcamp - W5D1
# Monitoring Dashboard and SLI/SLO

## Overview

This lab focuses on building an observability dashboard for an AI serving system using Prometheus and Grafana.

The objective is to monitor service performance, create SLI indicators, and visualize production metrics.

---

## Objectives

- Deploy monitoring components
- Configure Prometheus metrics collection
- Create Grafana dashboards
- Define SLI indicators
- Validate dashboard requirements

---

## Infrastructure

The deployed components:

| Component | Purpose |
|---|---|
| vLLM | AI model serving |
| Prometheus | Metrics collection |
| Grafana | Dashboard visualization |

---

## Dashboard Panels

The dashboard contains:

### Time Series Panel

Shows service performance trends over time.

Metrics include:

- Request activity
- Service behavior
- Performance observations


### Stat Panels

Implemented SLI indicators:

## 1. Completed Requests Per Minute

Measures completed service requests over time.


## 2. Scrape Success Percentage

Measures Prometheus scraping reliability.


## 3. P95 Time To First Token

Measures the 95th percentile latency until the first token is generated.

---

## SLI / SLO Monitoring

The dashboard provides visibility into:

- Service availability
- Request performance
- Model response latency


---

## Validation

Run:

```bash
bash verify.sh

Expected result:

GREEN CHECK: PASS

Status

✅ W5D1 Completed Successfully
