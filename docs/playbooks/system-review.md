# Playbook: System Review

Used to review the NOPE system itself.

## Goal

Understand whether the system has become contradictory, too soft, or incomplete.

## Review

- `master-prompt.md`
- `AGENTS.md`
- `prompts.md`
- `.agents/*`
- `docs/playbooks/*`
- `docs/project-profile.md`
- `docs/risk-map.md`
- `docs/known-unknowns.md`

## Main Questions

- Do AGENTS and playbooks contradict each other?
- Were approval requirements weakened?
- Does any prompt allow bypassing the workflow?
- Is there an adaptation block before code edits?
- Is there a ban on code edits before adaptation?
- Is there escalation for HIGH/CRITICAL?
- Is Recorder present?
- Is Governor present?
- Is system-workflow present?
- Is the next-step mechanism present?
- Are project-specific rules mixed with universal core?
- Are there outdated decisions without SUPERSEDED?

## Verdict

- PASS - the system is consistent.
- PASS WITH CONCERNS - there are issues, but the system works.
- FAIL - the system is dangerous or contradictory.

## Response Format

    # System Review

    ## Verdict

    ## Blocking issues

    ## Non-blocking issues

    ## Contradictions

    ## Missing files

    ## Dangerous shortcuts

    ## Required fixes
