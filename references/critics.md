# Critics — cold reads, blind comparisons, and the ledger

The rule that generates everything here: **cold critics compare; only warm
ledgers count.** Fresh-context critics cannot calibrate absolute scores across
rounds (every fresh critic invents its own meaning of "6/10"), so critics emit
only pairwise verdicts and same-context deltas. The run's memory lives in the
ledger, never in the critics.

## Two levels — the engine and the measurement layer

Judgment runs at two levels, and the first is the one that keeps eyes on
the work while it happens:

- **Level 1 — the piece-loop engine (continuous, inside the build).** Every
  piece with inspectable output — a scene, a screen, a system, a spread —
  gets its own builder and its own fresh-context critic, looping while the
  piece is built: the critic inspects the actual thing AGAINST the piece's
  reference material — real pixels beside the refs/ frames for its
  dimension when the piece is seen; the running product driven through its
  journey when the piece is a system; the real text against the brief when
  the piece is copy — never a summary the builder wrote, and never only
  builder-selected evidence. It names the largest remaining gap relative
  to that reference, and sends the piece back; the builder fixes; a fresh
  critic re-judges. Continuous, woven into building — not batched, not
  deferred to panels. The ORCHESTRATOR spawns the piece critic (never the
  builder) and hands it the artifact, its launch/run command, and the
  piece's reference material. A status line like "the player runs, zero
  exceptions" is a builder summary, not an inspection.
- **Level 2 — the measurement layer (per cycle).** The cold panels this
  file defines — champion–challenger, master A/B, the systems critic —
  plus the ledger and the plateau standard. This layer measures the run
  between cycles; it is layered ON TOP of the engine and never a
  substitute for it. A run whose only judgment is panel judgment has lost
  its engine.

**Telemetry purity**: piece-loop verdicts are advisory fix-fuel for the
builder — they never enter LEDGER.md. Only cold-panel output feeds the
curves; the plateau standard reads panels, not piece-loops.

## Cold-read protocol

- Every critic is a **fresh sub-agent with clean context**. It has never seen
  the project improve, holds no attachment to progress, and knows nothing
  except what this round hands it. A critic that watched the game get better
  grades on a curve; a cold one just sees a build losing to the reference.
- **Never grade ≠ never look.** Builders look at their own output
  continuously while working — launching the thing and sanity-checking your
  own screen is required practice; hours of visual work shipped unseen is a
  build failure. What builders never do is JUDGE: no verdicts, no
  self-graded comparisons, no "my screenshot looks right so the piece
  passes" — the builder's look is a smoke test, and every verdict belongs
  to a fresh-context critic. If it built it, it doesn't grade it.
- Randomize left/right (or A/B) position of images in every comparison —
  LLM judges have position bias. For decisions that matter (champion
  promotion, gambit evaluation), use 2–3 critics and majority-vote.
  **Blind staging is leak-proof by construction**: the side assignment is
  seeded and derivable, never a stored label; filenames handed to a
  critic are neutral; no label rides any path, name, or metadata the
  critic receives; and the seeded mapping is recomputable across
  compaction — a summarized orchestrator re-derives which side was
  which instead of losing the round.
- **A PANEL critic receives exactly the artifacts handed to it** — captures,
  refs, the dimension list, the output format — and nothing else: no
  repository access, no state files, no ledger or journal (those are warm
  context by definition). Spawn panel critics against a directory containing
  only the handed artifacts; the isolation is physical, not instructed.
  A PIECE-LOOP critic (and the systems critic, which drives the artifact)
  is instead handed the running artifact, its launch/run command, and the
  piece's reference material — still nothing warm: no ledger, journal,
  workbench, or prior verdicts. Cold context is the isolation both levels
  share; the artifact surface differs by job.

## Verdict shape (every critic, both levels)

- **Verdict first, stated plainly, before any hedging.** Which side is
  better, or whether the piece passes — then the reasoning. A verdict
  buried under context is a verdict softened.
