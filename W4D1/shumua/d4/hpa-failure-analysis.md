Today's CPU-based HPA fails for the real vLLM engine because vLLM is GPU-bound. During the load test, CPU usage was low while GPU utilization was high.

For my workload, I would use GPU utilization and engine queue depth (vllm_num_requests_waiting) as scaling signals because they better represent the actual serving pressure.

I would start with a target of 70% GPU utilization and monitor latency, queue depth, and GPU utilization to tune it
