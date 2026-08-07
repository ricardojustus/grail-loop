# State-file templates

The state files are the human's review interface — the run is judged by them
afterward. Write them for honesty, not advocacy.

## CONTRACT.md

```markdown
# CONTRACT — <project> (<bounded run|asymptotic run>)
Source: <bare prompt | vision doc: path> · Authored: <by agent | extracted>
GO: <received at launch, timestamp> · Subs: <model tier confirmed at the gate>

## Definition of Done (all must pass with evidence)
- [ ] CRITERION: <falsifiable claim>
      CHECK: <exact command/procedure>
      EVIDENCE: <path once produced>
(...)

## Regression thresholds (locked once measured)
- <metric>: <threshold> — set in cycle <N>, re-checked every cycle

## Sacred rules (verified at start and finalization)
- <invariant> — CHECK: <how>

## Human touchpoints (explicitly deferred, with justification)
- <item> — <why it cannot be machine-checked>
```

## LEDGER.md

Header block once (ceiling bars, dimensions per bar, refs/ inventory,
informative-bar status), then the per-cycle block from critics.md. Append
plateau evaluations explicitly:

```markdown
### Plateau check after cycle N
window: cycles <a-b> · odometer: <mean margin> (<stall? y/n>) ·
altitude: <net gain> (<stall? y/n>) · repeat-rate: <pct>, top cluster
attempts=<k> (<exhaustion? y/n>) · oscillation: <none | ITEM (declare)>
→ verdict: continue | PLATEAU PROTOCOL
```

## JOURNAL.md and DECISIONS.md

Owned by the harness's general journaling convention when one exists (a
"work autonomously" class skill, an AGENTS.md rule) — grail entries join
those files under that convention. When no convention exists: JOURNAL.md
is chronological, terse, honest — one entry per meaningful event with
timestamps; DECISIONS.md is one entry per decision a reader would
otherwise reverse-engineer (context → options → chosen → why). Grail
events that always merit entries: cycle completions, Contract failures
and fixes, headline critic verdicts, plateau evaluations, the gambit.

## FINAL_REPORT.md

```markdown
# FINAL REPORT — <project>
Outcome: <shipped | plateaued-after-gambit | human-stopped>
Cycles: <n> · Spend: <tokens/hours consumed>

## Contract verification (final sweep, fresh evidence)
<every criterion, pass, evidence link>

## The run in numbers
Champion-margin curve · dimension-wins curve · repeat-rate curve
(informative bars named; aspirational bars named)

## Persistent-deficiency map  ← a first-class deliverable
For each wall: the deficiency, fix attempts, why it held, whether the gambit
attacked it, and the agent's hypothesis (model ceiling vs medium ceiling vs
budget).

## What I would attempt with more budget
<ranked, concrete>
```
