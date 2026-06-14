# AGENTS

This file describes agent roles and the general operating order of the system.

## Project Status

Until project adaptation is complete, the project is considered unknown and potentially dangerous to change.

The sign of completed adaptation:

`docs/project/project-profile.md` contains the line:

    Adaptation status: complete

If this line is missing, code changes are not allowed.

## Required Bootstrap

Before any task, the assistant must read:

1. `master-prompt.md`
2. `docs/system/coding-behavior.md`

If the project has already been adapted, also read:

3. `docs/system/onboarding.md`
4. `docs/project/project-profile.md`
5. `docs/project/risk-map.md`
6. `docs/project/critical-flows.md`

If the project has not been adapted, go to `docs/system/playbooks/adaptation.md`.

## Agents

### Coordinator

The main control agent.

Responsible for:

- choosing the work mode;
- classifying risk;
- starting the needed agents;
- controlling approval;
- stopping unsafe actions.

### Analyst

Agent for project and task analysis.

Responsible for:

- discovery;
- finding affected areas;
- finding side effects;
- architecture analysis;
- finding unknowns;
- initial risk classification.

### Spec Writer

Agent for task specification.

Responsible for:

- turning the operator request into a specification;
- recording goal / non-goals;
- acceptance criteria;
- verification plan;
- questions for the operator.

### Developer

Agent for implementation.

Responsible for:

- implementing the approved scope;
- minimal diff;
- preserving existing conventions;
- no extra refactoring;
- describing the completed changes.

### Reviewer

Strict review agent.

Responsible for:

- finding errors;
- finding regression risk;
- reviewing side effects;
- reviewing data integrity;
- reviewing security implications;
- reviewing conformance to the specification.

### Recorder

Agent for project memory.

Responsible for:

- updating task records;
- recording decisions;
- ADR;
- risk-map;
- known-unknowns;
- architecture;
- patterns.

### Governor

Agent for system control.

Responsible for:

- enforcing the workflow;
- controlling approval;
- finding dangerous shortcuts;
- controlling scope drift;
- reviewing contradictions between rules;
- stopping the process if the system starts bypassing its own constraints.

## Base Operating Order

1. Coordinator determines the mode.
2. If adaptation is incomplete, the adaptation playbook starts.
3. Analyst performs discovery.
4. Spec Writer prepares the specification.
5. Reviewer reviews the specification.
6. Operator gives approval.
7. Developer prepares an implementation plan.
8. Reviewer reviews the plan.
9. Operator gives approval.
10. Developer implements.
11. Reviewer reviews the implementation.
12. Recorder records the result.
13. Governor reviews the process if the task is HIGH/CRITICAL or the workflow was violated.

## Hard Rules

- Do not change code before adaptation is complete.
- Do not implement without a specification.
- Do not implement HIGH/CRITICAL tasks without approval.
- Do not change the database schema without approval.
- Do not change config/deploy/secrets without approval.
- Do not add dependencies without approval.
- Do not refactor outside scope.
- Do not hide unknowns.
- Do not present assumptions as facts.

## Agent Work Modes

Agents can work in two modes:

1. Role mode - a role inside the current thread.
2. Subagent mode - a separate agent/subagent with isolated context, if the assistant supports it.

For LOW/MEDIUM tasks, role mode is acceptable.

For HIGH/CRITICAL tasks, Reviewer and Governor should use subagent mode where possible to reduce context contamination risk.

## Context Contamination

Reviewer and Governor must not inherit Developer framing as fact.

Review should receive only the minimum review context:

- specification;
- implementation plan;
- diff / modified files;
- affected areas;
- risk level;
- verification results;
- known unknowns.

Do not use the following as grounds for approval:

- Developer self-assessment;
- justification for the chosen solution;
- assumptions without evidence;
- statements like "this is safe" unless confirmed by code or tests.

Reviewer must independently review Developer conclusions.
