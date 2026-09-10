Policy: Serving gets guaranteed resources to meet its p95 SLO, dashboard bursts on refresh, and batch throttles first under heavy load.

Resources:
  - serving:
      requests: { cpu: 250m, memory: 2.5Gi }
      limits: { cpu: "1", memory: 2.5Gi }
  - dashboard:
      requests: { cpu: "100m", memory: "128Mi" }
      limits: { cpu: "500m", memory: "256Mi" }
  - batch:
      requests: { cpu: "50m", memory: "128Mi" }
      limits: { cpu: "500m", memory: "512Mi" }

Defense: Our measurements show that an unconstrained noisy neighbor degrades p95 latency to 5ms, whereas applying a 500m limit stabilizes p95 latency at 3ms, justifying throttling the deadline-free batch job to protect serving SLOs.