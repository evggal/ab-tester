# Spec Delta

## Purpose

Collect trusted product events and produce versioned, reproducible metrics and A/B analysis results.

## ADDED Requirements

### Requirement: Idempotent event collection
The system SHALL accept timestamped product events with an event name, anonymized subject key, idempotency key, and optional experiment, variant, and validated properties.

#### Scenario: Duplicate event submission
- **WHEN** an event is submitted again with an existing idempotency key
- **THEN** the system does not create a second raw event or change calculated metrics

### Requirement: Versioned metric definitions
The system SHALL publish validated metric definitions without application redeployment and retain the definition version used by every historical calculation.

#### Scenario: Metric definition is changed
- **WHEN** an authorized analyst publishes a changed metric definition
- **THEN** the system creates a new version and preserves earlier calculation results with their original version

### Requirement: Reproducible experiment analysis
The system SHALL calculate variant-level participant and exposure counts, primary and guardrail metric values, and analysis snapshots for a selected experiment and period.

#### Scenario: Ratio metric analysis completes
- **WHEN** an aggregation run processes a valid ratio metric
- **THEN** its result includes the estimate, absolute difference, relative uplift, confidence interval, statistical-significance result, and metric-definition version

### Requirement: Analysis data-quality warnings
The system SHALL identify insufficient sample size, missing exposures, unbalanced allocation, duplicate events, and incomplete analysis windows in experiment results.

#### Scenario: Incomplete analysis window
- **WHEN** a requested analysis period overlaps data that has not completed processing
- **THEN** the result includes an incomplete-window warning
