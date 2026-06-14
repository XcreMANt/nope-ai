# Approval Contract

This document defines what counts as operator approval in NOPE.

## Core Rule

An operator task description is not approval.

Clarifications, corrections, additional requirements, answers to questions, and restatements of the final goal are not approval.

Approval is valid only when the operator explicitly approves the current workflow artifact or risky action.

Examples of workflow artifacts:

- specification;
- implementation plan;
- reviewed diff;
- deployment or external side-effect action.

## Valid Approval

Approval must be tied to a named artifact and stage.

Before moving through a gated transition, the assistant must ask a direct approval question in the operator's language that names:

- the current stage;
- the artifact being approved;
- the next stage that approval unlocks.

The labels and wording may be localized, but the three semantic fields are required.

Example in English:

```text
Stage: Specification Review complete.
Blocked until: operator approval of the specification.
Question: Do you approve this specification so I can prepare the implementation plan?
```

Example in Russian:

```text
Стадия: review ТЗ завершён.
Блокировка: нужен approval оператора на ТЗ.
Вопрос: ты approve это ТЗ, чтобы я мог подготовить план реализации?
```

## Invalid Approval

The assistant must not infer approval from:

- the initial request to implement a feature;
- "do it" before the required specification and plan exist;
- "yes" when the current question was not an approval question;
- corrections or additions to the requirements;
- discussion of implementation details;
- urgency or delivery pressure;
- the absence of objections.

## Gate Semantics

Approval for one gate does not approve later gates.

Specification approval allows implementation planning only.

Implementation plan approval allows code changes only within the approved scope.

Review completion does not imply approval.

Recorder output does not imply approval.

## Direct Goal Requests

When the operator states an implementation goal directly, the assistant must still route the request through the workflow.

For MEDIUM, HIGH, CRITICAL, unclear, multi-module, database, external integration, config, deploy, security, or critical-flow tasks, the assistant must:

- start with Coordinator;
- determine risk and mode;
- produce the required artifact for the current stage;
- stop at approval gates;
- avoid implementation until the reviewed specification and reviewed implementation plan are explicitly approved.

The assistant should explain this to operators who may not know NOPE:

```text
I understand the final goal. Because this task is gated by NOPE, I will first prepare the specification and stop for approval before planning or coding.
```

## Coordinator Handshake

At the start of task processing through Coordinator, the assistant must report:

- detected mode;
- preliminary risk level;
- required roles;
- whether subagents are needed;
- next artifact to produce;
- stop point before the next gated transition.

Example:

```text
Coordinator result:
Mode: Specification.
Risk: HIGH.
Roles: Coordinator, Analyst, Spec Writer, Reviewer, Recorder.
Subagents: not needed.
Next: produce and record specification.
Stop point: before implementation planning, pending operator approval.
```
