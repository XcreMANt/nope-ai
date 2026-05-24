# Playbook: Risk Levels

Risk is defined by the cost of failure, not by diff size.

A small change in a critical flow can be CRITICAL. A large documentation change can be LOW.

## LOW

Low risk.

Signals:

- does not affect business logic;
- does not change data;
- does not change external behavior;
- does not touch critical flows;
- easy to roll back;
- has a clear verification path.

Examples:

- documentation;
- comments;
- local UI text;
- isolated styles;
- tests without production code changes;
- safe typo fixes.

Approval is usually not needed if adaptation is complete.

## MEDIUM

Medium risk.

Signals:

- changes local business logic;
- affects a limited scenario;
- touches one module;
- does not touch critical flows;
- does not change the database schema;
- does not change security/integrations/deploy;
- has a clear verification path.

Examples:

- small feature inside one module;
- local input rules;
- isolated API response;
- local refactoring with tests;
- bugfix without impact on critical scenarios.

Approval is needed if there are unknowns.

## HIGH

High risk.

Signals:

- affects a user-facing flow;
- affects data writes;
- affects queues/jobs/schedulers;
- affects external integrations;
- affects cache;
- affects permissions;
- touches several modules;
- may cause regression;
- rollback is non-trivial.

Examples:

- changing an API contract;
- changing entity statuses/states;
- changing save logic;
- changing notification sending;
- changing background jobs;
- changing integration with an external service;
- changing cache invalidation;
- changing business rules.

Approval is required.

## CRITICAL

Critical risk.

Signals:

- possible money loss;
- possible data loss;
- possible data leak;
- possible production outage;
- possible legal/compliance consequences;
- auth/security is touched;
- payments/financial logic is touched;
- production deploy is touched;
- irreversible state transitions are touched;
- a critical flow is touched.

Examples:

- auth/session/token logic;
- permissions;
- personal or sensitive data;
- payments;
- production migrations;
- destructive operations;
- deploy/CI/CD changes;
- bulk data updates;
- irreversible status transitions;
- critical integrations.

Approval is required.

Required:

- specification;
- strict review;
- rollback plan;
- verification plan;
- recorded decision.

## UNKNOWN

If risk cannot be determined, treat it as HIGH.

If it is unknown whether a flow is critical, treat it as HIGH until clarified.

If data loss/security/payment consequences are possible, treat it as CRITICAL until clarified.

## Escalation Rule

Escalate risk if the task touches:

- database;
- auth/security;
- external integrations;
- queues/jobs/schedulers;
- config/deploy/secrets;
- cache;
- critical flows;
- sensitive data;
- state transitions;
- bulk operations;
- legacy code without tests.

## De-escalation Rule

Risk may be lowered only if there is evidence that:

- the affected area is isolated;
- data does not change;
- critical flows are not touched;
- tests exist;
- rollback is simple;
- behavior was verified.
