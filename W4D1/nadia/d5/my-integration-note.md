# Integration note: team (v1, go-live)

- **base_url** (client form, ends in `/v1` - paste into an OpenAI client):
  `https://t16.aidc.nadir.sh/v1`

- **service root** (no `/v1` - the runbook's triage curls and `verify.sh`
  build paths from this): `https://t16.aidc.nadir.sh`

- **model id:** `Qwen/Qwen2.5-1.5B-Instruct-AWQ`

- **auth:** bearer key, handed over in person

- **modalities:** text in, text out, tool calls per the OpenAI schema. text only

- **example call:** the exact `curl` from your green check, with the key
  redacted

- **SLOs we publish:** availability 99% over the window · TTFT p95 < 1000 ms
  (tier 1) or e2e p95 < 1000 ms (tier 0) · error rate < 1%

- **limits, declared honestly:** max_tokens clamp 4096 · concurrency knee ~1
  (from your wk-3 bench) · standard OpenAI-compatible serving

- **on-call:** team · DM · response within 10 minutes during the window
