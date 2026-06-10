# MLAI Showcase: Project Review Guide

MLAI Showcase is a private demo project built to demonstrate QA automation, API and integration testing, systems reliability, and technical process automation. This public guide summarizes what reviewers can evaluate from the screenshots and what I can cover in a guided walkthrough.

The screenshots use synthetic local demo data only. They are intended to show the application surface, operator workflows, API contracts, Dockerized runtime, and automated verification evidence without exposing private repo contents, secrets, local paths, or raw test artifacts.

## What This Project Demonstrates

| Area | Reviewer takeaway | Evidence available in this public portfolio |
| --- | --- | --- |
| Multi-service application design | The project is more than a UI mockup. It includes a React UI, Nginx gateway, sync API, async API, workers, and supporting data/event services. | Dashboard, Operations workspace, Docker Compose service list |
| Gateway-routed integration | Browser and smoke-test traffic route through the gateway path, which helps catch rewrite, auth, and streaming issues that direct API calls can miss. | Docker services screenshot, Robot Framework smoke report |
| API contract validation | The sync API exposes OpenAPI/Swagger documentation for review, audit, threat, assessment, evaluation, and streaming endpoints. | Swagger/OpenAPI screenshot |
| Async workflow validation | Uploads return durable job identifiers, progress through lifecycle states, and produce result artifacts with confidence and review metadata. | Upload result artifact screenshot, API response validation screenshot |
| Automated QA coverage | Robot Framework smoke tests validate the gateway-routed stack and include positive and negative integration scenarios. | Robot Framework report, terminal smoke output |
| Systems reliability mindset | The runtime uses Docker Compose services, health checks, storage readiness indicators, metrics surfaces, and worker-oriented event paths. | Docker Compose service list, API health validation screenshot |
| Operator workflow depth | The UI includes candidate review, audit review/export, document upload, result inspection, and demo-data cleanup surfaces. | Operations workspace screenshots |
| Security-aware testing | The project includes role-aware auth concepts, protected operator routes, request traceability, and negative tests for unauthorized or forbidden access. | Walkthrough discussion and smoke-test scope |

## Public Screenshot Set

| Area | Preview |
| --- | --- |
| Analyst dashboard | ![React/OpenLayers analyst dashboard with live threat feed, critical-signal banner, map markers, and grounded assistant panel](./docs/screenshots/01-dashboard-threat-map.png) |
| Operations workspace: upload, review, audit | ![Operations workspace showing document upload, candidate review, and audit export controls](./docs/screenshots/02a-operations-upload-review-audit.png) |
| Operations workspace: audit and reset controls | ![Operations workspace showing candidate review, audit export, and demo-data reset controls](./docs/screenshots/02b-operations-review-audit-reset.png) |
| Async upload result | ![Async upload workflow with completed document extraction result artifact](./docs/screenshots/03-upload-result-artifact.png) |
| Robot smoke report | ![Robot Framework gateway smoke suite passing against the containerized stack](./docs/screenshots/04-robot-smoke-report.png) |
| Terminal smoke output | ![Local verification run showing the smoke suite completing successfully](./docs/screenshots/05-terminal-smoke-output.png) |
| Docker services | ![Local Docker Compose stack with UI, gateway, APIs, workers, and supporting services](./docs/screenshots/06-docker-compose-services.png) |
| Swagger contract | ![Swagger UI contract for sync API endpoints](./docs/screenshots/07-swagger-sync-api.png) |
| API health validation | ![Local API validation showing sync and async service health and storage readiness](./docs/screenshots/08-api-response-validation.png) |

## Guided Review Path

A guided walkthrough can be adjusted based on the reviewer. The goal is to move from visible application behavior to implementation and verification evidence.

### 1. Project and architecture overview

Review the system as a containerized multi-service prototype with a React dashboard, Nginx gateway, sync API, async API, background workers, Robot Framework smoke tests, and optional event-backed worker paths.

Key points:

- The domain is geospatial threat detection, but the hiring signal is the engineering pattern: API contracts, service boundaries, async state, workflow validation, traceability, and failure handling.
- Implemented behavior is separated from planned or provisioned capabilities.
- The project demonstrates both QA automation and systems-oriented troubleshooting.

### 2. UI and operator workflows

Review the dashboard and Operations workspace screenshots.

Evidence covered:

- Live threat feed and critical-signal banner
- Map markers and association drill-down behavior
- Grounded assistant panel
- Async document upload
- Review candidate inspection
- Audit review and CSV export
- Demo-data cleanup controls

Reviewer takeaway:

