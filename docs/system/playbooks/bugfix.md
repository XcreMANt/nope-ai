# Playbook: Bugfix

Used to fix defects.

## Goal

Fix a specific bug with a minimal change.

## Order

1. Reproduce or describe the symptom.
2. Find the root cause.
3. Identify the affected flow.
4. Define risk.
5. Prepare the minimal fix.
6. Verify regression risk.
7. Record the result.

## Must Clarify

- What exactly is broken.
- Where it appears.
- When it appeared.
- Which data is affected.
- Whether a temporary workaround exists.
- Whether the bugfix can break a neighboring flow.

## Forbidden

- Do not rewrite the whole module.
- Do not mask the error.
- Do not suppress an exception without a reason.
- Do not change behavior beyond the bug.
