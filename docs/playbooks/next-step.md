# Playbook: Next Step

Used when the next correct step must be determined.

## Goal

Do not continue the workflow mechanically if the previous stage is not complete.

## Review Points

Before choosing the next step, review:

- whether adaptation is complete;
- whether the mode is clear;
- whether discovery exists;
- whether the specification exists;
- whether specification review exists;
- whether approval is needed;
- whether the implementation plan exists;
- whether plan review exists;
- whether code may be changed;
- whether a verification plan exists;
- whether Recorder is needed;
- whether there is a BLOCKED state.

## Rules

If adaptation is incomplete, the next step is adaptation.

If discovery is missing, the next step is discovery.

If the task is non-trivial and there is no specification, the next step is specification.

If the specification has not been reviewed, the next step is specification review.

If approval is needed and missing, the next step is approval.

If there is no implementation plan, the next step is plan.

If the plan has not been reviewed, the next step is plan review.

If implementation is done but not reviewed, the next step is implementation review.

If the task is complete but not recorded, the next step is Recorder.

## Response Format

    ## Current stage

    ## Missing prerequisites

    ## Risk

    ## Next correct step

    ## What must NOT be done yet
