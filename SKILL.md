---
name: grail-loop
description: >-
  Grail Loop: autonomous build methodology — a Contract (machine-verified
  completion floor) plus an unreachable ceiling of master reference bars
  chased by blind A/B comparison, with plateau telemetry that ends the run
  honestly. Invoke for /grail-loop, "grail loop", or "gauntlet loop", for any long unsupervised
  build run of an app, game, site, or design, when the user asks to build
  "at the level of" a named reference, says "keep improving until", or
  hands over a vision doc or one-shot build prompt.
---

# Grail Loop

Named for its defining move: the run chases reference bars it can never
reach, and the pursuit itself forges the quality. That is the only place
the name appears — the process vocabulary below is what the run thinks in.

Invocation shape: `/grail-loop [bounded|asymptotic] [game|app|design]
[prompt or path to vision doc]` — all arguments optional; infer what is
missing.

**On a bare `/grail-loop`, or when the user asks what this skill is or how
to use it, print the Usage card below, then wait.**

## Usage card

```text
GRAIL LOOP — autonomous build runs with a verified floor and a chased ceiling.

  /grail-loop <what you want built>            I pick mode and domain
  /grail-loop quest game <one-shot prompt>     full quality pursuit (asymptotic)
  /grail-loop errand <task>                    rigor only, no pursuit (bounded)
  /grail-loop asymptotic app ./VISION.md       you own design, I own execution

You can name quality bars ("at the level of X") and a style ("in the vein
of Y") — or leave both to me. I will: write CONTRACT.md (the machine-checked
definition of done) before building, download reference images into refs/,
build in cycles, have fresh cold critics blind-compare every cycle against
the references, log everything to LEDGER.md and JOURNAL.md, and stop by
explicit rules (plateau / you). You read FINAL_REPORT.md at the end.
Asymptotic runs are deliberately token-heavy — I will state the spend and
ask for your explicit GO before the run starts.
```

Two layers answering two different questions:

- **The Contract** (floor): *is this allowed to ship?* Machine-verified
  completion criteria. Evidence, not vibes. Binary, must reach 100%.
- **The ceiling**: *how good is it when it ships?* Unreachable
  per-dimension master reference bars, compared blind by fresh cold
  critics. Asymptotic by design — the comparison keeps failing, and the
  margin data is the point.

The machinery — Contract checks, ledger, plateau standard — measures the
loop **between** cycles. **Inside** a build cycle, builder sub-agents own
their approach entirely; the aim prompt is their whole instruction.

## Modes

| Mode | Layers | Use for |
|---|---|---|
| **bounded** | Contract only | Scripts, migrations, ports, tooling — rigor with a real finish line |
| **asymptotic** | Contract + ceiling | Anything with a quality ceiling worth chasing: games, apps, sites, designs |

Route by stakes: does the artifact have a quality dimension where "better"
is meaningful beyond "done"? Yes → asymptotic. No → bounded. Every run has
a Contract. At invocation, accept any synonym and route by intent —
"quest", "full", "max", "AAA", "masterpiece", "chase the bar", "keep
improving", "make it incredible" → asymptotic; "errand", "quick", "simple",
"just build it", "just ship it" → bounded. The canonical names are for the
run's own thinking; the human never needs them.

## On invoke

1. **Normalize input.** A bare prompt (agent owns the design) and a vision
   doc (user owns design, agent owns execution) are both first-class. If
   stakes are asymptotic but the input is thin, offer one round of rapid
   elicitation to produce a micro-vision — the bare-prompt path stays
   legitimate if declined. Done when: mode and domain chosen, logged in
   DECISIONS.md.
