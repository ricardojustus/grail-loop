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
the references, keep a live workbench page you can glance at from a phone,
log panel telemetry to LEDGER.md and the run's story to JOURNAL.md, and
stop by explicit rules (plateau / you). You read FINAL_REPORT.md at the end.
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
their approach entirely; in ASYMPTOTIC mode the engine runs there too:
every piece with inspectable output loops with its own fresh-context piece
critic while it is built (`references/critics.md`, the two levels). The
panels measure; the piece-loops keep eyes on the work while it happens.
(Bounded runs carry neither engine nor panels — Contract checks are their
whole verification.)

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
2. **Ground in standing state** — for a run invoked inside a repo or
   thread that already carries state files; inert for a fresh standalone
   run, which has no state to read. BEFORE the Contract or bars are
   written, read the DECISIONS/JOURNAL files the active journaling
   convention names (`references/templates.md`) for standing operator
   rulings. A ruling that binds direction is quoted into the run's GIVEN
   material: DECISIONS.md at this step — the durable home every run has,
   which bar selection reads before choosing — and, as each is created,
   the aim prompt's concept/ambition paragraphs (asymptotic) and the
   fan-out's shared preamble (`references/fanout.md`) carry the
   applicable rulings forward, so every builder and bar decision starts
   from them. An aim
   that contradicts a standing ruling is a **launch conflict** — surface
   it to the human at launch; a cycle-4 discovery of a ruling that was
   on disk at launch is a grounding failure.
3. **Launch gate (asymptotic).** Before anything is built, state in one
   short message: this is a deliberate high-token run — cycles of builder
   fan-outs and multi-critic reviews, plus a fresh critic on every piece,
   continuously; the spend is what buys the quality —
   and ask three things: (a) an **explicit GO**; (b) builder/critic
   sub-agents default to the strongest non-frontier tier available
   (Opus-class; the harness's implementer pin where one exists) — default
   fine, or change?; (c) **if the medium-capability gate returns NO**
   (`references/bars.md`), may the run proceed down the research-first
   ladder on its own — bounded, logged, vetted tools only — or hold the
   visual lanes for your word? Stated default when unanswered:
   proceed-with-ladder; CUSTOM-BUILDING stays reserved to the operator
   either way. No GO → no run. There is no budget cap to set — the
   stop rules and the human are the brakes, and the human can always name
   a constraint ad hoc ("don't spend more than X"), which the run obeys
   like any instruction. An invocation that already carries the GO and
   the model answer (a dispatching agent, a pre-authorized handoff)
   passes the gate without re-asking; an absent medium answer takes the
   stated default.
4. **Write CONTRACT.md.** First artifact of every run, before any
   building. From a vision doc: extract the Definition of Done into
   machine-checkable criteria. From a bare prompt: author the criteria
   and commit in writing — then run the mandatory contract cold-read
   before building starts. Mark the **instrument-floor items** — the
   reachable checks that verify first (`references/contract.md` owns the
   definition; the capture preflight belongs to capture-bearing runs —
   asymptotic, or any domain that renders frames — never to a headless
   errand). How, both: `references/contract.md`.
5. **Asymptotic only — select the bars.** Bar selection and the
   direction/bar split: `references/bars.md`. Critic roster and domain
   Contract patterns: the one matching domain file (`references/games.md`,
   `references/apps.md`, `references/design.md`). Build `refs/` per the
   lifecycle in bars.md, then freeze the capture manifest and seal the
   hidden set (`references/critics.md`). Before the first visual
   piece-loop, run the **medium-capability gate** — can the authoring
   toolkit physically reach the bars' form language? Doctrine and the
   research-first answer ladder: `references/bars.md`; a NO is an
   operator touchpoint, never the run's own call.
6. **Fill the aim prompt** (asymptotic) from the skeleton below and
   execute it as your own instructions immediately.
7. **Run the loop**, logging telemetry per `references/critics.md`.
8. **Check the stop rules** (below) every cycle.
9. **Finalize**: re-verify the full Contract from clean state with
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
have a separate, fresh-context sub-agent check it against the reference
material — visually for anything seen, by driving the running product for
systems. That critic must be a really harsh cold reader, and if
it doesn't meet [TIER], it should keep going.

Maintain a simple live progress page (WORKBENCH.md or a local HTML page,
at the access path named at launch) and update it as you work — content
and cadence per the workbench template — so progress can be glanced at
without interrupting you.

Don't stop until a fresh critic, comparing side by side blind, genuinely
struggles to say which side is the reference. You will not reach that
point. Get as close as you possibly can. /loop until it's utterly perfect.
Fan out sub-agents and ultracode.
```

## The loop (both modes)

```
[asymptotic]
build wave — per-piece builder↔critic loops on every inspectable piece
             (a wave = the build phase of one cycle; critics inspect real
              output against the piece's references, continuously;
              critics.md — wave anatomy + briefs + ownership: fanout.md)
  ∥ in parallel: the Contract lane verifies whatever items can run
             (instrument floor first — first light)
→ cycle close = the judged panel:
     capture evidence (preflight on every capture) → spawn FRESH cold critics:
        a) champion–challenger: current vs best-so-far, blind,
           signed margin (−3..+3)
        b) master A/B: per-dimension deltas vs refs/, blind
        c) [domain] systems critic (playability / flow / engineering)
