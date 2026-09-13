Serving is guaranteed, dashboard can burst briefly, and batch throttles first.

serving:
  requests:
    cpu: 2
    memory: 256Mi
  limits:
    cpu: 2
    memory: 512Mi

batch:
  requests:
    cpu: 250m
    memory: 256Mi
  limits:
    cpu: 500m
    memory: 512Mi

dashboard:
  # BestEffort: no resource requests or limits

Batch is the first to throttle because unlimited p95 was 4ms, while limited p95 was 3ms.
