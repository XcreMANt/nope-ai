# Playbook: Critical Flow

Used for tasks that touch critical scenarios.

## Critical flow

Critical flow is a scenario where a mistake may lead to:

- data loss;
- money loss;
- data leak;
- security failure;
- production outage;
- legal consequences;
- irreversible state change.

## Requirements

For a critical flow, the following are required:

- specification;
- strict review;
- approval;
- rollback plan;
- verification plan;
- recorded decision;
- no scope drift.

## Before Implementation, Review

- Current flow.
- All side effects.
- Database writes.
- External integrations.
- Queues/jobs/schedulers.
- Permissions.
- Error handling.
- Retry/idempotency.
- Rollback.

## Forbidden

- Do not change a critical flow without approval.
- Do not make a "quick fix" without impact analysis.
- Do not change several critical flows in one task.
- Do not do refactoring together with a functional change.
