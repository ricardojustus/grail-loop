# Keep-alive — the anti-stall layer

The stop rules (SKILL.md, plateau.md) decide when a run legitimately ends.
This file is the other half: how an unattended run avoids ending by
accident — a turn that quietly yields with work outstanding, a dead
delegate nobody notices, a loop that looks finished because nothing woke
it up. Stalling silently is a run failure even when every artifact so far
is good, because the human authorized a run, not a nap.

**Deference rule (same pattern as JOURNAL/DECISIONS): where the harness
provides an autonomous-running convention — heartbeats, watcher
discipline, stop boundaries — invoke it at launch and it supersedes this
baseline. Otherwise apply the baseline below.**

## Heartbeat

Never end a turn with outstanding run work and no scheduled re-entry.
Before yielding, arm a fallback wakeup — roughly 20–30 minutes — via
whatever re-entry mechanism the runtime provides (a scheduled wakeup, a
timer, a cron slot). Completion notifications from delegates are the fast
path; the heartbeat is the guarantee for when nothing fires. A wakeup
that finds nothing actionable re-arms and yields — that is the mechanism
working, not waste.

## Watcher discipline — two delegate classes, opposite semantics

- **External-CLI implementers** (an implementation job driven through a
  broker or companion CLI, e.g. Codex): these are **broker jobs**. Ask
  the broker for status directly; never infer state from silence or an
  empty log. Job-loss is terminal, not retriable-in-place — salvage any
  partial output, relaunch fresh with a new job, and never poll a dead
  job ID.
- **Runtime-tracked subagents** (critic panels, workflow stages,
  in-harness builders): the runtime notifies on completion — **silence is
  not death**. Do not kill or relaunch on a hunch, and never touch a
  possibly-live subagent's workspace: a two-writer collision is the worst
  self-inflicted failure a run can have, because it corrupts the very
  evidence the run judges itself by. Confirm a delegate is dead through
  the runtime's own state surface before taking over its work.

## The hard loop (optional)

A Stop-hook completion-promise: a hook on the runtime's stop event
re-injects the run prompt until an exact finalization phrase appears or
an iteration cap hits.

- **Bounded runs**: phrase = the Contract-verified finalization line;
  cap = a generous ceiling — the Contract is reachable, so the cap is a
  runaway brake, not a budget.
- **Asymptotic runs** (optional): phrase = the FINAL_REPORT finalization
  line; cap = the max-cycles constraint, where the human named one.

Generic shape — adapt to the runtime's hook schema:

```text
on stop-event:
  transcript contains "<EXACT FINALIZATION PHRASE>" → allow the stop
  iterations ≥ CAP → allow the stop, flag it: "cap-stopped, NOT finished"
  otherwise → block the stop, re-inject the run prompt
```

The hard loop complements the stop rules and relaxes none of them: the
phrase appears exactly when the normal rules end the run, and only
genuine finalization may write it. Keep-alive keeps the run alive, never
"done" — a mechanism that manufactures the phrase to escape the loop has
inverted the design.