- **Three deficiencies, largest gap first, each actionable.** A
  comparison names the three specific things the weaker side does worse
  — the largest remaining gap leads (that lead IS the piece-loop's
  verdict; a piece with fewer than three genuine gaps names what remains)
  — each phrased as a change someone could make: "the shadow terminator
  is a hard edge; soften it" — never a mood. These are the itemized
  deficiencies the ledger classifies (panels) or the fix-fuel the builder
  consumes (piece-loops).
- **One honest credit (comparisons).** The one thing the weaker side does
  better, if anything, said plainly. Honesty about partial wins keeps the
  verdict credible.
- **Calibration floors, stated in the critic's brief**: a 7 is a
  competent shipped product; the median first-pass output is a 4. No 8s
  to be polite, and the phrase "given the constraints" (and its family —
  "for a browser game," "considering the scope") never appears: the bar
  is the bar. Named technical defects with a location are free wins —
  always report them.

(The champion–challenger signed margin, −3..+3, is unchanged by this
shape — plateau.md's thresholds read that scale.)

## The capture manifest

At cycle 1, define the capture manifest — scene list, camera positions,
app states, resolutions, and the exact capture commands — and freeze it;
every cycle captures exactly the manifest. Unpinned captures poison the
margin signal invisibly: a champion–challenger verdict between two
different camera angles measures the angle, not the progress, and every
stop rule sits downstream of that signal. The manifest may gain entries as
new subsystems appear; existing entries never change mid-run.

The same discipline binds the artifact: **captures must be deterministic —
same config in, same pixels out** — sameness defined by the preflight's
pixel-diff threshold, byte-identical where the renderer permits it.
Seeded randomness only; stateful animation driven from injected time or
frozen; temporal effects may carry benign nondeterminism — that is what
the threshold absorbs, and without the discipline the screenshot
comparisons are worthless.

Captures are run evidence: stored per cycle (`captures/cycle-N/`), never
deleted or modified until finalization. The champion's captures are the
odometer's memory — deleting them blinds the odometer the way deleting
refs/ blinds the masters.

**The capture preflight runs on every capture invocation.** Before any
capture is handed to a critic or stored as evidence, a deterministic
degenerate-output check runs on it: non-zero file size, resolution matching
the manifest, and the frame not a near-uniform void (single-color,
blown-white, or crushed-black by histogram). The preflight also owns the
run's **sameness threshold** — a pixel-diff tolerance pinned once at
first light (what share of pixels may differ, and by how much) —
consulted wherever two captures are compared for determinism;
byte-identical is that threshold's zero setting, chosen where the
renderer permits it. A failed preflight is an
instrument-floor failure (contract.md): the run's eyes are broken, and
fixing them preempts everything else. An instrument without a schedule is
decoration — the preflight's schedule is every capture, and captures run
from first light onward (SKILL.md, Cycles).

**Piece-loop captures are working evidence, not manifest evidence.** They
live outside `captures/cycle-N/`, are never handed to a panel, and never
join the manifest — a champion–challenger pair drawn from a working shot
measures the angle, not the progress. The preflight still runs on them
(every capture, no exceptions); only their storage and audience differ.

## The hidden set (sealed holdout)

The manifest has a blind spot: every angle the run judges itself on is
also an angle builders get feedback on, so a long run can overfit to the
manifest — polishing the judged shots while everything off-camera lags.
The hidden set is the holdout that catches this.

At cycle 1, alongside the manifest, define a second capture set of the
same form (scenes, cameras, states, exact commands) covering angles and
states the manifest does not — then **seal it**:

- **Stored in orchestrator state only** — the orchestrating context's own
  notes, never the repo's manifest file, CONTRACT.md, LEDGER.md, the
  workbench (an always-visible surface by design), or any file builders or
  critics read. Its existence may be logged; its contents may not.
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

Every PANEL critic returns **itemized deficiencies** (concrete, actionable,
ranked). After each cycle, classify each panel item against the accumulated
ledger — piece-loop verdicts are never classified here (Telemetry purity
above):

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
