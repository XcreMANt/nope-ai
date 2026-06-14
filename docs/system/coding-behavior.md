# Coding Behavior

This document defines a mandatory behavior filter for code changes in NOPE.

It is subordinate to:

- risk classification;
- stage bundles;
- approval contract;
- critical-flow rules;
- security and data-integrity review;
- operator-approved scope.

It cannot bypass specification, planning, approval, or verification requirements.

## Principles

### 1. Think Before Coding

Do not assume silently.

- Mark assumptions explicitly.
- Separate facts, assumptions, open questions, and operator approval.
- If multiple interpretations materially affect implementation, surface them before changing code.
- If a simpler or safer approach exists, say so.
- If confusion affects risk, scope, or verification, stop and ask.

### 2. Simplicity First

Use the minimum design that solves the approved task.

- Do not add features beyond approved scope.
- Do not add speculative flexibility or configurability.
- Do not add abstractions for single-use code unless the approved plan requires them.
- Do not add error handling for impossible scenarios unless evidence shows they are possible.
- If the implementation is larger than needed, simplify before review.

### 3. Surgical Changes

Touch only what the approved task requires.

- Every changed line must trace to the specification, approved implementation plan, or an explicitly approved exception.
- Do not improve adjacent code, comments, formatting, or style as a side effect.
- Match existing project conventions even when a different style would be preferable.
- Remove unused imports, variables, functions, or files created by the current change.
- Do not remove pre-existing dead code unless that removal is approved scope.

### 4. Goal-Driven Execution

Treat success as a verified outcome, not as completed editing.

- Define success criteria before implementation is considered complete.
- Prefer tests or concrete checks that prove the intended behavior.
- For bugfixes, reproduce or describe the failure before claiming it is fixed.
- For refactors, verify behavior before and after when feasible.
- If verification cannot be run, record the limitation and why it is acceptable under NOPE risk rules.

## Coding Behavior Filter

For any task that changed code, Reviewer must run this filter during Implementation Review after available verification and before Recorder marks the task complete.

The filter is additional to normal Implementation Review. It does not replace checks for specification conformance, plan conformance, side effects, backward compatibility, data integrity, security, tests, rollback risk, or critical-flow safety.

Reviewer must check:

- hidden assumptions;
- unapproved scope expansion;
- speculative features;
- unnecessary abstraction;
- drive-by refactoring;
- style or formatting drift;
- changed lines that do not trace to approved scope;
- weak, missing, or overstated verification.

Verdict:

- PASS: the implementation conforms to this filter.
- PASS WITH CONCERNS: non-blocking concerns are recorded and do not invalidate the approved scope or verification.
- FAIL: the task cannot be recorded as complete until the implementation is revised or an explicit approved exception is recorded.

FAIL conditions include:

- changed lines cannot be traced to approved scope;
- implementation adds speculative features, unused flexibility, or unnecessary abstraction without an approved reason;
- implementation changes adjacent code, comments, formatting, or style without need;
- implementation hides assumptions or presents assumptions as facts;
- verification is vague, missing, or claims more than the evidence supports;
- a simpler implementation was available but not considered or rejected with evidence.

Allowed exceptions:

- Broader design can pass only if it is explicitly in the approved plan, required by existing architecture, or approved through a plan revision.
- Missing automated tests can pass only when verification limits are explicitly recorded and accepted by applicable NOPE risk rules.
- LOW trivial tasks may keep lightweight handling, but any code diff still requires scope traceability and no drive-by changes.

## Source Note

This document adapts the useful structure of `multica-ai/andrej-karpathy-skills`, an MIT-licensed guideline set derived from Andrej Karpathy's observations about common LLM coding mistakes.
