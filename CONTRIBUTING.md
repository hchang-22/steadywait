# Contributing to SteadyWait

Thanks for helping improve SteadyWait. Keep changes small, evidence-based, and focused on long-running asynchronous work.

## Report an issue

Include enough detail to reproduce the behavior:

- Which agent host and tools were involved.
- What operation was running and how long it was expected to take.
- Which wait or polling behavior occurred.
- What behavior you expected instead.
- Whether the operation was interactive.

Do not include credentials, private logs, or other sensitive data.

## Propose a change

1. Fork the repository and create a focused branch.
2. Update the smallest set of files needed.
3. Preserve the distinction between silent waiting and interactive input.
4. Explain the real scenario that supports an instruction change.
5. Validate the skill folder before opening a pull request.

Changes to `SKILL.md` should solve a demonstrated behavior problem rather than add speculative rules. Documentation-only improvements should not change the skill's behavior.

## Validate

Use the Codex skill validator when it is available:

```text
python path/to/skill-creator/scripts/quick_validate.py skills/long_run_saver
```

The current internal identifier uses an underscore for compatibility with existing installations. Some validators require hyphenated names; note that known compatibility exception rather than silently renaming the skill.
