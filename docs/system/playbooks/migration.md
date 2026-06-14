# Playbook: Migration

Used for migrations, transitions, shadow modes, and replacing an old flow with a new one.

## Main Principle

The old flow must not break before the new one is verified.

## Must Review

- What exactly is being migrated.
- What remains old.
- Whether shadow mode exists.
- Whether rollback exists.
- Whether logging exists.
- How to compare old and new behavior.
- What happens if the new flow fails.
- Whether duplicate side effects may appear.

## Shadow mode

If possible, use shadow mode first:

- the old flow works as before;
- the new flow runs in isolation;
- errors in the new flow are logged;
- errors in the new flow do not affect the user;
- results can be compared.

## Forbidden

- Do not delete old logic before the new logic is verified.
- Do not change production behavior without approval.
- Do not do migration without rollback.
- Do not combine migration and refactoring.
