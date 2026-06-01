# MoiraWeave Roadmap

MoiraWeave is an open-source, self-hosted operations platform for AI workloads:
model services, pipelines, and long-running agent runtimes.

MoiraWeave is the control and deployment plane. Hermes, OpenClaw, LangGraph, or
custom agents keep their own reasoning loop, tools, memory, and runtime-specific
behavior.

## Current Direction

### v0.4: AI Workload Control Plane
- Workload manifests replace legacy pipeline/job terminology.
- Postgres stores workloads, runs, sessions, events, and artifact metadata.
- Redis is limited to queueing and short-lived worker coordination.
- Docker Compose and Helm render from the same `workload.yaml` model.
- Ops dashboard covers workloads, runs, agent sessions, events, artifacts, and health.

### v0.5: Durable Agent Operations
- Formal agent adapter contract: dispatch, status, cancel, artifacts.
- First adapters: `generic-http`, `hermes`, and `openclaw`.
- Short-lived dispatch calls for long-running agents.
- Run timeouts, stale-run recovery, dead-letter handling, and lifecycle guards.
- Agent session history stores user and assistant messages.

### v0.6: Deployment And Governance
- Deployment records for local and Kubernetes environments.
- Deploy status, logs, undeploy, validation, and health per workload.
- API keys, RBAC roles, audit trail, and environment-scoped secrets.
- Channel connectors: UI/API first, then Telegram, Slack/Discord, and webhooks.

## Backlog

- Professional architecture diagrams: C4 context, containers, components, and key sequences.
- UI architecture refactor: keep `moiraweave-ui/src/App.tsx` as routing and shell only, with route screens, shared components, hooks, and typed utilities split into dedicated modules.
- UI polish: workload editor, run timeline, live events, agent chat, artifacts, deployment health.
- E2E scenarios: mock model, mock pipeline, mock long-running agent, cancel, stale recovery.
- Comparison docs against LangGraph/LangSmith, Dify, Temporal, and Ray Serve.
- Migration docs for users moving from legacy pipeline/job concepts.

## Versioning Policy

MoiraWeave follows Semantic Versioning. Breaking changes in public APIs,
`workload.yaml`, CLI commands, or Helm values must be documented in changelogs.
