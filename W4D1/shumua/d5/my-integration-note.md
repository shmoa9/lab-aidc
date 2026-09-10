# Integration note: shumua (v1, go-live)

- *base_url:* https://t16.aidc.nadir.sh/v1
- *service root:* https://t16.aidc.nadir.sh
- *model id:* Qwen/Qwen2.5-1.5B-Instruct-AWQ
- *auth:* bearer key, handed over DM to their on-call, never in this file
- *modalities:* text in, text out. Text only.
- *example call:* curl -s https://t16.aidc.nadir.sh/v1/chat/completions -H "Authorization: Bearer REDACTED" -H 'Content-Type: application/json' -d '{"model":"Qwen/Qwen2.5-1.5B-Instruct-AWQ","messages":[{"role":"user","content":"hello from outside"}]}'
- *SLOs we publish:* availability 100% over the window · TTFT p95 < 2.0 s · error rate 0%
- *limits, declared honestly:* concurrency knee ~4 · load shedding cap 8
- *on-call:* team on-call · DM
