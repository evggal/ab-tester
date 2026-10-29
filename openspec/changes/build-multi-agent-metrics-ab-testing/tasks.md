# Tasks

## 1. Project boundaries and platform foundation

- [ ] 1.1 Create owned directories for database, migrations, backend API, backend services, frontend app, frontend design system, infrastructure, system tests, and documentation; verify no development ownership areas overlap.
- [ ] 1.2 Create FastAPI, React/TypeScript, worker, and shared contract foundations; verify each service starts with its local development command.
- [ ] 1.3 Configure local, test, and production environment variables and secret injection; verify no credential is committed to version control.
- [ ] 1.4 Provision PostgreSQL roles for migration, runtime, worker, DataLens read-only access, and auditing; verify every role has only required permissions.

## 2. Database foundation and security

- [ ] 2.1 Configure SQLAlchemy and Alembic migrations; verify migrations apply to an empty database and have a reviewed rollback or backward-compatible strategy.
- [ ] 2.2 Create core roles, user-role mapping, and immutable audit-log migrations; verify every configuration mutation creates a safe audit record.
- [ ] 2.3 Create experiment, version, variant, assignment, and exposure migrations with lifecycle and allocation constraints; verify allocation validation and assignment uniqueness.
- [ ] 2.4 Create immutable event and rejection-record migrations with idempotency constraints and reporting indexes; verify duplicate submissions cannot create duplicate events.
- [ ] 2.5 Create metric-definition, metric-version, aggregation-run, aggregate, analysis-snapshot, and data-quality migrations; verify historical results retain their metric version.
- [ ] 2.6 Create OpenSpec notification, agent-work, and token-usage migrations; verify estimated usage is distinguishable from provider-reported usage.
- [ ] 2.7 Create safe reporting views and the DataLens read-only role; verify it cannot query raw sensitive tables or write to any table or view.

## 3. Backend API and authorization

- [ ] 3.1 Implement FastAPI configuration, health/readiness endpoints, correlation IDs, error responses, and OpenAPI generation; verify health checks and API schema in automated tests.
- [ ] 3.2 Implement authentication, role-based authorization, and audit dependencies; verify unauthorized requests return 401/403 and authorized mutations are audited.
- [ ] 3.3 Implement experiment lifecycle APIs with draft/active/paused/completed/archived transitions; verify invalid transitions, invalid allocation, and unpublished metric references are rejected.
- [ ] 3.4 Implement clone-based protected-change flow for active experiments; verify direct changes to variants, allocation, audience, randomization, primary metric, alpha, or statistical method are rejected.
- [ ] 3.5 Implement assignment and exposure APIs with idempotency; verify repeated assignment remains stable after service restart.
- [ ] 3.6 Implement product-event ingestion and safe rejection responses; verify property validation, redaction, delayed events, and duplicate idempotency behavior.
- [ ] 3.7 Implement metric-definition, publication, recalculation, and result APIs; verify versioned definitions and zero-denominator results return `null` with quality flags.
- [ ] 3.8 Implement OpenSpec notification, agent-work, and token-usage APIs; verify envelopes conform to `agent-communication.json` and service access is restricted.

## 4. Backend services and asynchronous analysis

- [ ] 4.1 Implement repository and transaction services for experiments, events, metrics, telemetry, and audits; verify concurrent mutation and rollback behavior.
- [ ] 4.2 Implement deterministic persisted assignment using experiment ID, configuration version, and anonymized subject key; verify distribution matches configured allocation with fixture populations.
- [ ] 4.3 Implement idempotent event normalization and asynchronous processing; verify retries do not duplicate stored events or aggregates.
- [ ] 4.4 Implement validated versioned metric definitions for count, unique-count, sum, and ratio metrics; verify incompatible filters and numerator/denominator rules fail validation.
- [ ] 4.5 Implement aggregation jobs, checkpoints, calculation runs, and dead-letter handling; verify raw events remain immutable and failed jobs retry safely.
- [ ] 4.6 Implement ratio/conversion comparison with two-sided alpha 0.05, 95% confidence interval, uplift, and data-quality warnings; verify known statistical fixtures and insufficient-data cases.
- [ ] 4.7 Implement reporting-view refresh and operational telemetry; verify aggregation delay, worker failures, and database dependency health are observable.

## 5. Frontend product experience

- [ ] 5.1 Implement authenticated shell, role-aware navigation, shared form/table/status components, and accessible error states; verify route access and keyboard navigation.
- [ ] 5.2 Implement experiment list, create/edit form, lifecycle controls, and clone flow; verify active protected fields cannot be edited directly.
- [ ] 5.3 Implement metric-definition list, editor, validation, publishing, and version display; verify ratio configuration and publication confirmation behavior.
- [ ] 5.4 Implement experiment result screens with variant counts, uplift, confidence interval, p-value, and quality warnings; verify zero-denominator values display as insufficient data, not zero.
- [ ] 5.5 Implement internal assignment-test screen for authorized users; verify repeated requests show the persisted assignment version.

## 6. Frontend UX and DataLens integration

- [ ] 6.1 Implement the design system, responsive layouts, visual status mapping, and accessibility coverage; verify desktop/tablet behavior and semantic controls.
- [ ] 6.2 Implement secure experiment, metric, and data-quality DataLens dashboard directory/integration; verify permitted filters and unavailable/unauthorized states.
- [ ] 6.3 Implement restricted development analytics pages for task workflow, OpenSpec notifications, token usage, reviews, tests, and compliance; verify ordinary product users cannot access internal routes or datasets.
- [ ] 6.4 Implement token-consumption filtering by agent, model, task, complexity, cycle, and date; verify estimated usage is visibly labelled.

## 7. Agent coordination and access control

- [ ] 7.1 Enforce scoped assignment and result packets through Lid; verify a specialist receives only its task objective, own paths, required contracts, acceptance criteria, and required evidence.
- [ ] 7.2 Enforce OpenCode read, discovery, edit, and shell restrictions for every specialist; verify an agent cannot access another ownership area or delegate directly.
- [ ] 7.3 Create read-only review-bundle generation for code review; verify the reviewer receives only approved changed artifacts, contracts, requirements, and test evidence.
- [ ] 7.4 Verify requirements, architecture, testing, compliance, and technical-writing agents receive only their stated artifacts and no unrelated work history.

## 8. Integration, operations, and acceptance

- [ ] 8.1 Configure worker scheduling, health checks, monitoring, backups, retention, and dead-letter operations; verify an ingestion or aggregation failure can be observed and retried safely.
- [ ] 8.2 Perform code review using the scoped review bundle; verify every blocking finding is resolved or routed through the Lid remediation flow.
- [ ] 8.3 Execute end-to-end system tests for experiment setup, assignment, ingestion, analysis, DataLens filters, token telemetry, notification failure, access denial, and service reload; verify evidence is recorded for compliance review.
- [ ] 8.4 Run compliance assessment against all OpenSpec requirements and quality criteria; verify approval is recorded or correction findings are classified and routed within the five-cycle limit.

## Workflow follow-up

- Archive the change after implementation, review, testing, and compliance approval are complete.
- Verify the archived change and synchronized specifications.
