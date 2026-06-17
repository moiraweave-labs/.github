# MoiraWeave Roadmap

MoiraWeave is an open-source, self-hosted operations platform for AI workloads:
model services, pipelines, and long-running agent runtimes.

MoiraWeave is the control and deployment plane. Hermes, OpenClaw, LangGraph, or
custom agents keep their own reasoning loop, tools, memory, and runtime-specific
behavior.

## Current Direction

### v0.3.x: Instant Local Onboarding
- `moira up` is the primary first-use path from an empty directory.
- `moira doctor` diagnoses workspace, Docker, ports, secrets, Compose, API, UI, and demo agent readiness.
- The no-secret demo agent is the canonical smoke test before Hermes/OpenClaw.
- Quickstart uses one route: start locally, chat, inspect runs/events/artifacts.

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
- Optional Kubernetes deployment controller for applying operations without
  giving the UI direct cluster credentials.

### v0.7: Product Usability
- Guided workload creation for Demo Agent, Hermes, OpenClaw, Generic HTTP Agent, External Agent, Model Service, and Pipeline.
- Agent Console links each message to run state, live events, cancel/retry, and artifacts.
- Operations Center explains `created`, `deployed`, `reachable`, and `healthy` with actionable remediation.
- Artifact Library supports workload/session/run/date/content-type navigation.
- Security console covers users, teams, memberships, API keys, and audit events.

### v0.8: Channels And Team Governance
- Production users and teams replace demo auth outside local/dev mode.
- API keys can be global or team-scoped.
- A signed inbound webhook connector lands before Telegram, Slack, and Discord.
- Runtime-owned channels remain supervised through `externalOwnedChannels`.
- Multi-environment views keep local, dev, staging, and production state separate.

## Recently Completed

- `moira up` local onboarding path with generated UI, API, worker, storage, workloads, deployment records, and persisted dev CLI auth.
- Optional local onboarding E2E: fresh workspace, `moira up`, demo-agent chat, run events, and artifacts.
- Public GHCR image smoke checks for API gateway, worker, and UI.
- Worker dispatch preflight check that reports Redis consumer-group/consumer state.
- UI Agent Console run activity summary, history filters, cancel/retry, run links, and artifact links.
- UI workload template summaries for adapter, ports, secrets, persistence, and channel ownership.
- Multi-agent deploy tests for Compose and Helm with Hermes and OpenClaw service separation.
- Combined core pytest harness for API gateway, worker, and integration suites despite service-local `app` package names.
- Versioned Hermes/OpenClaw examples with consistent ports, health checks, persistence, workspaces, and optional live-runtime tests.
- Observability linkage tests for API, worker, workloads, UI, monitoring manifests, metrics, and network policies.
- C4 and sequence architecture docs for agent operations, channels, runtime ownership, cancellation, and artifacts.
- Artifact Library filters, previews, downloads, and cross-links back to runs and agent sessions.
- Security console for hashed API keys with create, list, rotate, revoke, role display, and audit events.
- Persistent users, teams, team memberships, team-scoped API keys, membership removal, and CLI/UI security administration.
- `DEMO_AUTH_ENABLED` keeps demo login local/dev only; staging and production Helm overlays disable it.
- Durable worker settings for heartbeat, stale detection, Redis pending reclaim,
  bounded retries, backoff, and dead-letter handling are wired through tests,
  Compose, and Helm.
- Operators can inspect and purge worker dead-letter dispatch entries through
  `/v1/runs/dead-letter` and `moira run dead-letter list|purge`.
- Worker exposes Prometheus counters for dead-letter, pending reclaim outcomes,
  scheduled retries, and stale-heartbeat lost runs.

## Backlog

- Formal migrations: move control-plane DDL from inline startup code to Alembic with a baseline matching the current schema.
- Durable worker hardening: richer retry classification, safe dead-letter
  replay, and dashboard/alert coverage for reclaim/retry/lost/dead-letter
  transitions.
- Production auth hardening: password rotation/reset, richer team lifecycle, scoped visibility, and first-admin bootstrap guidance.
- Kubernetes deployment execution: optional controller that consumes deployment operations and writes command/log/result events.
- Channel connectors: signed inbound webhook first, then Telegram, Slack/Discord, with runtime-owned channels remaining supervised.
- UI polish: user/team administration, deployment-controller state, live event streaming in run detail and agent chat, and clearer multi-env filters.
- E2E scenarios: mock pipeline, mock long-running agent, cancel, stale recovery, dead-letter, and optional kind controller smoke.
- Comparison docs against LangGraph/LangSmith, Dify, Temporal, and Ray Serve.
- Migration docs for users moving from legacy pipeline/job concepts.

## Versioning Policy

MoiraWeave follows Semantic Versioning. Breaking changes in public APIs,
`workload.yaml`, CLI commands, or Helm values must be documented in changelogs.
