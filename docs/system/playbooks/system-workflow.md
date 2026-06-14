# Playbook: System Workflow

Describes how the whole multi-agent system works.

## Main Idea

The system does not work as a set of independent agents, but as a controlled pipeline.

Do not skip stages for speed.

Initial operator goals are inputs to the workflow, not approval to implement.

Clarifications, corrections, additional requirements, answers to questions, and restatements of the final goal are not approval.

Requests to modify NOPE itself are NOPE self-modification. The assistant must warn the operator, use the gated workflow, and include Governor review as defined in `master-prompt.md`.

Specification and implementation planning stages are bundled for MEDIUM, HIGH, CRITICAL, unclear, multi-module, database, external integration, config, deploy, security, or critical-flow tasks.

A stage artifact is not complete until its required review is complete and recorded.

## Base Chain

1. Coordinator determines the mode.
2. Analyst performs discovery.
3. Spec Writer writes the specification.
4. Reviewer reviews the specification.
5. Recorder records the reviewed specification.
6. Operator gives approval.
7. Developer prepares the implementation plan.
8. Reviewer reviews the plan.
9. Recorder records the reviewed plan.
10. Operator gives approval.
11. Developer implements.
12. Reviewer reviews the implementation.
13. Recorder records the result.
14. Governor may review process correctness.

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
- treating the initial implementation goal as permission to code;
- treating requirement clarifications as approval;
- treating specification approval as implementation approval;
- treating a raw specification draft as a completed specification stage;
- treating a raw implementation plan draft as a completed planning stage;
- implement without a specification;
- implement without approval;
- direct NOPE self-modification from conversational instructions;
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
5. run Governor review if the violation involved NOPE self-modification;
6. continue only after the cause is fixed.
