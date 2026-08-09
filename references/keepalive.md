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

## Bounded waits — never block a turn on an unbounded wait

**Scope: these rules govern waits on processes and commands the RUN ITSELF
launches** — players, builds, servers, scripts. Runtime-tracked delegates
AND broker jobs keep the watcher rules above for LIVENESS AND DEATH calls:
silence is not death for a delegate, a broker's state comes from asking
the broker, and no staleness kill ever applies to either. But no in-turn
wait of any kind escapes rules 1 and 3 — a loop polling a broker or
waiting on a delegate's file still carries a hard deadline (the deadline
half of rule 1 only; its staleness kill stays forbidden for these), and
past a few minutes it becomes background work with the heartbeat armed.

The heartbeat guards idle-BETWEEN-turns. A session wedged inside a
synchronous wait is not idle — the wakeup queues politely behind the very
wait it should have broken, and nothing can interrupt the turn from
outside. Three rules make that state unconstructible:

1. **No unbounded waits.** Every blocking command carries a hard deadline
   at the command itself — a timeout wrapper, a launch script with a
   budget, a polling loop with a deadline and a staleness kill. A wait
   that can outlive its budget is a bug at authoring time, not a practice
   to discourage.
2. **Completion is a positive signal only.** Detect "done" by a sentinel
   the work itself writes at genuine completion — a log line, a marker
   file — never by process state. Process state lies in both directions:
   aliveness is not work, and exit is not done — a process that finished
   its work but never exits holds a process-poll wait forever.
3. **A long wait becomes background work.** Anything legitimately longer
   than a few minutes runs as a background task; the turn ends; the
   heartbeat is armed. That converts in-turn blocking (which nothing can
   interrupt) into idle-with-outstanding-work (which the heartbeat
   already guards). Never construct a wait the heartbeat cannot outlive.

The launch-script shape that encodes all three: run the process detached
under a hard deadline, watch for the completion sentinel, kill on
staleness (no new output for N minutes), back it with a watchdog — then
return to the loop and let notifications and the heartbeat do their jobs.

## The hard loop (optional)

A Stop-hook completion-promise: a hook on the runtime's stop event
re-injects a continuation payload until an exact finalization phrase
appears or a cap hits.

- **Bounded runs**: payload = the run prompt; phrase = the
  Contract-verified finalization line; cap = a generous iteration
  ceiling — the Contract is reachable, so the cap is a runaway brake,
  not a budget.
- **Asymptotic runs** (optional): the hook is a STALL-RECOVERY device,
  not a completion device — the stop rules own termination. Payload = a
  continuation sentinel ("resume the run from LEDGER and the compaction
  checkpoint; evaluate the stop rules; continue"), never the original
  aim prompt: re-injecting the aim prompt at cycle 7 induces
  restart-from-zero reasoning, the amnesia the checkpoint exists to
  prevent. Cap = progress-keyed, not run-keyed: N consecutive
  re-injections (default 5) with no new LEDGER entry stops the hook,
  parks a question, and notifies — bounding stall-thrash, never run
  length. The phrase exit still applies when finalization legitimately
  occurs, and only after the stop-rule evaluation is written to LEDGER
  with its evidence. Where the harness carries this shape natively
  (Manifold's autonomous-work completion-promise loop does), defer to
  it.

Generic shape — adapt to the runtime's hook schema:

```text
on stop-event:
  last message contains "<EXACT FINALIZATION PHRASE>" → allow the stop
  cap hit (iterations, or re-injections without ledger progress) →
    allow the stop, flag it: "stopped by the cap, NOT finished"
  otherwise → block the stop, re-inject the payload
```

The hard loop complements the stop rules and relaxes none of them: the
phrase appears exactly when the normal rules end the run, and only
genuine finalization may write it. Keep-alive keeps the run alive, never
"done" — a mechanism that manufactures the phrase to escape the loop has
inverted the design.
