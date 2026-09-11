# HPA Failure Analysis

## Where the CPU-based scaler fails

The CPU-based HPA works fine for the echo backend, because that
backend actually uses CPU. When we sent load to it, CPU went up to
300-400% and the HPA scaled to 3 replicas quickly. That part worked.

But when we tested the real vLLM engine the same way, CPU stayed
low the whole time: only about 994-1055m out of a 4000m request,
around 25%. At the same time, nvidia-smi showed the GPU at 97%
usage, almost fully busy.

This means the HPA would look at CPU, see only 25%, and think
everything is fine. It would never add more replicas. But the GPU
is actually maxed out and requests are piling up. So this scaler
would fail during a real traffic spike, because it is watching the
wrong number.

## Better signal to use instead

I would use vllm_num_requests_waiting (queue depth) instead of CPU.
This number shows how many requests are waiting to be processed.
For an LLM engine, this is a much better sign of real load than CPU,
because CPU stays low even when the engine is very busy.

## Starting target and what to check

I would start with a target of about 5 waiting requests per replica.
Then I would watch response time (p95 latency) to check if this
number is right. If latency stays good, I can raise the target to
save cost. If latency gets worse, I should lower the target so the
system scales out sooner.
