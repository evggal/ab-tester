# Spec Delta

## Purpose

Capture OpenSpec agent notifications, work outcomes, and token consumption as verifiable delivery telemetry.

## ADDED Requirements

### Requirement: OpenSpec notification tracking
The system SHALL validate and store agent notifications that follow the repository communication contract and correlate them with task, cycle, sender, outcome, and evidence.

#### Scenario: Invalid notification is rejected
- **WHEN** a notification omits a required communication-contract field or has an invalid cycle
- **THEN** the system rejects it and reports the validation error without storing a partial notification

### Requirement: Agent-work recording
The system SHALL record each agent task with its task ID, remediation cycle, agent ID, model, start and end time, status, and linked notification.

#### Scenario: Agent completes work
- **WHEN** an agent returns a complete structured handoff
- **THEN** the system records the associated agent-work outcome and links its evidence

### Requirement: Token-consumption accounting
The system SHALL record prompt, completion, cached, and total token consumption per agent-work record when available and mark calculated values as estimated.

#### Scenario: Provider omits usage values
- **WHEN** a model provider does not return token usage and the system calculates an approximation
- **THEN** the stored usage record is marked estimated
