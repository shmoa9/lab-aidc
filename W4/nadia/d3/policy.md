Policy: Serving gets guaranteed resources to meet its p95 SLO, batch bursts when idle, and batch/dashboard throttles first under heavy load.

Resources:
  - serving:
      requests: { cpu: "1", memory: "1Gi" }
      limits: { cpu: "2", memory: "2Gi" }
  - dashboard:
      requests: { cpu: "100m", memory: "128Mi" }
      limits: { cpu: "500m", memory: "256Mi" }
  - batch:
      requests: { cpu: "100m", memory: "128Mi" }
      limits: { cpu: "500m", memory: "512Mi" }

Defense: Based on our p95 measurements, an unbounded neighbour spikes latency drastically, whereas a 500m limit keeps the p95 flat and predictable.
