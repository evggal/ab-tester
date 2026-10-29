# Spec Delta

## Purpose

Manage A/B experiment lifecycles and provide stable, auditable participant variant assignments.

## ADDED Requirements

### Requirement: Experiment lifecycle configuration
The system SHALL create, edit, start, pause, stop, and archive experiments with a unique key, hypothesis, owner, target population, schedule, primary metric, guardrail metrics, variants, and allocation weights.

#### Scenario: Invalid allocation is rejected
- **WHEN** an analyst attempts to publish an experiment whose variant weights do not total 100%
- **THEN** the system rejects the configuration and identifies the invalid allocation

#### Scenario: Unpublished metric is selected
- **WHEN** an analyst selects a metric definition that is not published
- **THEN** the system rejects the experiment configuration

### Requirement: Deterministic variant assignment
The system SHALL assign an active experiment participant to a variant deterministically from the experiment identifier and anonymized subject key for the life of that experiment configuration.

#### Scenario: Repeated assignment request
- **WHEN** the same anonymized subject requests assignment for an active experiment more than once
- **THEN** the system returns the same variant and assignment version

### Requirement: Exposure eligibility
The system SHALL record an exposure before a participant is included in experiment analysis.

#### Scenario: Conversion without exposure
- **WHEN** an event is received for a participant without a recorded experiment exposure
- **THEN** the system excludes that participant from exposure-based experiment analysis and records a data-quality warning

### Requirement: Active experiment change control
The system SHALL version experiment configuration and permit only operational updates while an experiment is active. Changes to variants, allocation, audience, randomization unit, exposure event, primary metric, alpha, or statistical method SHALL require cloning a new experiment.

#### Scenario: Protected active configuration is changed
- **WHEN** an analyst attempts to change a protected field on an active experiment
- **THEN** the system rejects the direct change and offers a clone with a new experiment identifier

### Requirement: Restart-safe experiment state
The system SHALL restore active experiment configuration, participant assignments, and processing checkpoints after service or worker reload.

#### Scenario: Assignment after reload
- **WHEN** the assignment service reloads and a previously assigned participant requests an active experiment
- **THEN** the system returns the persisted variant and assignment version
