# SteadyWait

Token-efficient waiting for long-running agent tasks.

SteadyWait is a small Codex skill for commands, background jobs, and other operations that take several minutes. It tells the agent to use long blocking waits when the tool supports them, stop making empty progress checks, keep the current process alive, and work on something useful between real checkpoints.

The public project is called **SteadyWait**. Its internal skill identifier remains `long_run_saver` so existing installs and prompts keep working.

## Why use it?

Frequent status checks burn tokens without moving the task forward. Worse, an empty poll can make an agent assume the command is stuck and start it again. SteadyWait keeps the original job running and waits for output that matters.

## What it changes

- Uses long blocking waits for operations expected to take several minutes.
- Prefers a five-minute wait for silent work when supported.
- Keeps interactive `write_stdin` calls responsive.
- Accounts for nested wait deadlines inside `functions.exec`.
- Resumes reasoning when output becomes actionable or a real checkpoint arrives.
- Reuses the existing process, session, or cell instead of duplicating work.
- Looks for useful independent work before polling again.

SteadyWait is instruction-only. It has no executable code or dependencies, and it does not need credentials or external services.

## Install

Ask Codex to install the skill from this repository:

```text
Use $skill-installer to install https://github.com/hchang-22/steadywait/tree/main/skills/long_run_saver
```

The skill becomes available on the next turn. If it does not appear, restart Codex.

### Manual installation

Copy `skills/long_run_saver` into your personal Codex skills directory as `long_run_saver`:

```text
~/.codex/skills/long_run_saver/
```

## Use

Codex can activate the skill automatically when a task involves genuinely long-running asynchronous work. You can also invoke it explicitly:

```text
Use $long_run_saver while you run this build and wait for it to finish.
```

The skill applies only when long waits are appropriate. It does not delay interactive input or replace tool-specific limits and higher-priority instructions.

## Repository layout

```text
.
├── CONTRIBUTING.md
├── LICENSE
├── README.md
└── skills/
    └── long_run_saver/
        ├── LICENSE.txt
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```

## Contributing

Bug reports and focused improvements are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for the expected workflow.

## License

SteadyWait is available under the [MIT License](LICENSE).
