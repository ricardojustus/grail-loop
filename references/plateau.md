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

## Finalization

1. Re-verify the **entire Contract** with fresh evidence (gambits can silently
   break early passes).
2. Write FINAL_REPORT.md: what shipped, the margin curves, and the
   persistent-deficiency map — which walls the run died against and how hard
   each was attacked. Both endings are good mornings: "plateaued, gambit
   worked, kept going" or "plateaued, gambit failed, here is exactly where
   the ceiling was."
3. Delete refs/ as the very final action, after the last critic evaluation.

## The outer boundary

The **human** is the outer boundary. A stop order at any time — including a
spend constraint named mid-run ("don't spend more than X") — skips directly
to finalization, noting in the report that the human, not the plateau, ended
the run. There is deliberately no codified budget cap: the spend was
authorized explicitly at the launch gate, and a cap would terminate exactly
the long-tail cycles the pursuit exists for. The plateau standard above is
the honest brake; the human is the absolute one.
