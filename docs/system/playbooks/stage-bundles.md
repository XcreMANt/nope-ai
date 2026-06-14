# Playbook: Stage Bundles

Stage bundles define what it means to complete a workflow stage.

For MEDIUM, HIGH, CRITICAL, unclear, multi-module, database, external integration, config, deploy, security, or critical-flow tasks, stage commands are expanded automatically.

The operator does not need to separately request review or recording for specification and implementation planning stages.

## Core Rule

A stage artifact is not complete until its required review is complete and recorded.

The assistant must not stop after producing a raw draft when the requested stage has a required bundle.

The assistant must not move to the next gated stage until the current bundle is complete and the required approval is received.

## Specification Bundle

When the operator asks to prepare a task, create a specification, write a task description, prepare technical requirements, or otherwise prepare work for implementation, the assistant must execute the specification bundle.

Specification bundle:

1. Coordinator confirms mode, risk, roles, and stop point.
2. Analyst performs discovery as needed.
3. Spec Writer drafts the specification.
4. Reviewer reviews the specification.
5. Spec Writer revises the specification if review finds blocking issues.
6. Reviewer re-reviews if the specification changed materially.
7. Recorder saves the reviewed specification and decisions.
8. Assistant stops at Approval #1.

Stop format must be localized to the operator's language.

The wording may vary, but the stop message must include:

- stage;
- blocking condition;
- direct approval question.

Example:

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

## Implementation Plan Bundle

When the operator asks to prepare an implementation plan, plan the implementation, continue after specification approval, or otherwise prepare for code changes, the assistant must execute the implementation plan bundle.

Implementation plan bundle:

1. Coordinator confirms approved specification and planning mode.
2. Developer drafts the implementation plan without changing code.
3. Reviewer reviews the implementation plan.
4. Developer revises the plan if review finds blocking issues.
5. Reviewer re-reviews if the plan changed materially.
6. Recorder saves the reviewed implementation plan and decisions.
7. Assistant prepares a short implementation handoff prompt for another thread.
8. Assistant stops at Approval #2.

Stop format must be localized to the operator's language.

The wording may vary, but the stop message must include:

- stage;
- blocking condition;
- direct approval question.

Example:

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

## Implementation Handoff Prompt

After a reviewed implementation plan is recorded, the assistant must provide a short prompt that the operator can paste into another thread to start implementation.

The prompt must be localized to the operator's language and must use the standard NOPE task-start shape:

```text
Начни обработку задачи через Coordinator.

Задача:
<implement the approved reviewed implementation plan>

Контекст:
План реализации approved.
Документ задачи:
`<path-to-reviewed-task-artifact>`

Код менять только в рамках approved plan.
```

Rules:

- keep the prompt short;
- include the reviewed task artifact path;
- state that the implementation plan is approved only if Approval #2 has actually been given;
- if Approval #2 has not been given yet, provide the same prompt as a template and tell the operator to use it only after approving the plan;
- do not duplicate the full specification or full plan in the prompt;
- rely on Coordinator in the new thread to read NOPE bootstrap and the task artifact.

## Review Requirements

Review must not be a ceremonial pass.

Specification review must check:

- missing or conflicting requirements;
- hidden assumptions;
- scope drift;
- affected areas;
- risk level;
- non-goals;
- acceptance criteria;
- verification plan;
- open questions and blockers.

Implementation plan review must check:

- conformance to the approved specification;
- absence of scope drift;
- regression risk;
- data loss risk;
- breaking change risk;
- security implications;
- external side effects;
- sufficient verification;
- rollback or disablement path.

Reviewer verdicts:

- PASS;
- PASS WITH CONCERNS;
- FAIL.

FAIL returns the artifact to the author role for revision.

PASS WITH CONCERNS may proceed to approval only if concerns are explicitly recorded and do not block the next stage.

## Role Mode And Subagent Mode

Role mode is acceptable for LOW and MEDIUM tasks.

For HIGH and CRITICAL tasks:

- role mode is acceptable when the scope is narrow and the operator has not requested independent agents;
- Reviewer or Governor subagents should be considered when the task has broad scope, high uncertainty, strong external side effects, security implications, or prior workflow drift;
- subagents are not required merely because the bundle contains a review step.

## Operator Experience

If the operator does not know NOPE and asks for the final implementation directly, the assistant should explain the bundle briefly in the operator's language:

```text
I understand the final goal. Because this task is gated by NOPE, I will first run the specification bundle: discovery, specification, review, recording, then stop for approval before planning or coding.
```
