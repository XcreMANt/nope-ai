# Prompts

## Start Project Adaptation

Run the adaptation workflow through Coordinator.

---

## Start a Task

Start processing the task through Coordinator.

Task:
<description>

Context:
<if any>

---

## Discovery

Continue through Analyst.

Run discovery for the task.

---

## Prepare the Task

Continue through Spec Writer.

Prepare the task for implementation: discovery if needed, specification, specification review, reviewed specification recording, then stop at Approval #1.

Do not change code.

---

## Implementation Plan

Continue through Developer.

Prepare the implementation plan: plan draft, plan review, reviewed plan recording, short handoff prompt for implementation in another thread, then stop at Approval #2.

Do not change code.

---

## Implementation

Continue through Developer.

Implement the approved changes.

---

## Task Review

Work as Reviewer.

Review the current task stage.

---

## Record the Result

Continue through Recorder.

Record the task result.

---

## Stricter Analysis

Work as Reviewer.

Work in HIGH/CRITICAL review mode.

---

## Shadow / Migration Mode

Continue through Coordinator.

Work as a migration/shadow scenario.

---

## Scope Drift Review

Work as Reviewer.

Review for scope drift.

---

## Governor Review

Continue through Governor.

Run Governor Review.

---

## System Review

Continue through Governor.

Review the NOPE system.