The UI is not only a static dashboard. It exposes analyst and operator workflows that connect to backend contracts and testable system behavior.

### 3. API contract and integration validation

Review the Swagger/OpenAPI screenshot and API health validation screenshot.

Evidence covered:

- Sync API endpoint groups for audit, review, threats, assessment, and evaluation workflows
- Health responses for sync and async APIs
- Storage readiness and service status fields
- Local gateway-routed API validation using safe localhost requests

Reviewer takeaway:

The API surface is documented and validated through repeatable local checks, not treated as an informal backend implementation detail.

### 4. Async workflow behavior

Review the upload result artifact and Operations workspace screenshots.

Evidence covered:

- Upload flow returns a durable job identifier
- Job status progresses through lifecycle states
- Completed jobs expose result artifacts
- Results include extraction strategy, confidence, review status, degradation indicators, and preview text
- Low-confidence or degraded extraction can be marked for review instead of being treated as automatically reliable

Reviewer takeaway:

The project treats async state, result readiness, and review handling as first-class test scenarios.

### 5. Dockerized runtime and service orchestration

Review the Docker Compose services screenshot.

Evidence covered:

- UI, gateway, sync API, async API, workers, and supporting services run as a local stack
- Service names and port mappings are visible for runtime troubleshooting
- The stack supports smoke-test and event-backed validation paths

Reviewer takeaway:

The project demonstrates practical runtime awareness, not just isolated code snippets.

### 6. Automated verification

Review the Robot Framework report and terminal smoke output.

Evidence covered:

- The current smoke suite shows 20 tests passing and 0 failing
- Smoke validation exercises gateway-routed sync and async behavior
- Test coverage includes health checks, Swagger availability, API contracts, file upload handling, result retrieval, SSE-related behavior, and negative cases

Reviewer takeaway:

The project includes repeatable integration evidence and does not rely only on manual UI inspection.

### 7. Negative and security-aware test coverage

During a guided walkthrough, I can review examples of negative and access-control validation.

Examples include:

- Unauthenticated protected routes returning 401
- Lower-role analyst access to operator routes returning 403
- Empty upload validation returning 400
- Unknown async job retrieval returning 404
- Not-ready result states returning structured non-success responses
- Storage fallback and fail-closed behavior covered in service tests

Reviewer takeaway:

The project validates failure modes and access boundaries, not only happy paths.

### 8. Event-backed worker path

During a deeper technical walkthrough, I can review the event-backed worker path and how it extends the local smoke-test model.

Areas covered:

- Async upload event publishing
- Worker consumption and processed-event publishing
- Remorse event publishing and inbox persistence
- Candidate promotion and execution materialization
- Retry, backoff, dead-letter topic configuration, and idempotency concepts

Reviewer takeaway:

This is not presented as a finished production event platform. It demonstrates the patterns I would expect to harden further: durable state, idempotency, poison-event handling, and worker observability.

## Review Options

For a short recruiter screen, I would focus on:

1. Dashboard and Operations screenshots
2. Swagger/OpenAPI contract screenshot
3. Robot Framework smoke report
4. Docker Compose services screenshot
5. Resume tie-in: QA automation, API testing, Docker, Robot Framework, and process automation

For a technical reviewer, I can go deeper into:

1. Sync threat workflow and API contracts
2. Async upload and job-result lifecycle
3. Gateway routing and SSE behavior
4. Robot Framework suite organization
5. Event-backed worker path
6. Negative testing and access-control validation
7. Known limitations and next hardening steps

## Known Limits and Next Improvements

This project is a portfolio prototype, not a production deployment. Current limitations are documented intentionally because they affect test strategy and production hardening priorities.

Current limits:

- Auth uses demo static-token and JWT configuration, not a full identity-provider integration.
- Assistant quality depends on local model configuration, while smoke tests use deterministic behavior where needed.
- Redis, MongoDB, and Milvus are provisioned or planned in parts of the stack, but they are not all active core runtime paths.
- OCR is functional but conservative, and noisy scans can remain provisional.
- Staging deployment is an opt-in scaffold, not an always-on public production environment.

Potential next improvements:

- Stronger identity-provider integration
- Deeper retrieval and ranking for assistant grounding
- Broader audit pagination and saved filters
- Centralized tracing and observability
- Additional OCR tuning with more realistic noisy-document samples
- Expanded CI visibility and public screenshot evidence

## Private Demo Review

The full MLAI Showcase source remains private so the review path can stay controlled and sanitized. Guided walkthroughs of selected project areas are available upon request.
