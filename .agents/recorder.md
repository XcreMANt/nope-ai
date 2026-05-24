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

- `docs/tasks/*`
- `docs/decisions/*`
- `docs/project-profile.md`
- `docs/architecture.md`
- `docs/risk-map.md`
- `docs/patterns.md`
- `docs/known-unknowns.md`

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
