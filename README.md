# Grail Loop

An autonomous build methodology for coding agents: a machine-verified floor, an unreachable ceiling, and an honest stop.

Point it at a game, an app, a site, or a design piece. It writes a machine-checkable definition of done before building anything, then builds in cycles while fresh cold-context critics blind-compare every cycle's output against master references it can never match (real film stills, shipped AAA frames, best-in-class product UI). The pursuit of an unreachable bar is what forges the quality. Telemetry, not vibes, decides when the run ends.

Ships as a [Claude Code](https://code.claude.com) skill: one `SKILL.md` router plus eight on-demand reference files.

## Why it exists

The Grail Loop is Ricardo Justus's synthesis of three ancestors, each with a defect the others fix:

1. **The Ralph Loop**: run until externally validated. Simple, but nothing defines "validated."
2. **Matt Shumer's [Gauntlet Loop](https://github.com/mshumer/Claude-of-Duty)** (the prompting method behind Claude of Duty): builder sub-agents fan out while a harsh fresh critic blind-compares screenshots against real Call of Duty footage, never approving. The unreachable bar is the engine, and it produces startling quality. But it is unfalsifiable (beautiful screenshots can hide a secretly broken product) and it has no honest stop: the human is the brake.
3. **A contract-first build methodology** Ricardo had already used before the gauntlet had a name: machine-checkable completion criteria, destructive testing, "it should work" is not evidence. An earlier, weaker version of this loop one-shotted a full production app in 22 hours. But a contract alone stops exactly at spec and never enters the quality-squeezing phase.

The synthesis: **floor and ceiling simultaneously, plus the telemetry that replaces the human brake.**

## The two layers

| Layer | Question it answers | Mechanism |
|---|---|---|
| **The Contract** (floor) | Is this allowed to ship? | Machine-verified criteria, written before any building. Binary, evidence-based, must reach 100%. Destructive tests included. |
| **The ceiling** | How good is it when it ships? | Per-dimension master references, compared blind by fresh cold critics every cycle. Asymptotic by design: the comparison keeps failing, and the margin data is the point. |

Two modes: **bounded** (Contract only, for work with a real finish line) and **asymptotic** (Contract plus ceiling, for anything with a quality dimension worth chasing).

## The instruments

Fresh critics cannot calibrate absolute scores across rounds (every fresh judge invents its own meaning of "6/10"), so critics emit only pairwise verdicts and deltas. The run's memory lives in a ledger, never in the critics:

- **Champion vs challenger** (the odometer): each cycle blind-compared against the best cycle so far, signed margin from -3 to +3. Measures whether the run moved.
- **Master A/B** (altitude): per-dimension blind deltas against the reference masters. Measures which way is up.
- **Deficiency ledger**: every complaint classified new / repeat / reintroduced, with fix attempts counted. A twice-attacked survivor reported by critics who never met each other is a wall, and the map of walls ships in the final report as a first-class deliverable: where the model's ceiling actually sits.

## The honest stop

An unreachable bar with no brake is a token furnace. The run ends only by explicit rule:

1. **Plateau declared**: 2 of 3 stall tests hold over a 3-cycle window (margin stall, altitude stall, criticism exhaustion). Declaration triggers one structural gambit at the top persistent deficiency; a decisive win resets the window, anything less finalizes.
2. **Oscillation**: the same deficiency reintroduced twice (fixed, broken, fixed, broken). Immediate declaration, the loop is chasing its tail.
3. **The human says stop**, anytime.

There is deliberately no codified budget cap: a cap amputates exactly the long-tail cycles the pursuit exists for. Instead, the skill will not start without an explicit GO (see below), and you can name a spend constraint at any moment.

## Cost: read this before running

**A Grail Run is a deliberate, heavy token spend.** Asymptotic mode runs cycles of builder fan-outs and multi-critic reviews, potentially for hours. That spend is the price of very high quality output in one autonomous shot. The skill states this and asks for your explicit GO at launch, plus one question (sub-agent model: strongest non-frontier tier by default, currently Opus-class). No GO, no run.

## Install

```bash
git clone https://github.com/ricardojustus/grail-loop ~/.claude/skills/grail-loop
```

Then, in Claude Code:

```
/grail <what you want built>                 the agent picks mode and domain
/grail asymptotic game <one-shot prompt>     full quality pursuit
/grail bounded <task>                        rigor only, real finish line
/grail asymptotic app ./VISION.md            you own design, agent owns execution
```

You can name quality bars ("at the level of X") and a style ("in the vein of Y"), or leave both to the agent.

## Reference images and copyright

Master references (film stills, game frames, product captures) are downloaded to a local, gitignored `refs/` folder, used solely for private, transient comparative evaluation during the run, never distributed or committed, and deleted as the run's final action. Keep it that way.

## What is in the box

```
SKILL.md                    the router: modes, launch gate, loop, stop rules
references/contract.md      writing and verifying the machine-checked floor
references/critics.md       cold-read protocol, blind comparisons, the ledger
references/plateau.md       stall tests, the gambit, finalization
references/bars.md          choosing unreachable masters; direction vs bar
references/games.md         domain pack: games
references/apps.md          domain pack: apps and sites
references/design.md        domain pack: static design work
references/templates.md     CONTRACT, LEDGER, FINAL_REPORT skeletons
```

## License

MIT. See [LICENSE](LICENSE).

Credit where due: the unreachable-bar insight belongs to Matt Shumer's Gauntlet Loop. The floor, the instruments, and the honest stop are what this project adds.