2. **Launch gate (asymptotic).** Before anything is built, state in one
   short message: this is a deliberate high-token run — cycles of builder
   fan-outs and multi-critic reviews; the spend is what buys the quality —
   and ask two things: (a) an **explicit GO**, and (b) builder/critic
   sub-agents default to the strongest non-frontier tier available
   (Opus-class; the harness's implementer pin where one exists) — default
   fine, or change? No GO → no run. There is no budget cap to set — the
   stop rules and the human are the brakes, and the human can always name
   a constraint ad hoc ("don't spend more than X"), which the run obeys
   like any instruction. An invocation that already carries the GO and
   the model answer (a dispatching agent, a pre-authorized handoff)
   passes the gate without re-asking.
3. **Write CONTRACT.md.** First artifact of every run, before any
   building. From a vision doc: extract the Definition of Done into
   machine-checkable criteria. From a bare prompt: author the criteria
   and commit in writing — then run the mandatory contract cold-read
   before building starts. How, both: `references/contract.md`.
4. **Asymptotic only — select the bars.** Bar selection and the
   direction/bar split: `references/bars.md`. Critic roster and domain
   Contract patterns: the one matching domain file (`references/games.md`,
   `references/apps.md`, `references/design.md`). Build `refs/` per the
   lifecycle in bars.md, then freeze the capture manifest and seal the
   hidden set (`references/critics.md`).
5. **Fill the aim prompt** (asymptotic) from the skeleton below and
   execute it as your own instructions immediately.
6. **Run the loop**, logging telemetry per `references/critics.md`.
7. **Check the stop rules** (below) every cycle.
8. **Finalize**: re-verify the full Contract from clean state with
   evidence, open the hidden set for its one-time panel
   (`references/plateau.md`), write FINAL_REPORT.md, deliver the
   persistent-deficiency map — a real deliverable: the evidence-backed
   map of where the model's ceiling was on this run.

## The aim prompt skeleton (asymptotic mode)

Preserve this shape — concept, ambition + bars, fan-out, critic, closing
incantation — it is load-bearing; the exact phrasing is the validated
form. Fill, then execute:

```text
I want you to build [THING]: [concept paragraph — every load-bearing
mechanic or requirement that makes it THIS thing; leave implementation
choices free. Bound the scope concretely (one neighborhood, one core
journey, 5-7 evenings)].

It should be utterly perfect, [LOOK], with every single thing done at
[TIER] quality — from [AREA_1] to [AREA_2] to anything you could think of.
The art direction is [REACHABLE_DIRECTION — a style to imitate]. The HARD
quality bar it must be blind-compared against is [UNREACHABLE_BARS — one
master per dimension, non-overlapping; see references/bars.md]. Reference
frames live in the gitignored refs/ folder; keep refs/ intact for every
critic until the very final action, then delete it.

Fan out sub-agents and have sub-agents tackle each subsystem individually
so that the [THING] is utterly perfect. You should /loop on each item and
have a separate, fresh-context sub-agent check it visually against the
reference material. That critic must be a really harsh cold reader, and if
it doesn't meet [TIER], it should keep going.

Don't stop until a fresh critic, comparing side by side blind, genuinely
struggles to say which side is the reference. You will not reach that
point. Get as close as you possibly can. /loop until it's utterly perfect.
Fan out sub-agents and ultracode.
```

## The loop (both modes)

```
build cycle → machine-check Contract progress (bounded: the whole check)
           → [asymptotic] capture evidence → spawn FRESH cold critics:
                a) champion–challenger: current vs best-so-far, blind,
                   signed margin (−3..+3)
                b) master A/B: per-dimension deltas vs refs/, blind
                c) [domain] systems critic (playability / flow / engineering)
           → classify deficiencies vs ledger: new / repeat / reintroduced
           → append LEDGER.md → feed deficiencies back to builders
           → check stop rules → continue | plateau protocol | finalize
```

## Stop rules — checked every cycle

**Bounded mode stops** when the Contract is 100% verified with evidence.
That is the finish line; there is no other.

**Asymptotic mode stops** on the first of:

1. **Plateau declared** — after the minimum cycle count, any 2 of 3 hold
   over the evaluation window: champion–challenger margins stalled;
   informative bars show zero net gain; deficiency repeat-rate exhausted.
   Thresholds, window, and minimum: `references/plateau.md`.
2. **Oscillation** — the same deficiency reintroduced twice in the window
   (fixed, broken, fixed, broken). Declare immediately; the loop is
   chasing its tail. Overrides the 2-of-3 vote.
3. **The human says stop** — anytime, including a spend constraint they
   named mid-run. Deliberately no codified budget cap: the spend is
   pre-authorized at the launch gate, and a cap would amputate exactly
   the long-tail cycles the pursuit exists for.

Plateau (rule 1 or 2) triggers the **plateau protocol**, not a silent
stop: snapshot the ledger evidence → notify the human on the configured
channel (continue without waiting) → run ONE bounded structural gambit at
the top persistent deficiency. Gambit wins the champion–challenger
comparison decisively (+2 or better) → plateau was local, reset the
window, resume. Anything less → finalize. Full protocol:
`references/plateau.md`.

## Rules — both modes

Each line is the rule; the named reference owns the procedure and numbers.

- **All judgment comes from fresh, separate cold critics** — output is
  graded only by contexts that did not build it. Protocol:
  `references/critics.md`.
- **Critics compare; only warm ledgers count.** Pairwise verdicts and
  same-context deltas; the run's memory lives in LEDGER.md.
- **Evidence decides.** Contract items are verified by scripts, tests,
  destructive trials, or captured artifacts — "it should work" is not
  evidence. Doctrine: `references/contract.md`.
- **Imitate the reachable, lose to the unreachable.** Direction and bar
  are different slots; a reachable reference in the bar set installs an
  exit door. Split: `references/bars.md`.
- **The floor must be passable; the ceiling must not be.** Critic verdicts,
  master comparisons, and margin thresholds never enter the Contract — one
  unreachable criterion deadlocks finalization; user quality language ("at
  X quality", "AAA") is ceiling material by default. Law:
  `references/contract.md`.
- **refs/ stays intact for every critic** until the final action.
  Lifecycle: `references/bars.md`.
- **The capture manifest is frozen instrumentation.** Every cycle captures
  exactly the cycle-1 manifest; per-cycle captures persist until
  finalization — the champion's captures are the odometer's memory.
  Lifecycle: `references/critics.md`.
- **The hidden set stays sealed.** At cycle 1 the run also seals a second
  capture set as a holdout — held in orchestrator state, never in the
  repo's manifest file or anything builders read; never captured, judged,
  or named to builders during the run. Finalization opens it exactly once
  for a cold panel, and FINAL_REPORT carries the manifest-vs-hidden margin
  delta. The panel audits the stop; it never gates it. Protocol:
  `references/critics.md`.
- **Process vocabulary stays out of the artifact.** Contract, ceiling,
  champion, ledger, plateau, gambit describe the methodology only; the
  artifact's code, naming, copy, and content take vocabulary from the
  user's concept alone.
- **State files are the review interface.** Maintain CONTRACT.md,
  LEDGER.md (asymptotic), and FINAL_REPORT.md — templates in
  `references/templates.md` — plus JOURNAL.md and DECISIONS.md, which
  follow the harness's existing journaling conventions when another
  active skill defines them; grail entries join that journal rather than
  fork a second one. Write all of them as if the run's honesty will be
  judged by them, because it will.
- **An unattended run must not stall silently.** Where the harness
  provides an autonomous-running convention (heartbeats, watchers, stop
  boundaries), invoke it at launch — it supersedes the baseline.
  Otherwise apply the portable baseline: `references/keepalive.md`.
- **Operate only inside the declared workspace**, and preserve fixtures,
  captured data, and queued handoffs — destructive tests run on copies
  (`references/contract.md`).

## Reference files

Read on demand, not upfront:

- `references/contract.md` — writing and verifying the Contract;
  extraction from vision docs; self-authored contracts; destructive
  testing.
- `references/critics.md` — cold-read protocol, champion–challenger
  comparison, master A/B decomposition, signed margins, deficiency
  ledger, telemetry schema.
- `references/plateau.md` — plateau thresholds and window, the plateau
  protocol, the gambit, finalization.
- `references/keepalive.md` — the anti-stall baseline: heartbeat, watcher
  discipline, the optional Stop-hook hard loop (applies when no harness
  autonomous-running convention supersedes it).
- `references/bars.md` — bar selection, direction/bar split,
  informative-bar diagnostics, refs/ lifecycle.
- `references/games.md` / `references/apps.md` / `references/design.md` —
  domain packs: Contract patterns, critic rosters, bar libraries.
- `references/templates.md` — CONTRACT.md, LEDGER.md, JOURNAL.md,
  DECISIONS.md, FINAL_REPORT.md skeletons.

## Status lines

Once at launch, then work:

```text
Grail Loop: [bounded|asymptotic] — [THING] [vs BARS, if asymptotic]. GO received.
```

Asymptotic honesty line, once:

> The blind comparison against the master bars will keep failing. That is
> the design, not the defect. The stop rules decide when the run ends —
> and the persistent deficiencies it cannot beat are themselves a
> deliverable.
