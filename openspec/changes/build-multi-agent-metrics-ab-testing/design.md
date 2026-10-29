# Design

## Context

This greenfield repository contains the Lid/subagent communication contract and planning documents but no application code. See `proposal.md` for the product motivation and the capability deltas for externally observable behavior.

## Goals / Non-Goals

**Goals:**
- Deliver a modular FastAPI, React/TypeScript, PostgreSQL, worker, and DataLens solution.
- Keep experiments, metric definitions, events, analysis runs, and agent telemetry traceable.
- Make configuration changes safe, auditable, and usable without application redeployment.

**Non-Goals:**
- Replace DataLens with a custom visualization product.
- Store direct personal identifiers, secrets, or unredacted private prompts.
- Introduce a separate analytical database before PostgreSQL capacity data demonstrates the need.

## Decisions

### PostgreSQL is the initial system of record
PostgreSQL holds transactional configuration, immutable raw events, calculated aggregates, analysis snapshots, agent work, token usage, and audit records. Event tables will be partitioned and reporting views indexed for expected dashboard filters. This minimizes operational complexity while the product is new; an analytical store remains a future scaling option.

### FastAPI separates synchronous APIs from asynchronous calculations
The API handles authorization, validation, experiment assignment, and idempotent ingestion. A worker validates queued work, aggregates metrics, computes A/B results, refreshes reporting views, and raises data-quality warnings. This keeps ingestion and assignment latency independent of analysis cost.

### Stable assignments use a persisted deterministic result
The assignment service derives a candidate from the experiment ID and anonymized subject key, then persists the selected variant and configuration version. Persistence preserves historical reproducibility if allocation changes or an experiment is restarted.

### OpenSpec notifications use the repository envelope
The notification adapter validates the required fields and allowed values in `agent-communication.json`, redacts sensitive evidence, and records a correlation ID with agent-work and token-usage records. This preserves the existing Lid workflow rather than creating a competing protocol.

### DataLens reads reporting views only
DataLens uses a dedicated read-only database identity and approved views. Views expose no raw secrets, direct identifiers, prompts, or mutable operational tables. This favors a small, enforceable permission boundary over direct access to all analytics tables.

## Risks / Trade-offs

- [PostgreSQL reporting becomes slow at high event volume] → Partition events, pre-aggregate metrics, benchmark dashboard queries, and migrate read models to an analytical store only when measured limits are exceeded.
- [Metric definitions become overly expressive or unsafe] → Allow only validated fields, aggregation types, and filters; version and audit publication.
- [Token usage differs by model provider] → Store provider-reported fields separately from estimated values and label estimates in every reporting view.
- [Sensitive content reaches event or notification payloads] → Apply schema limits and redaction at ingestion, restrict DataLens to safe views, and test redaction paths.

## Migration Plan

1. Provision databases, roles, secret injection, and backups.
2. Apply schema migrations and deploy APIs, worker, and reporting views.
3. Verify a small internal experiment, event flow, agent notification, and token-usage record.
4. Connect DataLens with the reporting identity and validate dashboard filters.
5. Roll back application releases to the prior version; retain immutable events and analysis snapshots. Roll back database changes with reviewed backward-compatible migrations or a specific migration rollback.
