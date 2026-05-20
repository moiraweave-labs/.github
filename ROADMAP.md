# MoiraWeave Roadmap

MoiraWeave is an open-source, self-hosted MLOps platform for composing and operating AI inference pipelines.

---

## Released

### v0.3 — Core pipeline execution
- KServe V2 inference protocol (`/v2/models/{id}/infer`)
- `input_from` step routing: chain outputs across pipeline steps
- Redis Streams async job queue with consumer-group delivery
- API gateway with JWT auth, rate limiting, and OpenTelemetry tracing
- Helm chart with NetworkPolicies, RBAC, and KEDA autoscaling
- ExternalSecrets support (AWS + GCP)
- CLI: `moira init`, `step new`, `step add --from-catalog`, `pipeline new/validate`, `flow flow-command`
- Steps catalog: text-embed-fastembed, vector-index-qdrant, vector-search-qdrant, audio-transcribe-whisper, vision-clip

---

## In progress — v0.4

### DX hardening
- [ ] `moira job submit --watch` — submit a job and poll until completion
- [ ] Workspace-aware `flow` (reads step URLs from pipeline.yaml correctly)

### Observability
- [ ] Structured JSON logs on all services (already on api-gateway)
- [ ] Grafana dashboard bundle (latency, queue depth, error rate)
- [ ] Drift detector integration with Evidently

---

## Planned — v0.5

### Pipeline authoring
- [ ] YAML pipeline schema validation with `jsonschema` (reject unknown fields at load time)
- [ ] `moira pipeline graph` — render DOT/Mermaid diagram of the pipeline DAG
- [ ] Multi-output steps: a step can produce named outputs consumed by multiple downstream steps

### Step SDK
- [ ] Streaming inference support (SSE / chunked responses)
- [ ] Batching adapter: collect N requests before forwarding to model
- [ ] GPU memory-aware health checks

### Platform
- [ ] Multi-tenant namespace isolation (per-team namespaces in the same cluster)
- [ ] Pipeline versioning: side-by-side deploy of pipeline v1 and v2 with traffic splitting
- [ ] Prometheus-based SLO alerting rules (latency p99, error budget)

---

## Ideas / Backlog

- Audio-to-text-to-embedding end-to-end pipeline example
- UI dashboard for job status and pipeline topology
- Plugin system for custom trigger sources (HTTP webhook, S3 event, Kafka topic)
- Fine-tuning pipeline support (data prep → training → evaluation → promotion)
- `moira deploy` command — wraps `helm upgrade` with env-specific values

---

## Versioning policy

MoiraWeave follows [Semantic Versioning](https://semver.org/).
Breaking changes in public APIs (pipeline.yaml schema, step SDK, CLI flags) are documented in the relevant `CHANGELOG.md` and gate a minor or major version bump.
