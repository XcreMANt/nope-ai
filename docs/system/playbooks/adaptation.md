# Playbook: Project Adaptation

The purpose of this playbook is to safely adapt the universal risk-driven NOPE system to a specific project.

Adaptation is not just a project description.

The purpose of adaptation:

- identify critical flows;
- identify high-risk zones;
- identify the cost of failure;
- identify dangerous commands;
- identify approval points;
- identify verification requirements;
- identify where the assistant is not allowed to act independently;
- calibrate the risk-driven workflow for the specific project.

Until adaptation is complete, the project is considered unknown. Any application code changes are forbidden.

## When To Use

Use if:

- NOPE root has just been created;
- the project is new to the system;
- project-profile is not filled;
- run/test/build commands are unknown;
- critical flows are unknown;
- architecture boundaries are unknown;
- risk zones are unknown.

## Main Principle

During adaptation, priority goes to:

1. understanding the project;
2. defining the cost of failure;
3. finding risky areas;
4. defining the verification strategy;
5. limiting dangerous actions.

Research speed is secondary.

## Hard Bans

During adaptation it is forbidden to:

- change application code;
- change application configs;
- change dependencies;
- create migrations;
- delete files;
- change CI/CD;
- change Docker/deploy;
- run destructive commands;
- do auto-fix;
- refactor;
- perform "quick fixes";
- make assumptions without marking them.

## Allowed

Allowed:

- read files;
- study project structure;
- find entry points;
- analyze dependencies;
- analyze tests;
- analyze CI/CD;
- analyze Docker/deploy;
- find external integrations;
- find background jobs;
- update files inside NOPE root;
- record unknowns;
- record risks;
- record dangerous areas;
- record verification constraints.

## Stage 1. Passive Discovery

Coordinator starts Analyst.

Analyst studies:

- README and documentation;
- dependency files;
- framework config;
- routes / entry points;
- app structure;
- database migrations/schema;
- tests;
- CI/CD;
- Docker/deploy;
- queues/jobs/schedulers;
- external integrations;
- auth/security;
- storage/files;
- logging/monitoring.

Result:

- list of facts;
- list of assumptions;
- list of unknowns;
- list of risky areas;
- list of potentially critical flows;
- recommendations for the next review step.

## Stage 2. Project Profile

Fill:

- `docs/project/project-profile.md`
- `docs/project/tooling.md`
- `docs/project/testing.md`
- `docs/project/conventions.md`
- `docs/project/known-unknowns.md`

Requirements:

- do not write "clear" if it was not verified;
- record unknowns explicitly;
- list commands only if they were found in the project;
- do not copy habits from other projects;
- separately record dangerous assumptions;
- separately record verification limitations.

## Stage 3. Architecture Map

Fill:

- `docs/project/architecture.md`
- `docs/project/critical-flows.md`
- `docs/project/legacy-risks.md`
- `docs/project/patterns.md`

Identify:

- main modules;
- layer boundaries;
- entry points;
- data write paths;
- external integrations;
- background processes;
- critical user scenarios;
- legacy zones;
- places with a high cost of failure;
- dangerous state transitions;
- irreversible operations;
- production-sensitive areas.

## Stage 4. Risk Map

Fill:

- `docs/project/risk-map.md`

Classify project areas:

- LOW;
- MEDIUM;
- HIGH;
- CRITICAL;
- UNKNOWN.

If an area is unclear, classify it as UNKNOWN/HIGH until clarified.

Important:

a small diff does not mean small risk.

## Stage 5. Calibration

After discovery, calibrate:

- risk-levels;
- base-workflow;
- critical-flow playbook;
- prompts, if project-specific control commands are needed;
- AGENTS, if project-specific constraints appeared;
- approval strategy;
- verification strategy;
- rollback expectations.

Important:

universal rules must not be weakened without an explicit reason.

## Adaptation Completion Criteria

Adaptation may be marked complete only if:

- the project stack is identified;
- main entry points are identified;
- install/build/test/lint/run commands are identified or explicitly recorded as unknown;
- architecture is described;
- critical flows are described;
- risk zones are described;
- conventions are described;
- external integrations are described;
- background jobs are described or their absence/unknown status is recorded;
- the way to verify changes is described;
- dangerous areas are described;
- approval-sensitive areas are described;
- unknowns are separated out;
- verification limitations are separated out.

After that, `docs/project/project-profile.md` may be set to:

    Adaptation status: complete

## Final Adaptation Report

At the end of adaptation, Coordinator must report:

- what was studied;
- what was filled;
- critical flows;
- risk zones;
- dangerous areas;
- unknowns;
- verification limitations;
- what must not be done without approval;
- where the assistant must not act independently;
- whether development may start.
