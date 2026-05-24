# Playbook: Feature

Used to add new functionality.

## Order

1. Coordinator determines risk.
2. Analyst performs discovery.
3. Spec Writer writes the specification.
4. Reviewer reviews the specification.
5. Approval #1.
6. Developer prepares the plan.
7. Reviewer reviews the plan.
8. Approval #2.
9. Developer implements.
10. Reviewer reviews the implementation.
11. Recorder records the result.

## Required Review Points

- Whether the feature duplicates existing logic.
- Whether it breaks existing flows.
- Whether it requires migrations.
- Whether it changes API contracts.
- Whether it affects permissions.
- Whether it affects external integrations.
- Whether rollback exists.

## Forbidden

- Do not cause scope drift.
- Do not do refactoring "while we are here".
- Do not add dependencies without approval.
- Do not change architecture without an ADR.
