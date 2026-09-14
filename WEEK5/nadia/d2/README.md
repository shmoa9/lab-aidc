# AIDC Bootcamp - W5D2

## Alerting and Notification Pipeline

### Overview

Implemented Grafana alerting and notification workflow for the AI serving service.

Configured alert rules, notification delivery, recovery testing, and service reporting.

---

## Components

- Grafana Alert Rules
- Prometheus Queries
- Alert Inbox Service
- Notification Evidence
- Service Report

---

## Alert Rules

### Team Service Alert

Configuration:

- Evaluation interval: 1m
- Pending period: 1m
- Prometheus based query

---

### Lab Notification Test

Verified:

- Alert firing state
- Alert resolved state
- Recovery workflow
- Alert pause after recovery

---

## Notification Evidence

Collected from:

```bash
kubectl -n "$NAMESPACE" logs deploy/alert-inbox
```

Verified:

```
✅ Firing notification
✅ Resolved notification
```

---

## Service Report

Created:

```
my-service-report.md
```

Includes:

```
Team
Use case
Service and model
Measurement query
SLO target
Workload
Evidence
Conclusion
Limitations
Follow-up action
```

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
✅ W5D2 Completed Successfully
```
