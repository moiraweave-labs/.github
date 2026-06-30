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
- Security console supports user/team edits and Playwright covers the main
  identity administration path.

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
- Release Please calls the reusable/manual Python package publish workflow;
  PyPI publishing is opt-in through `PYPI_PUBLISH_ENABLED=true`, and the
  fallback build-and-skip path has been validated on a real release.
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
- Operators can inspect, replay, and purge worker dead-letter dispatch entries
  through `/v1/runs/dead-letter` and
  `moira run dead-letter list|replay|purge`.
- Worker exposes Prometheus counters for dead-letter, pending reclaim outcomes,
  scheduled retries, and stale-heartbeat lost runs.
- Safe dead-letter replay is available through
  `/v1/runs/dead-letter/{message_id}/replay` and
  `moira run dead-letter replay`.
- Signed inbound webhooks provide the first v1 external channel connector while
  Telegram, Slack, and Discord remain post-webhook work.
- Deployment operations use explicit state-machine validation, controller claim,
  heartbeat, lease expiry, reclaim events, stdout/stderr summaries, and a CLI
  controller heartbeat loop while Kubernetes commands run.
- Persistent auth now includes first-admin bootstrap, password change/reset,
  user update/disable/enable, team update/member lifecycle, team-scoped API
  keys, and team-aware visibility for runs, sessions, deployments, operations,
  artifacts, and audit events.
- Login attempts, secret inventory reads, user/team/API-key changes,
  dead-letter replay/purge, artifact access, and deployment controller actions
  are audited.
- Alembic is the runtime-facing Postgres schema owner, with legacy baseline SQL
  isolated for migration compatibility checks.
- Real Postgres migration tests cover empty database, existing baseline,
  idempotent upgrades, and critical tables/indexes.
- Worker retry classification separates transient adapter/runtime failures from
  non-retryable manifest, auth, payload, and missing-workload failures.
- Operations Center alerts cover retry/reclaim pressure, stale/lost runs,
  dead-letter backlog, expired controller leases, and duplicate dispatch
  acknowledgements.
- Optional kind controller smoke tests cover apply, logs, undeploy, expired
  lease reclaim, and abandoned operation recovery.
- Sensitive endpoint rate-limit tests cover login, API key creation, webhook
  ingress, dead-letter replay, and deployment controller claim paths.
- Cross-team visibility regression covers runs, sessions, artifacts,
  deployments, deployment operations, and audit events.
- UI Playwright coverage asserts operation execution labels for guidance-only,
  control-plane, and controller-executed deployment operations.
- Operations Center lists, replays, and purges dead-letter dispatch messages
  through the API gateway; Playwright covers replay.
- Runs, Artifact Library, and audit events support deployment-environment
  filters, and Operations shared URLs preserve the selected environment.
- Workloads are shared by default or can persistently scope to a team through
  `moiraweave.io/team-id`; the API and Create Workload wizard enforce and expose
  that boundary.
- Staging/prod Helm overlays now have an auth contract: demo login is disabled,
  while bootstrap, persistent-user login, and persistent API keys keep working.
- Run Detail opens the recent event tail and resumes SSE with `Last-Event-ID`;
  cursor reads avoid polling an entire long-running timeline.
- Agent Console pages sessions and history, including deep links to sessions
  beyond the first page and a Playwright "load earlier" regression flow.
- Artifact Library now retrieves bounded pages while retaining its existing
  workload/session/run/date/type filters and artifact-to-run links.
- Runs, deployment operations, and audit events now retrieve bounded pages from
  the dashboard with explicit older-page loading.
- Workloads, Runs, Artifact Library, and Agent Console now distinguish API
  errors from true empty states, with Playwright regressions for failed list
  paths.
- Run Detail now distinguishes run-status, event-timeline, and artifact load
  failures from true empty timeline/artifact states.
- Security now distinguishes user, team, team-member, and API-key load failures
  from true empty identity inventories.
- Operations Center now distinguishes environment, alert, deployment,
  operation, and audit load failures from true empty platform state.
- Local onboarding E2E now validates `moira up`, demo-agent chat, run listing,
  stored events, and produced artifacts.

## Backlog

- Production auth hardening: continued scope and rate-limit coverage for new
  sensitive endpoints.
- Durable control-plane polish: load-oriented API tests and dead-letter
  traceability regression checks as schemas evolve.
- Kubernetes deployment execution: wire optional kind/controller smoke into CI
  only when cluster credentials and execution budget are available.
- Release-gate product E2E maintenance as onboarding, chat, artifacts,
  Operations Center, Security, and failure recovery evolve.
- E2E scenarios: mock pipeline, mock long-running agent, cancel, stale
  recovery, dead-letter replay, and release-gate product flows.
- Comparison docs against LangGraph/LangSmith, Dify, Temporal, and Ray Serve.
- Migration docs for users moving from legacy pipeline/job concepts.

## Versioning Policy

MoiraWeave follows Semantic Versioning. Breaking changes in public APIs,
`workload.yaml`, CLI commands, or Helm values must be documented in changelogs.
