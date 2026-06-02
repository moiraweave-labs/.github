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
- Channel connectors: UI/API first, then Telegram, Slack/Discord, and webhooks.

### v0.7: Product Usability
- Guided workload creation for Demo Agent, Hermes, OpenClaw, Generic HTTP Agent, External Agent, Model Service, and Pipeline.
- Agent Console links each message to run state, live events, cancel/retry, and artifacts.
- Operations Center explains `created`, `deployed`, `reachable`, and `healthy` with actionable remediation.
- Artifact Library supports workload/session/run/date/content-type navigation.

## Recently Completed

- `moira up` local onboarding path with generated UI, API, worker, storage, workloads, deployment records, and persisted dev CLI auth.
- Optional local onboarding E2E: fresh workspace, `moira up`, demo-agent chat, run events, and artifacts.
- Public GHCR image smoke checks for API gateway, worker, and UI.
- Worker dispatch preflight check that reports Redis consumer-group/consumer state.
- UI Agent Console run activity summary, history filters, cancel/retry, run links, and artifact links.
- UI workload template summaries for adapter, ports, secrets, persistence, and channel ownership.
- Multi-agent deploy tests for Compose and Helm with Hermes and OpenClaw service separation.
- Combined core pytest harness for API gateway, worker, and integration suites despite service-local `app` package names.

## Backlog

- Hermes/OpenClaw certification: versioned examples, ports, secrets, healthchecks, persistence, and optional live-runtime tests.
- Observability smoke tests: API, worker, workloads, UI, monitoring assets, and log/metric entrypoints.
- Security hardening: users, teams, API key rotation, RBAC, and audit trail.
- Channel connectors: Telegram, Slack/Discord, inbound webhooks, and external-owned channel supervision.
- Professional architecture diagrams: C4 context, containers, components, and key sequences.
- UI polish: workload wizard validation, run timeline refinements, live event streaming in chat, artifacts previews, and deployment health actions.
- E2E scenarios: mock model, mock pipeline, mock long-running agent, cancel, stale recovery.
- Comparison docs against LangGraph/LangSmith, Dify, Temporal, and Ray Serve.
- Migration docs for users moving from legacy pipeline/job concepts.

## Versioning Policy

MoiraWeave follows Semantic Versioning. Breaking changes in public APIs,
`workload.yaml`, CLI commands, or Helm values must be documented in changelogs.
