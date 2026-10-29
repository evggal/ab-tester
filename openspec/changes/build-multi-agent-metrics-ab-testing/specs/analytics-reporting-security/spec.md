# Spec Delta

## Purpose

Expose safe, filterable analytics in DataLens while protecting sensitive data and configuration integrity.

## ADDED Requirements

### Requirement: DataLens reporting datasets
The system SHALL publish read models for experiment summaries, variant comparison, metric trends, data quality, agent workflow, and token consumption.

#### Scenario: Analyst filters a dashboard
- **WHEN** an authorized analyst filters a DataLens dataset by experiment, variant, metric version, date range, task, agent, or model
- **THEN** the dataset returns only the matching reporting rows

### Requirement: Read-only reporting access
The system SHALL grant DataLens a database identity with read-only access limited to approved reporting views.

#### Scenario: Reporting identity attempts a write
- **WHEN** the DataLens database identity attempts to modify operational or reporting data
- **THEN** the database denies the operation

### Requirement: Restricted development analytics
The system SHALL restrict agent-work, review, compliance, and token-consumption dashboards to Lid, administrators, and explicitly authorized project members.

#### Scenario: Product user requests development analytics
- **WHEN** a user without development-analytics access requests an internal dashboard or dataset
- **THEN** the system denies access without exposing internal metrics

### Requirement: Sensitive-data protection and auditability
The system SHALL redact secrets, credentials, authorization headers, private prompts, personal identifiers, and unredacted sensitive payloads before persistence or reporting, and SHALL audit configuration changes.

#### Scenario: Sensitive event property is submitted
- **WHEN** an event or notification contains a configured sensitive value
- **THEN** the system stores and reports only its redacted representation

#### Scenario: Experiment configuration changes
- **WHEN** an authorized actor changes an experiment or metric definition
- **THEN** the system writes an audit entry with actor, action, target, timestamp, and safe before/after metadata
