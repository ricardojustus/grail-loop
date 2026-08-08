# Critics — cold reads, blind comparisons, and the ledger

The rule that generates everything here: **cold critics compare; only warm
ledgers count.** Fresh-context critics cannot calibrate absolute scores across
rounds (every fresh critic invents its own meaning of "6/10"), so critics emit
only pairwise verdicts and same-context deltas. The run's memory lives in the
ledger, never in the critics.

## Cold-read protocol

- Every critic is a **fresh sub-agent with clean context**. It has never seen
  the project improve, holds no attachment to progress, and knows nothing
  except what this round hands it. A critic that watched the game get better
  grades on a curve; a cold one just sees a build losing to the reference.
- The builder NEVER critiques its own output. No self-screenshots-review, no
  "use your vision capability on your own UI." If it built it, it doesn't
  judge it.
- Randomize left/right (or A/B) position of images in every comparison —
  LLM judges have position bias. For decisions that matter (champion
  promotion, gambit evaluation), use 2–3 critics and majority-vote.
- **A critic receives exactly the artifacts handed to it** — captures,
  refs, the dimension list, the output format — and nothing else: no
  repository access, no state files, no ledger or journal (those are warm
  context by definition). Spawn critics against a directory containing
  only the handed artifacts; the isolation is physical, not instructed.

## The capture manifest

At cycle 1, define the capture manifest — scene list, camera positions,
app states, resolutions, and the exact capture commands — and freeze it;
every cycle captures exactly the manifest. Unpinned captures poison the
margin signal invisibly: a champion–challenger verdict between two
different camera angles measures the angle, not the progress, and every
stop rule sits downstream of that signal. The manifest may gain entries as
new subsystems appear; existing entries never change mid-run.

Captures are run evidence: stored per cycle (`captures/cycle-N/`), never
deleted or modified until finalization. The champion's captures are the
odometer's memory — deleting them blinds the odometer the way deleting
refs/ blinds the masters.

## The hidden set (sealed holdout)

The manifest has a blind spot: every angle the run judges itself on is
also an angle builders get feedback on, so a long run can overfit to the
manifest — polishing the judged shots while everything off-camera lags.
The hidden set is the holdout that catches this.

At cycle 1, alongside the manifest, define a second capture set of the
same form (scenes, cameras, states, exact commands) covering angles and
states the manifest does not — then **seal it**:

- **Stored in orchestrator state only** — the orchestrating context's own
  notes, never the repo's manifest file, CONTRACT.md, LEDGER.md, or any
  file builders or critics read. Its existence may be logged; its
  contents may not.
- **Never captured, never judged, never named to builders** during the
  run. A holdout that leaks feedback is just more manifest.
- **Opened exactly once, at finalization.**

At finalization, capture the hidden set for the first time and run one
cold critic panel on it — same protocol as a normal master A/B round:
fresh critics, blind, dimension-decomposed, deltas only. Set its margins
beside the final manifest margins and write the difference into
FINAL_REPORT's generalization line: a small delta means the quality
generalized beyond the judged angles; a large delta means manifest
overfitting — reported as a finding. **The panel audits the stop; it
never gates it** — the run ends by the normal stop rules, and a bad delta
is a finding in the report, never a reason to reopen the loop.

## The three comparison instruments

### 1. Champion–challenger comparison (the odometer)

Each cycle, a cold critic receives two unlabeled captures of the SAME scene /
screen / spread: the current cycle's output vs the **champion** (best cycle so
far). Question: which is better, and why? Verdict is a **signed margin**:

```
-3 champion wins decisively   +1 challenger narrowly
-2 champion clearly           +2 challenger clearly
-1 champion narrowly          +3 challenger decisively
 0 genuinely cannot tell
```

Positive → challenger becomes the new champion (progress, machine-confirmed).
Negative → **regression detected**: revert or flag before continuing.
Zero is meaningful — it is what convergence looks like up close.

This is the instrument that CAN pass even while every master comparison fails.
It measures whether you moved; the masters measure which way is up.

### 2. Master A/B (altitude)

Blind comparison of the round's captures against the refs/ masters — but
never as one hopeless binary. **Decompose into dimensions** appropriate to
the domain (e.g., composition, palette cohesion, silhouette readability,
light direction, edge quality, atmosphere; or density, hierarchy, motion,
copy tone for apps). For each dimension, the critic views both images in the
same context and emits either a verdict-with-magnitude (decisively /clearly /
narrowly loses, hesitated, wins) or side-by-side scores from which **only the
delta is kept — absolutes are discarded**. A 4-vs-9 today and a 6-vs-9 next
week from different critics is a real gap-narrowing of 2 even though no
individual score was calibrated.

Some dimensions can genuinely flip against a master (silhouette readability
vs a film still) — those wins are real signal. Some never will (edge quality
vs a $2M/episode animation) — that is the ceiling doing its job.

### 3. Systems critic (what screenshots cannot judge)

One critic per cycle drives the artifact itself: plays a full loop, walks the
core user journey, runs the measurable suite. Domain packs define the roster
(see games.md / apps.md / design.md). Fails the round on anything that stalls
the core experience regardless of how the visuals scored.

## The deficiency ledger

Every critic returns **itemized deficiencies** (concrete, actionable, ranked).
After each cycle, classify each item against the accumulated ledger:

- **new** — never raised before
- **repeat** — raised before, still present
- **reintroduced** — previously fixed, now back (regression of the second kind)

Also record, per persistent item, how many **dedicated fix attempts** it has
survived. A repeated complaint that was never attacked is backlog; one that
ate two fix cycles and returned from critics who never met each other is a
wall. Walls feed the plateau standard and, at finalization, become the
persistent-deficiency map — a deliverable in its own right: the empirical map
of where the model's ceiling sits for this task.

## LEDGER.md telemetry (append every cycle)

```markdown
## Cycle N — <timestamp>
- champion_challenger: <signed margin> (<critic count>, majority)
- champion: cycle <M>
- master_deltas: {bar: {dimension: delta_or_verdict, ...}, ...}
- dimension_wins: <count> (informative bars only)
- deficiencies: new <n> / repeat <n> / reintroduced <n>  → repeat-rate <pct>
- top_persistent: [<item>, fix_attempts=<k>]
- churn: <diff size> vs margin gain → ratio
- contract_progress: <passed>/<total>
- spend: <tokens/hours/cycles consumed so far — telemetry, not a gate>
```

The ledger is the machine version of the human glance that says "it's
improving, keep going" or "it's done, stop" — so a 4 AM run can make that
call with evidence instead of a human making it with a look.
