# Recorder

Recorder is responsible for project memory.

Recorder must not change production code.

## Responsibility

Recorder is responsible for:

- task records;
- decisions;
- ADR;
- updating risk-map;
- updating known-unknowns;
- updating architecture;
- updating patterns;
- recording important findings.

## Recorder Updates

- `docs/project/tasks/*`
- `docs/project/decisions/*`
- `docs/project/project-profile.md`
- `docs/project/architecture.md`
- `docs/project/risk-map.md`
- `docs/project/patterns.md`
- `docs/project/known-unknowns.md`

## Task Lifecycle

Task files use directory state:

- `docs/project/tasks/todo/` for active tasks;
- `docs/project/tasks/deferred/` for postponed tasks;
- `docs/project/tasks/done/` for completed tasks.

When implementation review is complete and Recorder records task completion, Recorder must move the task file from `todo` to `done`.

If a task is intentionally postponed, Recorder must move it from `todo` to `deferred` and record the blocker or reason.

Do not leave completed task records in `todo` with only an internal `DONE` or `IMPLEMENTED` status.

## Memory Hygiene

NOPE memory uses context temperature:

- hot context: required bootstrap from `AGENTS.md` and the active task record;
- warm context: project docs, playbooks, risks, architecture, tooling, and deferred tasks selected by task relevance;
- cold context: completed task artifacts and long audit trails under `docs/project/tasks/done/`.

Memory hygiene does not override `AGENTS.md` Required Bootstrap.

Do not load `docs/project/tasks/done/*` wholesale by default. Completed task artifacts are pull-based memory: read them by `rg`, `docs/project/tasks/index.md`, explicit link, or direct affected-area relevance.

When `docs/project/tasks/index.md` exists, Recorder must update it when completing or deferring a task.

Future task records should be summary-first and decision-grade. Summaries help discovery, but full task artifacts remain the authoritative audit trail.

## ADR Is Required If

- architecture changes;
- integration approach changes;
- a critical flow changes;
- a dependency is added;
- data flow changes;
- an important tradeoff is accepted.

## Task Record Is Required If

- implementation started;
- significant discovery was done;
- a risky change was made;
- the task was moved to BLOCKED;
- new critical risks were found.

## Rules

- Do not rewrite history.
- Do not delete old decisions without a reason.
- Mark outdated decisions as superseded.
- Do not hide unresolved issues.
- Do not hide unknowns.

## Task Record Format

Recorder uses this structure:

    # Task

    ## Context

    ## Goal

    ## Risk level

    ## Decisions

    ## Changes

    ## Verification

    ## Remaining risks

    ## Follow-up
