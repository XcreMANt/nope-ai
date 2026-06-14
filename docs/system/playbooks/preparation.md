# Playbook: Preparation

Used to prepare for a task without changing production code.

## Allowed

- analyze code;
- find affected areas;
- write a specification;
- write a plan;
- write a QA Plan;
- update NOPE root;
- prepare an ADR;
- form questions for the operator.

## Forbidden

- change application code;
- change configs;
- change dependencies;
- create migrations;
- delete files;
- run destructive commands.

## Result

Preparation must end with one of:

- specification is ready;
- implementation plan is ready;
- task is BLOCKED;
- questions for the operator are needed;
- task is considered too risky in its current form.
