---
name: long_run_saver
description: Reduce token use during long-running asynchronous work by avoiding frequent empty status polls and using long blocking waits. Apply when waiting on commands, background jobs, or yielded functions.exec cells expected to take several minutes; keep interactive input responsive.
---

# Long Run Saver

Use these rules for long-running asynchronous work, within the active tool limits and higher-priority instructions.

- Before polling again, check whether useful independent work can be performed instead. Do that work while the existing operation continues.
- Avoid frequent polling. For empty status polls on operations expected to take several minutes, use long blocking waits whenever supported, typically `180000-300000` ms. Prefer `300000` ms for silent operations when no intermediate output is needed.
- For `write_stdin`, apply long waits only when `chars` is empty or omitted. Do not apply long waits to non-empty calls that send interactive input; use the tool's interactive default or an appropriately short supported interval.
- For `functions.wait`, use a similarly long `yield_time_ms` for genuinely long-running work. Call it only after `functions.exec` returns a running cell ID, and resume that same cell.
- When a nested wait runs inside `functions.exec`, set the outer exec yield deadline at least `30000` ms longer than the longest nested wait whenever supported. For example, a `300000` ms nested wait calls for an outer deadline of at least `330000` ms. If the runtime enforces a smaller maximum, use that maximum instead of repeatedly retrying unsupported values or busy-polling. Await the nested operation so the exec script remains alive; if the outer call yields, continue the existing cell with `functions.wait`.
- Do not poll merely to report that work is still running. Resume substantive reasoning when the process completes, produces actionable output, requires input, encounters an error, or reaches a meaningful monitoring checkpoint. Choose checkpoints around actual decisions, expected milestones, or required communication deadlines.
- A quiet poll or elapsed wait interval does not imply failure. Preserve the existing session, cell, or job identifier. Never restart or duplicate a long-running command merely because a poll returned no output.