→ classify PANEL deficiencies vs ledger: new / repeat / reintroduced
→ append LEDGER.md → update the workbench → openable artifact exists
→ feed deficiencies back to builders
→ check stop rules → continue | plateau protocol | finalize

[bounded]
build → verify Contract items progressively as their checks can run
→ a bounded cycle closes on a Contract-lane verification round
→ stop at Contract 100% verified with evidence (no panels, no piece-loop
  engine, no ceiling — the Modes table governs)
```

## Cycles (asymptotic) — a cycle ends in a judged panel

A cycle is not a unit of time or a pile of work items: **a cycle ENDS in a
judged panel**, and "cycle complete" without a panel verdict is a
contradiction in terms. Nothing in the run works for hours without eyes:

- **Cycle 1's explicit target is first light** — the artifact builds,
  launches, captures emit and pass the preflight — judged immediately by
  the first panel, however unfinished the content. The first hours of an
  asymptotic run produce a judged picture, not a verified pile.
- **After cycle 1, the panel fires when the wave's piece-loops converge**
  (no piece critic naming a gap the builder has not answered; an
  escalated gap routes up, not to the builder, and never blocks
  convergence — `references/critics.md`) — and an
  open cycle is never left to age: hours of building without a panel means
  close the cycle NOW, take the measurement, and split the remaining work
  into the next cycle. An unclosed cycle is an unmeasured cycle, and the
  stop rules go unchecked exactly that long.
- **Cycle close is a checklist, and every item is a gate**: panel verdict
  recorded → LEDGER.md appended → workbench updated → an **openable
  artifact** exists — a build, page, or render the human can launch or
  open themselves, however unfinished the content; piece frames are
  working evidence, never the cycle's proof. A stale workbench or a
  missing openable artifact blocks cycle close exactly as a failed
  preflight blocks a capture, and the next wave does not start until the
  checklist is green.
- A work item whose output can be inspected — a seen surface (rendering,
  lighting, VFX, animation, UI), a system (its running behavior), or copy
  (its real text) — does not close until its piece-loop critic has seen
  that real output (`references/critics.md`).
- The Contract lane never delays a panel (`references/contract.md` — a
  lane, not a gate).

(Bounded runs have no panels: a bounded cycle closes on a Contract-lane
verification round, and the run ends at Contract 100% — the Modes table
governs.)

## Stop rules — checked every cycle

**Bounded mode stops** at Contract 100% verified with evidence — its
completion finish line — or on the human's stop order, which reaches
both modes (`references/plateau.md`, the outer boundary; a bounded
human-stop finalizes at the Contract's current verified state, per that
section).

**Asymptotic mode ends** on the first of:

1. **Plateau confirmed** — plateau is DECLARED (any 2 of 3 tests over
   the evaluation window after the minimum cycle count, or the
   oscillation override — the same deficiency reintroduced twice in the
   window — declared immediately, skipping the vote; thresholds, window,
   minimum: `references/plateau.md`), the plateau protocol runs —
   snapshot → notify the human on the configured channel (continue
   without waiting) → ONE bounded structural gambit at the top
   persistent deficiency — and the gambit's exit test FAILS
   (champion–challenger margin < +2). Declaration alone never ends the
   run: a decisive gambit (≥ +2) means the plateau was local — reset the
   window, resume — and finalizing on a bare declaration, protocol
   unrun, is a stop without a fired rule.
2. **The human says stop** — anytime. A stop ORDER ends the run now; a
   named spend CEILING ("don't spend more than X") is an instruction the
   run obeys, becoming a stop only when the ceiling is reached
   (`references/plateau.md`, the outer boundary, owns the split).
   Deliberately no codified budget cap: the spend is pre-authorized at
   the launch gate, and a cap would amputate exactly the long-tail
   cycles the pursuit exists for.

**The stop list is closed.** A run ends by a fired rule — bounded at
Contract 100% or the human's stop order, asymptotic by rules 1–2 — and
no other way. Direction doubt, inferred operator intent, spend concern,
or any other judgment is never a stop: it is a QUESTION — park it in the
journal, notify the human on the configured channel, and keep running
every lane the question does not gate. When every remaining lane is
gated on the question, enter the parked-question hold
(`references/keepalive.md`; a superseding harness convention implements
the same hold): armed re-entry, no FINAL_REPORT, no stop record — a
hold awaits an answer; an end requires a rule. A stop attributed to the
human requires the human's instruction from THIS run, quoted verbatim
in the run-record entry that records the stop — LEDGER.md in an
asymptotic run, the journal in a bounded one — and an inferred stop
written as "human-stopped" is a falsified record. A run that stopped
without a fired rule has failed, whatever its reasoning.

The gambit is not plateau-locked: on structural evidence it also fires
MID-RUN, where its exit test decides the gambit's fate, never the run's.
Full protocol, mid-run triggers, and the mode-split exit test:
`references/plateau.md`.

## Rules — both modes

Each line is the rule; the named reference owns the procedure and numbers.

- **All verdicts come from fresh, separate cold critics** — output is
  graded only by contexts that did not build it. Builders look at their own
  output continuously while working; they never grade it (never grade ≠
  never look). CEILING critics exist in asymptotic mode only — a bounded
  run's verdicts are its Contract checks — but the contract cold-read
  (`references/contract.md`) runs in every bare-prompt run, both modes: it
  reviews the Contract, not the artifact. Protocol + the two judgment
  levels (piece-loop engine / measurement panels): `references/critics.md`.
- **Critics compare; only warm ledgers count.** Pairwise verdicts and
  same-context deltas; the run's memory lives in LEDGER.md.
- **Visual authoring needs hands and eyes in one body.** A seat takes
  visual authoring only if it natively reads images AND gets a fresh
  capture of its own output in seconds — captured directly, or fed by a
  warm capture service the run controls; eyeless seats take work whose
  feedback medium is logs and numbers — systems, tests, tooling, the
  Contract lane. Detail + the full wave anatomy (doc trio, briefs,
  ownership, triage seats): `references/fanout.md`.
- **Evidence decides.** Contract items are verified by scripts, tests,
  destructive trials, or captured artifacts — "it should work" is not
  evidence. The Contract is a parallel lane, never a gate in front of
  judgment; only the instrument floor (build, launch, passing captures)
  schedules first. Doctrine: `references/contract.md`.
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
- **The workbench keeps the human's glance cheap.** The run maintains a
  simple auto-updating progress surface (WORKBENCH.md or a local HTML
  page) and NAMES ITS ACCESS PATH at launch — a file only the workstation
  can read is not glanceable; where the harness provides a synced or
  served surface the human already reads, use it. Visual observability,
  not telemetry: the LEDGER measures, the workbench shows. The sealed
  hidden set never appears on it. Content list + update cadence:
  `references/templates.md`.
- **Smoothing pass** (optional; the harness binding may turn it on or
  off): at the end of a MAJOR wave — a milestone, not every cycle — one
  fresh agent inspects the complete artifact for coherence across
  separately-improved pieces — resolving seams and conflicts, never
  redesigning. Independently-improved pieces drift apart; the smoothing
  pass is the counterweight.
- **Process vocabulary stays out of the artifact.** Contract, ceiling,
  champion, ledger, plateau, gambit describe the methodology only; the
  artifact's code, naming, copy, and content take vocabulary from the
  user's concept alone.
- **State files are the review interface.** Maintain CONTRACT.md,
  LEDGER.md + the workbench (asymptotic), and FINAL_REPORT.md — templates in
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
- `references/critics.md` — the two judgment levels (piece-loop engine +
  measurement panels), cold-read protocol, verdict shape, capture
  preflight, champion–challenger comparison, master A/B decomposition,
  signed margins, deficiency ledger, telemetry schema.
- `references/fanout.md` — wave anatomy: the doc trio, builder briefs +
  the eye mandate, ownership and the builder report, the triage
  seat, seat anatomy.
- `references/plateau.md` — plateau thresholds and window, the plateau
  protocol, the gambit, finalization.
- `references/keepalive.md` — the anti-stall baseline: heartbeat, watcher
  discipline, the parked-question hold, the optional Stop-hook hard loop
  (applies when no harness autonomous-running convention supersedes it).
- `references/bars.md` — bar selection, direction/bar split,
  informative-bar diagnostics, refs/ lifecycle.
- `references/games.md` / `references/apps.md` / `references/design.md` —
  domain packs: Contract patterns, critic rosters, bar libraries.
- `references/templates.md` — CONTRACT.md, LEDGER.md, WORKBENCH.md,
  JOURNAL.md, DECISIONS.md, FINAL_REPORT.md skeletons.

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
