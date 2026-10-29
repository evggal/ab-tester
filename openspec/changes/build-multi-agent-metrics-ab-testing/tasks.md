# Tasks

## 1. Platform foundation

- [ ] 1.1 Create the FastAPI, React/TypeScript, worker, and shared-contract project structure; verify each service starts with its local development command.
- [ ] 1.2 Provision PostgreSQL roles, migration tooling, local/test configuration, and secret injection; verify migrations apply on an empty database without secrets in version control.
- [ ] 1.3 Create migrations for experiments, variants, assignments, events, metric definitions, aggregates, analysis snapshots, audits, agent work, and token usage; verify migration rollback or backward-compatible deployment behavior.

## 2. Experiment and event services

- [ ] 2.1 Implement authorized experiment lifecycle and configuration validation APIs; verify invalid allocations and unpublished metrics are rejected by API tests.
- [ ] 2.2 Implement deterministic assignment with persisted assignment versions; verify repeated requests for the same subject return the same variant.
- [ ] 2.3 Implement idempotent product-event and exposure ingestion with schema validation; verify duplicate idempotency keys do not change stored-event or metric counts.
- [ ] 2.4 Implement experiment and event authorization and audit entries; verify unauthorized mutation is denied and authorized mutations create safe audit records.

## 3. Metric definitions and analysis

- [ ] 3.1 Implement versioned metric-definition creation, validation, publication, and recalculation requests; verify prior calculation records retain their original metric version.
- [ ] 3.2 Implement asynchronous aggregation for count, sum, unique-count, and ratio metrics; verify fixture-based unit tests cover numerator, denominator, filters, and time windows.
- [ ] 3.3 Implement experiment result snapshots with uplift, confidence interval, significance result, and quality warnings; verify incomplete data, missing exposures, and allocation imbalance produce warnings.
- [ ] 3.4 Document metric configuration and calculation semantics in the application documentation; verify examples match the implemented request and response contracts.

## 4. OpenSpec agent telemetry

- [ ] 4.1 Implement notification ingestion against `agent-communication.json`, including correlation IDs and redaction; verify malformed notifications and secret-bearing fields are rejected or redacted.
- [ ] 4.2 Implement agent-work and token-usage persistence, preserving provider-reported versus estimated usage; verify dashboards can distinguish estimated values in integration tests.
- [ ] 4.3 Implement agent-telemetry authorization and audit coverage; verify only permitted service identities can submit telemetry.

## 5. Frontend and DataLens reporting

- [ ] 5.1 Implement experiment, variant, and metric-definition management screens; verify users can create a valid two-variant experiment and see validation errors for invalid input.
- [ ] 5.2 Implement task and notification history views with linked status and evidence; verify data shown matches stored OpenSpec notification records.
- [ ] 5.3 Create indexed, read-only reporting views for experiments, metrics, data quality, agent workflow, and token consumption; verify the DataLens identity has SELECT-only access to approved views.
- [ ] 5.4 Configure DataLens dashboards and filters for experiment, variant, metric version, date range, task, agent, and model; verify sensitive columns are unavailable in every dataset.

## 6. Integration, operations, and acceptance

- [ ] 6.1 Configure worker scheduling, health checks, monitoring, backups, retention, and dead-letter handling; verify a failed aggregation or notification can be observed and retried safely.
- [ ] 6.2 Perform code review against architecture, security, contracts, tests, and documentation; verify every blocking finding is resolved or tracked through the Lid remediation flow.
- [ ] 6.3 Execute end-to-end system tests for experiment setup, assignment, event ingestion, aggregation, DataLens filtering, telemetry, notification failure, and access denial; verify results are recorded for compliance review.
- [ ] 6.4 Run compliance assessment against all OpenSpec requirements and quality criteria; verify approval is recorded or correction findings are routed according to `agent-communication.json`.

## Workflow follow-up

- Archive the change after implementation, review, testing, and compliance approval are complete.
- Verify the archived change and synchronized specifications.
