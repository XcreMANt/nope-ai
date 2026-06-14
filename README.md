# NOPE

**NOPE — No Opportunistic Production Edits**

NOPE is a risk-driven orchestration system for AI-assisted software development in existing production projects.

Instead of optimizing for maximum autonomy or code generation speed, NOPE focuses on change control, risk reduction, and keeping a human operator in the decision-making loop.

NOPE is particularly useful for:

- legacy systems;
- critical production code;
- projects with a high cost of failure;
- long-lived systems with complex architectures.

NOPE is built on a simple assumption: modern AI models can significantly accelerate software development, but they can also make incorrect assumptions, expand the scope of changes, and underestimate architectural or business consequences.

The primary goal of NOPE is to reduce the likelihood of such failures while keeping the operator responsible for final decisions.

> NOPE is experimental.
>
> It is intended to reduce risk in AI-assisted development, not to guarantee safety.
>
> Final responsibility always remains with the human operator.

---

## How NOPE Differs from Typical AI-Assisted Development

Most AI coding workflows are optimized to reach code changes as quickly as possible.

That approach works well for isolated tasks but becomes increasingly risky as project complexity and the cost of mistakes grow.

NOPE introduces additional analysis and review stages before implementation begins. The system attempts to understand the project, identify risks, define the affected areas of the system, and establish clear boundaries for the requested change before any code is modified.

The goal is not to slow development down, but to reduce the likelihood of:

- misunderstanding requirements;
- unintended scope expansion;
- unsupported assumptions;
- dangerous side effects;
- modifications to critical parts of the system without sufficient analysis.

---

## Core Idea

NOPE does not try to write code as early as possible.

A typical workflow looks like this:

```text
Task
→ Specification
→ Review
→ Approval
→ Implementation Plan
→ Review
→ Approval
→ Implementation
→ Review
→ Verification
→ Recording
```

Both the specification and the implementation plan are reviewed before development begins.

In practice, many AI-related failures occur long before code is written — during requirement interpretation, architectural reasoning, and impact analysis. NOPE therefore places most of its effort on understanding and validation before implementation.

---

## Installation

NOPE is intended to be installed as a nested Git repository inside the target project.

Example for Codex:

```bash
git clone https://github.com/XcreMANt/nope-ai.git /path/to/project/.codex
```

---

## Quick Start

### Step 1. Adapt the Project

Before development begins, run the adaptation workflow.

Example:

```text
Start adaptation workflow via Coordinator.

The project is new.
Do not modify application code before adaptation is complete.
```

NOPE does not assume prior knowledge of the project.

During adaptation, the system studies the project structure, identifies critical flows, maps risk areas, determines verification constraints, and builds an operational model of the system.

Production code should not be modified until adaptation is complete.

---

### Step 2. Start a Task

Once adaptation is finished, assign a task to the Coordinator.

Example:

```text
Start task via Coordinator.

Task:
<task description>
```

You may also describe the task in natural language.

The Coordinator determines the next workflow stage and ensures that required reviews and approvals are completed before implementation begins.

---

## Project Memory

As work progresses, NOPE accumulates project-specific knowledge.

This includes architectural information, decisions, constraints, identified risks, and completed tasks.

Finished tasks are archived, while condensed summaries are stored in indexes. This helps reduce active context size, lower token usage, and make previous decisions easier to discover without repeatedly loading the full project history.

NOPE documentation is split by responsibility:

- `docs/system/` contains reusable NOPE workflow, approval, playbook, template, and control documentation.
- `docs/project/` contains per-project memory created during adaptation and task execution, including project profile, risks, critical flows, decisions, and task records.

---

## Limitations

NOPE does not replace engineers and does not guarantee safe changes.

It is designed to reduce risk in AI-assisted development, not to enable fully autonomous modification of production systems.

The operator remains responsible for:

- decisions and approvals;
- validation of proposed changes;
- verification of results;
- the final state of the production system.

NOPE is not intended for unattended production changes.

---

## Current Status

NOPE is under active development.

The architecture, workflows, and playbooks continue to be tested and refined through real-world production use cases.

Feedback, criticism, and practical experience reports are welcome.

---

## License

MIT License.
