# The Contract — machine-verified completion floor

The Contract answers one question: **is this allowed to ship?** It is binary,
evidence-based, and must reach 100% before any run finalizes. Every run has
one, bounded or asymptotic, bare prompt or vision doc. It is the first artifact
written, before any building starts.

## Why first

Writing the Contract first forces the run to commit to falsifiable criteria before
motivation exists to weaken them. A Contract written mid-run bends toward what
already got built. A Contract written first is a real commitment.

## Sourcing the Contract

**From a vision doc**: the Definition of Done is usually already present in
prose. Extract every completion claim and formalize each into a machine-
checkable criterion: what command, script, test, or captured artifact proves
it. If a criterion cannot be made checkable, either rewrite it until it can be,
or move it explicitly to a Human Touchpoints section with justification — a
criterion silently dropped is a lie of omission.

**From a bare prompt**: author the Contract yourself before building. Ask: if this
artifact were secretly broken, what checks would expose it? Commit those in
writing. This closes the gap that makes pure prompt-runs unfalsifiable
(beautiful screenshots, secretly broken product) while preserving one-shot
spontaneity — the agent authored the criteria, so design freedom is intact.

**The contract cold-read (mandatory, bare-prompt mode only).** A self-authored
Contract has one undefended loophole: honest-looking but hollow criteria.
Before building starts, hand one fresh critic CONTRACT.md and the aim prompt —
nothing else — with two questions: *if this artifact were secretly broken or
hollow, what check is missing?* and *does any criterion's pass depend on
critic judgment or an unreachable comparison? Flag it for removal or
reformulation as a measured benchmark* (the exclusivity law below — one
unreachable criterion deadlocks finalization). Incorporate accepted findings;
log rejected ones with reasons in DECISIONS.md. One dispatch, and even the floor gets
adversarial review before a single line is built. (Vision-doc runs skip this —
the human authored the Definition of Done.)

## What a good criterion looks like

Each Contract item has three fields:

```markdown
- [ ] CRITERION: <the claim, stated falsifiably>
      CHECK: <the exact command / script / procedure that verifies it>
      EVIDENCE: <where the proof lands: log path, screenshot, test output>
```

Good: "A full evening loop completes headless with zero console errors —
CHECK: `npm run headless-playthrough`, EVIDENCE: logs/playthrough-N.log."
Bad: "The game feels polished." (That is ceiling territory, not Contract.)

## Principles (battle-tested)

- **"It should work" is not evidence.** Reliability claims require destructive
  tests: kill processes mid-pipeline, sever connections mid-handoff, fill
  queues and drain them, corrupt an input and watch the failure mode. A claim
  never tested destructively is a hope.
- **Benchmarks become regression thresholds.** When a fixture benchmark sets a
  quality floor (transcription accuracy, FPS, latency), the measured result
  becomes the permanent regression threshold. Later cycles re-run it; falling
  below it is a Contract failure regardless of what else improved.
- **Programmatic over eyeball.** If a check can be a script, write the script.
  Scripts are faster, more reliable, and re-runnable every cycle for free.
- **Sacred data rules go in the Contract.** "Never lose a recording," "never
  modify the read-only folder," "never overwrite fixtures" — encode standing
  invariants as Contract items with checks (e.g., checksum fixtures at start and
  finalization).
- **The Contract is re-verified in full at finalization.** Not "it passed once in
  cycle 2." Every item, fresh evidence, as the last act before FINAL_REPORT.md.
  Late-run gambits and refactors can silently break early passes; the final
  sweep catches it.

## The floor/ceiling exclusivity law

The mirror of bars.md's "a reachable reference is never a bar": **the floor
must be passable; the ceiling must not be.** Contract criteria are reachable
by construction — every item can genuinely go green on this run. Master
comparisons, critic verdicts, and margin thresholds never enter the
Contract, no matter how mechanical they look: "spawn a critic, read the
verdict" is technically a procedure, but its PASS depends on judgment, not
on script output.

This is load-bearing, not taxonomy. A run finalizes only at Contract 100%,
so one unreachable item deadlocks finalization: "beats the master A/B on
atmosphere" can never pass by design, and the run holding it can never end.
The ceiling has stop rules precisely because it never completes; the
Contract has none because it must.

The test, per criterion, at authoring time:

- Pass depends on critic judgment rather than script/test output → ceiling.
- Can never reach 100% → it belongs nowhere: reformulate it as a measured
  benchmark with a fixed threshold (then it is Contract), or hand its
  dimension to the ceiling as a bar.

(Scope: the law governs *criteria*. The contract cold-read above still uses
a critic, legally — its output is advisory review of the Contract, never a
criterion's pass condition.)

**User quality language routes to the ceiling by default.** "At X quality,"
"AAA," "as good as X" — including the degenerate prompt "make me Call of
Duty at Call of Duty quality" — names ceiling material: bars and direction.
The Contract receives only the quality demand's measurable shadow, authored
by the agent: performance floors, completion checks, stability under
destructive tests, playable end to end. (One unreachable reference legally
serving as concept, direction, and bar at once is fine — see bars.md; the
split forbids only reachable references from being bars.)

When in doubt at the boundary: if a criterion can genuinely reach done, it
is Contract. If "better" remains meaningful past any achievable threshold,
it is ceiling. Put the measurable floor in the Contract (60fps minimum,
WCAG AA contrast, test suite green) and the aspiration in the ceiling (feel
like Insomniac, read like Linear). The same dimension often appears in
both, at different altitudes. That is correct, not redundant.
