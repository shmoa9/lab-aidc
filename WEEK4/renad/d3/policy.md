Policy: Serving gets guaranteed resources because it has a latency
SLO — if it slows down, real users feel it. Dashboard can burst a
bit when someone refreshes it, since that's short and rare. Batch
throttles first because it has no deadline, so it's fine if it just
runs slower.

Resources (4-CPU node):

serving:
  requests:
    cpu: "1"
    memory: 512Mi
  limits:
    cpu: "1"
    memory: 512Mi
  # requests == limits -> Guaranteed QoS

dashboard:
  requests:
    cpu: 200m
    memory: 128Mi
  limits:
    cpu: 500m
    memory: 256Mi
  # Burstable

batch:
  requests:
    cpu: 100m
    memory: 128Mi
  limits:
    cpu: 500m
    memory: 256Mi
  # Burstable, but lowest requests -> first to get squeezed

Defense: When I ran 20 unlimited noisy-neighbour pods against my
serving pod, p95 latency was 4ms. With the neighbours limited to
500m cpu, p95 was 3ms. Barely any difference, and zero failed
requests either way. That happened because serving already had
CPU requests set from Step 1, so the kernel favored it over the
burner pods even when they had no limit at all. This is why batch
is the safe one to throttle: the same protection that kept serving
fast in my test will keep it fast when batch is the one competing
for CPU, and batch loses nothing since it has no deadline anyway.
