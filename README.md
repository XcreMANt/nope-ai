# NOPE

**NOPE - No Opportunistic Production Edits**

NOPE is a risk-driven orchestration system for AI-assisted development in existing production projects where mistakes are expensive.

The system is not optimized for maximum autonomy or the fastest possible code generation. It is optimized for controlled changes and reduced risk of side effects.

NOPE is especially useful for:

- legacy monoliths;
- changes in critical code;
- projects with a high cost of failure;
- long-lived systems with complex architecture.

NOPE does not try to fully replace an engineer or make decisions on their behalf.

The system assumes that AI is probabilistic by nature and can be wrong, especially in large projects with complex logic and implicit dependencies.

AI models tend to expand changes beyond the original task scope, make unverified assumptions, and modify related parts of a system without fully understanding the architectural and business consequences.

The purpose of NOPE is to reduce the risk of such changes and prevent AI from making critical architecture or production decisions on its own, without operator control.

---

# Main Idea

Many AI development tools are mainly oriented around task speed and autonomous changes.

NOPE does not try to write code as early as possible. It tries to understand first:

- how the project is structured;
- which parts of the system are affected;
- what risks and unknowns exist;
- what cannot be verified locally;
- where side effects may appear.

---

# Core Principles

- risk-aware changes;
- the smallest necessary change set;
- no opportunistic refactoring;
- no unverified assumptions;
- operator control over changes;
- strict review of risky changes;
- explicit recording of unknowns and doubtful areas;
- rollback awareness;
- protection of critical user flows.

---

## System Limits

NOPE does not guarantee that changes are safe and does not eliminate AI model errors.

The system is meant to reduce the risk of AI-assisted development, not to enable fully autonomous changes to production systems.

NOPE is not designed for unattended production changes.

The operator remains responsible for approving risky actions and for the final state of the system.

---

# Installation

NOPE is best installed as a separate nested git repository. This makes the system easier to update and keeps NOPE separate from project code.

Example for Codex:

```bash
git clone https://github.com/<user>/nope.git /path/to/project/.codex
```

## Important

NOPE is not an immutable framework.

After the adaptation workflow, the system is adapted to a specific project and starts storing project-specific operational knowledge. After that, the contents of `docs/` become project memory for the system.

Before updating NOPE, review possible conflicts between the new NOPE version and the project-specific documentation.

## After Installation

Open the project in the AI assistant and run the adaptation workflow.

---

# Adaptation Workflow

Before development, run the adaptation workflow.

It:

- studies the project;
- identifies critical user flows;
- identifies risk zones;
- identifies dangerous operations;
- identifies verification limits;
- builds a working model of the project.

Changing production code before the adaptation workflow is complete is not recommended.

---

# Operator Language

English is the canonical internal workflow language for NOPE.

The operator may communicate in Russian or another language. If the operator writes in Russian, answer the operator in Russian unless they explicitly ask otherwise.

The operator language must not change the internal NOPE workflow. Terms such as `approval`, `review`, `verification`, `critical flow`, `scope drift`, and `NOPE root` keep their NOPE meaning across languages.

---

# Project Status

The project is in a phase of variable activity.

The architecture, workflow, and playbooks are still being calibrated on real production scenarios.

---

# Search Keywords

AI-assisted development  
risk-driven development  
safe AI coding  
production-safe AI workflow  
AI orchestration  
LLM software engineering  
multi-agent workflow  
critical production systems  
AI governance  
AI coding safety  
legacy-safe AI development

## License

MIT