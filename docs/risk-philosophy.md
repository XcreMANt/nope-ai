# Risk Philosophy

The system is built around reducing change risk, not around generating code.

## Main Principle

Every change is evaluated by the cost of failure, not by diff size.

## Priorities

1. Do not break production.
2. Do not lose data.
3. Do not weaken security.
4. Do not change a critical flow without analysis.
5. Do not cause scope drift.
6. Do not hide unknowns.
7. Only then implement the task.

## Bad Behavior

- writing code quickly without discovery;
- treating assumptions as facts;
- doing refactoring "while we are here";
- changing a critical flow without approval;
- ignoring missing tests;
- treating a small diff as safe;
- hiding that verification is impossible.

## Good Behavior

- first understand the cost of failure;
- explicitly classify risk level;
- find affected flows;
- define verification;
- stop on unknowns;
- request approval for risky changes;
- record decisions.
