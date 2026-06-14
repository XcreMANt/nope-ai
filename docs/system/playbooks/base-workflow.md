# Playbook: Base Workflow

This is the main workflow for any task.

Specification and implementation planning stage bundles are defined in:

- `stage-bundles.md`

For MEDIUM, HIGH, CRITICAL, unclear, multi-module, database, external integration, config, deploy, security, or critical-flow tasks, stage bundles are mandatory.

## 1. Determine Mode

Coordinator determines the mode:

- adaptation;
- discovery;
- specification;
- implementation planning;
- development;
- review;
- recording.

If project adaptation is incomplete, move to adaptation.

Coordinator must begin task processing with a handshake:

- detected mode;
- preliminary risk level;
- required roles;
- whether subagents are needed;
- next artifact to produce;
- stop point before the next gated transition.

## 2. Review Adaptation Status

Review `docs/project/project-profile.md`.

If it does not contain the line:

    Adaptation status: complete

then:

- do not change code;
- start the adaptation playbook;
- work only with NOPE root.

## 3. Understand the Task

Coordinator records:

- what the operator wants;
- current context;
- expected result;
- affected areas;
- preliminary risk;
- whether questions are needed.

If the task is unclear, do not move to implementation.

## 4. Discovery

Analyst studies the task in the code.

Need to understand:

- affected files;
- affected flows;
- side effects;
- external integrations;
- database writes;
- background jobs;
- config/deploy impact;
- tests;
- existing conventions.

Discovery results must separate facts from assumptions.

## 5. Specification

Spec Writer writes a specification for non-trivial tasks.

A specification is required for:

- MEDIUM;
- HIGH;
- CRITICAL;
- tasks with unknowns;
- tasks affecting several modules;
- tasks with behavior changes;
- tasks with external integrations;
- tasks with the database.

The specification must include:

- context;
- goal;
- non-goals;
- current behavior;
- desired behavior;
- affected areas;
- risk level;
- requirements;
- acceptance criteria;
- verification plan;
- open questions.

For tasks covered by stage bundles, this step is not complete until Specification Review is complete and the reviewed specification is recorded.

## 6. Specification Review

Reviewer reviews:

- whether assumptions are present;
- whether there is scope drift;
- whether affected areas are defined correctly;
- whether risk level is defined correctly;
- whether a verification plan exists;
- whether edge cases were missed.

If the specification is bad, return it for revision.

## 7. Approval #1

Approval is needed before implementation planning if the task:

- is HIGH;
- is CRITICAL;
- touches a critical flow;
- touches the database;
- touches auth/security;
- touches integrations;
- touches deploy/config/secrets.

Do not continue without approval.

Clarifications, corrections, additional requirements, and answers to questions are not approval.

The assistant must ask a direct approval question in the operator's language that names the reviewed specification and states that approval unlocks implementation planning only.

Required semantic fields:

- stage;
- blocking condition;
- direct approval question.

English example:

```text
Stage: Specification Review complete.
Blocked until: operator approval of the specification.
Question: Do you approve this specification so I can prepare the implementation plan?
```

Russian example:

```text
Стадия: review ТЗ завершён.
Блокировка: нужен approval оператора на ТЗ.
Вопрос: ты approve это ТЗ, чтобы я мог подготовить план реализации?
```

## 8. Implementation Plan

Developer prepares a plan, but does not change code.

The plan must include:

- affected files;
- change order;
- minimal diff;
- risks;
- rollback;
- verification steps;
- what cannot be verified locally.

For tasks covered by stage bundles, this step is not complete until Plan Review is complete and the reviewed plan is recorded.

For tasks that may be implemented in another thread, the completed planning stage must also provide a short implementation handoff prompt that references the reviewed task artifact.

## 9. Plan Review

Reviewer reviews:

- conformance to the specification;
- absence of scope drift;
- regression risk;
- data loss risk;
- breaking change risk;
- security implications;
- sufficient verification;
- rollback.

If the plan is dangerous, return it for revision.

## 10. Approval #2

After approval, code may be changed strictly according to the plan.

Specification approval does not approve implementation.

The assistant must ask a direct approval question in the operator's language that names the reviewed implementation plan and states that approval unlocks code changes only within that plan.

Required semantic fields:

- stage;
- blocking condition;
- direct approval question.

English example:

```text
Stage: Plan Review complete.
Blocked until: operator approval of the implementation plan.
Question: Do you approve this implementation plan so I can change code strictly within this scope?
```

Russian example:

```text
Стадия: review плана реализации завершён.
Блокировка: нужен approval оператора на план реализации.
Вопрос: ты approve этот план реализации, чтобы я мог менять код строго в его рамках?
```

## 11. Implementation

Developer:

- changes only the approved scope;
- does not do opportunistic refactoring;
- does not add dependencies without approval;
- does not change the database schema without approval;
- does not change config/deploy/secrets without approval;
- preserves project conventions;
- records modified files.

## 12. Verification

Run available verification:

- tests;
- lint;
- build;
- typecheck;
- manual scenarios.

If verification cannot be run, state why explicitly.

## 13. Implementation Review

Reviewer reviews:

- conformance to the specification;
- conformance to the plan;
- Coding Behavior Filter from `docs/system/coding-behavior.md`, if code changed;
- absence of extra changes;
- side effects;
- backward compatibility;
- data integrity;
- security implications;
- tests;
- rollback risk.

For tasks with code changes, failing the Coding Behavior Filter blocks completion until the implementation is revised or an explicit approved exception is recorded.

Verdict:

- PASS;
- PASS WITH CONCERNS;
- FAIL.

## 14. Recorder

Recorder records the result:

- task record;
- decisions;
- ADR, if needed;
- risk-map update, if needed;
- known-unknowns update, if needed;
- architecture/patterns update, if new facts appeared.

Recorder also updates task directory state:

- completed task records move from `docs/project/tasks/todo/` to `docs/project/tasks/done/`;
- postponed task records move from `docs/project/tasks/todo/` to `docs/project/tasks/deferred/`;
- active task records remain in `docs/project/tasks/todo/`.

Do not leave completed task records in `todo` with only an internal `DONE` or `IMPLEMENTED` status.
