# MoiraWeave Labs

**Open, modular MLOps platform for orchestrating, monitoring and scaling AI inference pipelines.**

Define your pipeline in YAML. Deploy with one command. Scale each step independently.

```yaml
# moiraweave.yaml
steps:
  - id: transcribe
    task: audio-transcribe
    url: http://whisper-stt:8080
  - id: embed
    task: text-embed
    url: http://fastembed:8080
  - id: index
    task: vector-index
    url: http://qdrant:8080
```

```bash
moira pipeline validate moiraweave.yaml
moira pipeline run moiraweave.yaml --input audio.mp3
```

## Repositories

| Repo | Description |
|------|-------------|
| [moiraweave-core](https://github.com/moiraweave-labs/moiraweave-core) | Runtime platform: API gateway + Redis Streams worker + Helm charts |
| [moiraweave-steps](https://github.com/moiraweave-labs/moiraweave-steps) | Community catalog of reusable inference steps |
| [moiraweave-cli](https://github.com/moiraweave-labs/moiraweave-cli) | Developer CLI — `pip install moiraweave-cli` |
| [moiraweave-docs](https://github.com/moiraweave-labs/moiraweave-docs) | Documentation — [moiraweave-labs.github.io/moiraweave-docs](https://moiraweave-labs.github.io/moiraweave-docs/) |

## Tech stack

FastAPI · Redis Streams · Qdrant · Kubernetes · Helm · ArgoCD · Prometheus · Grafana · Jaeger · Python 3.13

## Links

- 📖 [Documentation](https://moiraweave-labs.github.io/moiraweave-docs/)
- 🐛 [Report an issue](https://github.com/moiraweave-labs/moiraweave-core/issues)
- 💬 [Discussions](https://github.com/moiraweave-labs/moiraweave-core/discussions)
