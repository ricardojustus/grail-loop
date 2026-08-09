# The Plateau Standard and the plateau protocol

An unreachable bar with no brake is a token furnace. The stopping decision
belongs to this standard, not to hope — "it's still improving" is true of
every asymptote forever; that is what asymptote means.

## Preconditions

- **Minimum run length: 4 completed cycles** before plateau is evaluable.
  The early cycles are the steep part of the curve; declaring plateau inside
  them must be structurally impossible.
- **Evaluation window: 3 consecutive completed cycles.** Single rounds are
  noise by design (cold critics vary); windows of 5+ are expensive confidence.

## The three tests (measured over the window)

1. **Odometer stall** — mean champion–challenger margin ≤ +0.5 AND no single round
   exceeded +1. Three straight rounds of losing, tying, or squeaking past the
   champion. One decisive +2 anywhere in the window resets the count: proof
   the vein is not empty.

2. **Altitude stall** — zero net gain in dimension-wins-plus-margin-
   improvements against the masters, counting **only informative bars**
   (bars that have produced at least one "narrowly" or "hesitated" in the
   run). Bars stuck at "decisively loses" forever are the ceiling doing its
   job, not a plateau signal — exclude them.

3. **Criticism exhaustion** — deficiency repeat-rate ≥ 70% across the window
   AND the top persistent cluster has survived ≥ 2 dedicated fix attempts.
   The second clause matters: an unattacked repeat is backlog; a twice-
   attacked survivor from critics who never met each other is a wall.

## Declaration rule

**Plateau is declared when any 2 of 3 tests hold.** Not 1 (each test alone has
a known false positive: odometer stalls during setup refactors; altitude
stalls when critics rotate dimensional focus; repeat-rate spikes when one
stubborn bug dominates while everything else improves). Not 3 (unanimity is
nearly undeclarable and burns tokens waiting).

**Oscillation override — declare immediately, skip the vote**: the same
deficiency classified as *reintroduced* twice within the window (fixed,
broken, fixed, broken). That is the loop chasing its tail; every further
cycle is pure waste, and it is the pattern the 2-of-3 vote catches slowest.

## The plateau protocol (what declaration triggers)

Plateau ≠ stop. On declaration:

1. **Snapshot**: write the ledger state, the persistent-deficiency clusters,
   and the margin curves to the journal.
2. **Notify**: ping the human on whatever channel the harness provides
   (chat, a messaging bridge, email). Do not pause waiting for a reply —
   unattended runs must keep earning their runtime.
3. **The gambit** — one bounded structural attempt at the TOP
   persistent cluster: the refactor-scale move the incremental loop would
   never risk (new rendering approach, restructured system, changed
   architecture). One gambit, clearly journaled as such.
4. **Gambit exit test**: run the champion–challenger comparison on the gambit's output.
   - Margin **≥ +2** → the plateau was local. Reset the window, resume the
     run.
   - Margin **< +2** → the plateau is real. Finalize.

## The mid-run gambit — structural evidence, no plateau required

The gambit is a tool for foundations, and a foundation-level defect does
not wait four cycles to be foundation-level. Without a plateau
declaration, the run is authorized to run ONE gambit when evidence says
the deficiency is structural — any one of:

- **A standing operator ruling names the mechanism** the loop keeps
  refining (the grounding step, SKILL.md On invoke — a ruling found late
  still counts as this trigger the moment it is found).
- **A direction-level dimension sits at "clearly loses" or worse across
  the evaluation window** (the same 3-consecutive-cycle window this file
  defines) with no informative-bar movement — incremental fixes are not
  reaching the dimension.
- **A critic escalation flag**: a verdict marked "not fixable at this
  altitude: medium/structural" (critics.md, verdict shape).

Same shape as the plateau gambit: one bounded structural attempt at the
named deficiency, clearly journaled as a gambit, champion–challenger
exit test. Same rarity: a tool for foundations, never a license to
thrash — a second gambit at the same cluster waits for the plateau
protocol, where the stakes justify it.

**The exit test is mode-split.** At plateau, < +2 finalizes (the
protocol above) — the incremental loop was already exhausted. Mid-run,
the exit test decides the gambit's fate, never the run's: **≥ +2** →
adopt the gambit, reset the window, continue; **< +2** → revert to the
champion, journal the loss, count one dedicated fix attempt on the
cluster, and resume the incremental loop. A failed mid-run gambit is
never a stop — the stop list is closed (SKILL.md).

Two bookkeeping rules keep the mid-run gambit out of the plateau
arithmetic: the fix attempt is counted on the LEDGER cluster the gambit
attacked — a gambit launched from a piece-loop flag records its attempt
only where a panel has raised that cluster (telemetry purity,
critics.md) — and the exit-test margin is an exit test, never a window
round: it enters neither the odometer-stall test nor any other plateau
test.

## Finalization

1. Re-verify the **entire Contract** with fresh evidence (gambits can silently
   break early passes).
2. **Open the hidden set**: capture the sealed holdout shots for the first
   time and run the one-time cold panel (protocol: critics.md). The
   manifest-vs-hidden margin delta goes into FINAL_REPORT's generalization
   line. This audits the stop, it does not gate it — a large delta is a
   finding in the report, never a reason to resume the run.
3. Write FINAL_REPORT.md: what shipped, the margin curves, the
   generalization line, and the persistent-deficiency map — which walls the
   run died against and how hard each was attacked. Both endings are good
   mornings: "plateaued, gambit worked, kept going" or "plateaued, gambit
   failed, here is exactly where the ceiling was."
4. Delete refs/ as the very final action, after the last critic
   evaluation — the hidden-set panel included.

## The outer boundary

The **human** is the outer boundary, in both modes. Two different
utterances, two different acts: a stop ORDER ("stop", "wrap it up") skips
directly to finalization, noting in the report that the human, not the
plateau, ended the run; a spend CEILING ("don't spend more than X") is an
instruction the run obeys — it becomes a stop only when the ceiling is
reached, and the entry recording that stop quotes the ceiling instruction
plus the reading that fired it. Attribution evidence follows the closed
stop list's rule (SKILL.md, stop rules); the run never infers a stop. A
bounded run the human stops finalizes at the Contract's current verified
state — FINAL_REPORT records every still-unverified item; the asymptotic
finalization steps (the hidden set, refs/) do not exist there and are
skipped. There is deliberately no codified budget cap: the spend was
authorized explicitly at the launch gate, and a cap would terminate exactly
the long-tail cycles the pursuit exists for. The plateau standard above is
the honest brake; the human is the absolute one.
