# MoiraWeave Labs

**Self-hosted AI workload and agent operations platform.**

MoiraWeave deploys and operates model services, pipelines, and long-running
agent runtimes from one manifest model. It manages the control plane around
agents: sessions, messages, runs, events, logs, cancellation, health, and
artifacts. The agent runtime keeps its own reasoning loop, tools, memory, and
domain behavior.

```yaml
apiVersion: moiraweave.io/v1alpha1
kind: Workload
metadata:
  name: hermes
spec:
  type: agent-service
  image: ghcr.io/nousresearch/hermes-agent:latest
  execution:
    mode: session
    timeoutSeconds: 172800
  ports:
    - name: http
      port: 8000
  agent:
    adapter: hermes
    workspaceMount: /workspace
    exposedChannels: [ui, api]
```

```bash
moira init
moira workload new hermes --type agent-service --adapter hermes
moira deploy local --up
moira agent session create hermes
```

## Repositories

| Repo | Description |
|------|-------------|
| [moiraweave-core](https://github.com/moiraweave-labs/moiraweave-core) | Runtime, API gateway, workers, Helm, Compose, and control-plane storage |
| [moiraweave-cli](https://github.com/moiraweave-labs/moiraweave-cli) | User CLI for workspace init, workload manifests, runs, agents, and deploys |
| [moiraweave-ui](https://github.com/moiraweave-labs/moiraweave-ui) | Integrated Ops dashboard for workloads, runs, sessions, artifacts, and health |
| [moiraweave-docs](https://github.com/moiraweave-labs/moiraweave-docs) | Product and architecture documentation |

## Tech Stack

FastAPI · Postgres · Redis Streams · Qdrant · React · Kubernetes · Helm ·
Prometheus · Jaeger · Python 3.13

## Links

- [Documentation](https://moiraweave-labs.github.io/moiraweave-docs/)
- [Report an issue](https://github.com/moiraweave-labs/moiraweave-core/issues)
- [Discussions](https://github.com/moiraweave-labs/moiraweave-core/discussions)
