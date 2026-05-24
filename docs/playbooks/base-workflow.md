# Playbook: Base Workflow

This is the main workflow for any task.

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

## 2. Review Adaptation Status

Review `docs/project-profile.md`.

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
- absence of extra changes;
- side effects;
- backward compatibility;
- data integrity;
- security implications;
- tests;
- rollback risk.

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
