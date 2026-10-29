# Proposal

## Why

The project needs a traceable foundation for collecting product and agent-development metrics, running A/B tests, and presenting trusted results in DataLens. Product decisions, model token consumption, and multi-agent delivery evidence must be auditable without exposing sensitive data.

## What Changes

- Add experiment configuration, deterministic variant assignment, exposure tracking, and idempotent product-event ingestion.
- Add versioned, configurable metric definitions and asynchronous A/B aggregation with reproducible result snapshots.
- Add OpenSpec-notification ingestion, agent-work tracking, and provider-reported or estimated token-usage accounting.
- Add DataLens-safe reporting views, data-quality warnings, and access controls, auditing, and redaction.
- Establish the FastAPI, React/TypeScript, PostgreSQL, worker, and DataLens architecture for the initial release.

## Capabilities

### New Capabilities

- `experiment-management`: Configures experiments and produces stable participant-to-variant assignments.
- `metric-collection`: Ingests immutable product events and calculates versioned, configurable metrics and A/B results.
- `agent-telemetry`: Captures OpenSpec notifications, agent work, and token-consumption evidence.
- `analytics-reporting-security`: Publishes safe DataLens reporting views and enforces access, auditing, and sensitive-data protection.

### Modified Capabilities

None.

## Impact

- New React/TypeScript UI for experiment and metric configuration.
- New FastAPI APIs for experiment management, assignment, event ingestion, OpenSpec notifications, and reporting.
- New PostgreSQL schema, aggregation worker, DataLens read-only reporting views, and operational configuration.
- Integration with the existing `agent-communication.json` contract and configured Lid/subagent workflow.
