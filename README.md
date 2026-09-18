# long_run_saver

A Codex skill that reduces token use while waiting for long-running asynchronous work. It favors long blocking waits, avoids empty status polling, preserves running jobs, and uses idle time for useful independent work.

## Install on another device

Because this repository is private, sign in to GitHub on the target device first. Then ask Codex:

```text
Use $skill-installer to install the private GitHub skill from https://github.com/hchang-22/long_run_saver.git, path skills/long_run_saver.
```

The installer uses existing Git credentials or `GITHUB_TOKEN`/`GH_TOKEN` to access private repositories. The skill becomes available on the next turn after installation.

## Repository layout

```text
skills/
└── long_run_saver/
    └── SKILL.md
```
