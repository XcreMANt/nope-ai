# Playbook: System Workflow

Describes how the whole multi-agent system works.

## Main Idea

The system does not work as a set of independent agents, but as a controlled pipeline.

Do not skip stages for speed.

## Base Chain

1. Coordinator determines the mode.
2. Analyst performs discovery.
3. Spec Writer writes the specification.
4. Reviewer reviews the specification.
5. Operator gives approval.
6. Developer prepares the implementation plan.
7. Reviewer reviews the plan.
8. Operator gives approval.
9. Developer implements.
10. Reviewer reviews the implementation.
11. Recorder records the result.
12. Governor may review process correctness.

## Who Can Stop the Workflow

The process can be stopped by:

- Coordinator;
- Reviewer;
- Governor;
- Operator.

Stop reasons:

- unknown risk level;
- incomplete specification;
- missing approval;
- scope drift;
- critical flow without analysis;
- no verification plan;
- dangerous shortcut;
- conflicting requirements;
- risk of data loss/security/production outage.

## Escalation

Risk is escalated if the task touches:

- critical flow;
- database;
- auth/security;
- external integrations;
- config/deploy/secrets;
- queues/jobs/schedulers;
- payments/financial logic;
- sensitive data;
- irreversible state transitions;
- legacy zone without tests.

## Shortcut Ban

Forbidden:

- "just fix the code" without discovery;
- implement without a specification;
- implement without approval;
- do refactoring together with a feature;
- change architecture without an ADR;
- hide assumptions;
- ignore unknowns;
- treat missing tests as normal.

## Recovery

If the workflow is violated:

1. stop;
2. record the violation;
3. identify the last correct stage;
4. return to it;
5. continue only after the cause is fixed.
