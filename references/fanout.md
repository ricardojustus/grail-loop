# Fan-out — wave anatomy for parallel builders

A wave is the build phase of one cycle (SKILL.md). This file owns how the
fan-out itself is built: the documents that make parallel work integrate on
first try, the briefs, the ownership rules, the triage seat, and which seats
may take visual work. The judgment machinery — piece critics, panels, the
ledger — lives in critics.md and is untouched here: fan-out anatomy is about
building in parallel, not about grading.

Everything here applies to any run that fans out parallel builders,
bounded or asymptotic, with one exception: the art notes and the public
rubric are ceiling-fed — they presume refs/ and ceiling critics — and
exist in asymptotic runs only (the Modes table governs). A bounded
fan-out carries the rest: the architecture contract, the briefs (whose
quality bar is the Contract's checks — the naming rule below separates
those two senses of "contract"), ownership, triage, seat anatomy, and
the lead's wave discipline.

## The doc trio (written before the first wave)

Three documents (in a bounded fan-out, the architecture contract alone —
the scope note above), authored by the orchestrator before any builder
is dispatched, do the integration work that briefs alone cannot:

- **The architecture contract** — interface law for parallel builders:
  module signatures, shared context fields, lifecycle, per-subsystem
  budgets, hard conventions (color space, seeded randomness, no binary
  assets — whatever this artifact's floor is). Binding on every builder,
  with the escape valve stated in the document itself: *if you think a
  signature here is wrong, say so in your report — do not silently change
  it.* One naming rule, once: this "architecture contract" is interface
  law between builders — a different object from the run's Contract, the
  machine-verified completion floor (contract.md). The two never share a
  document. For a non-code artifact the interface law is its format —
  the grid, the shared tokens, the export spec.
- **The art notes** — derived from the reference frames, never from
  instinct: specific, checkable observations pulled from the actual refs/
  images, each with its implication for this artifact and a mechanical
  check a builder can run (*"sample the darkest 5% of any frame; if
  R≈G≈B, it is wrong"*). Where a note contradicts the builder's instinct,
  the note wins — it came from a frame that shipped.
- **The critic rubric, public** — every builder reads the bar it will be
  judged against; the dimensions, the calibration, what a 9 looks like.
  Judging stays blind and cold (critics.md). Public rubric, blind
  judgment: knowing the bar sharpens the work; knowing the judge would
  corrupt it.

## Builder briefs

- **One shared preamble.** The floor every builder shares — the
  architecture contract's hard rules, the quality bar, the eye mandate,
  validate-then-report — is written once as a PRE block and concatenated
  onto every task-specific brief. The floor stated once, not N times
  drifting apart.
- **Every brief opens with a where-the-build-is-now block** — what is
  built, what landed last wave, and explicit NOT-to-be-reverted markers
  for fresh fixes a builder might otherwise "clean up."
- **The eye mandate rides every visual brief, near-verbatim:** *Read your
  own screenshots. Look at them. Iterate until they are actually good.
  This is not optional — an agent that edits visuals without looking at
  the result is guessing.* And its reporting half: *report only what you
  verified by looking or by measuring.* (The builder's look is a smoke
  test, never a verdict — critics.md, never grade ≠ never look.)
- **Measure beside looking.** Builders verify with numbers as well as
  eyes: pixel samples and crops of the region under edit, live state
  probes evaluated in the running artifact (a value that never reached
  the shader is invisible in a screenshot), and on/off ablation with
  repeated trials for any performance claim — toggle your subsystem,
  sample frame time, isolate your own cost from ambient noise.

## Ownership and channel

- **Per-builder everything that is cheap to duplicate**: an explicit file
  list per builder (edit only yours), a private output directory and a
  private scratch directory per builder — a shared temp path between
  parallel agents lets one builder's probe file silently clobber
  another's, returning the wrong result with no error. A private
  instance/port per builder too, where the engine is cheap to boot; one
  warm capture daemon where it is not (games.md).
- **A defect in someone else's file goes in your report, never your
  edit.** Cross-file coordination is by reading the other module's API;
  if the fix must live there, the report says so.
- **Shared visual state drifts under siblings.** When parallel builders
  edit lighting, post-processing, or global look, an absolute pixel
  reading taken this round can move under you by next round. Measure
  however is fastest — absolute samples included; a DURABLE claim in a
  report is stated as a ratio within a single frame or as an authored
  value, which survive a sibling's edits where a bare absolute reading
  may not.
- **The builder report is binding, schema-enforced.** Every wave
  agent's return passes through one structured schema naming exactly what
  downstream integration needs: files written, exact exported signatures,
  stubs left for other builders, anything in the architecture contract
  that fought you — and, for visual work, the capture filenames plus your
  own honest read on where they fall short. Close-out fields: **done /
  remaining / verified / notForMe** — a `remaining` item carries the
  measured gap and why the builder stopped (convergence risk after N
  tuning rounds is a legitimate reason); the report documents the stop —
  it never closes the piece: in asymptotic mode closure stays with the
  piece critic (SKILL.md, Cycles), in a bounded run the Contract's
  checks own closure. A `notForMe` item names the owning file. No
  self-graded scores: the honest read is a report; asymptotic verdicts
  belong to cold critics, bounded verdicts are the Contract's checks.

## The triage seat

When a defect crosses subsystems, or survives repeated dedicated fix
attempts — in asymptotic mode that is the ledger's `fix_attempts` count,
and a piece-loop round of critic-names-gap → builder-fixes → re-judge is
the engine working, never a triage trigger; in a bounded run it is
simply repeated failed fixes on the same defect — the next dispatch is
not another fixer. It is one **diagnose-only** seat, at high effort:

- **Diagnosing only. It fixes nothing and edits no source file.**
- Root-cause each defect **precisely — file, line, value, mechanism —
  with numbers** (measured luminance, mesh counts, uniform dumps), not
  impressions. State the hypotheses considered and disprove the wrong
  ones empirically in the running artifact; close with a confidence
  statement.
- Its conclusions ship into the next builders' briefs **as established
  fact, with its confidence statement attached** — the specialists start
  from evidence, not from scratch (where budget permits, paste the triage
  document whole into the fixer briefs). When an investigation method has
  already failed, the brief pivots the method explicitly: *instrument,
  don't read* — a bug that survived code-reading gets a debug output and
  a minimal repro, not more reading.
- Budget note: deep triage is legitimately one of a run's biggest single
  spends, and priced correctly — every downstream fix depends on its
  accuracy. Guessing is worthless here.

## The lead during a wave (both modes)

- **Meanwhile-discipline**: while a wave runs, the lead's own hands
  touch only artifact work no running builder owns — the integration
  spine, design review, the next wave's evidence; its orchestration
  duties (spawning piece critics, closing cycles) continue as ever.
  Idling wastes the window; touching an owned file is a two-writer
  collision.
- **Emergent wave scoping**: each wave's brief is authored fresh from
  the prior wave's findings — in asymptotic mode the panel's
  deficiencies and the triage conclusions; in a bounded run the
  Contract's unmet checks and the builder reports' `remaining` items;
  wave 1 starts from the goal statement and the Contract — never from a
  pre-committed roadmap. The run decides what is next after it sees
  where it is. (A vision doc's own stated sequencing, where one exists,
  is direction the waves honor — the findings still scope each brief.)
- **Optional, for large fan-outs — the post-wave architecture-contract
  check**: one report-only seat mechanically checks every file the wave
  produced against the architecture contract — import/load checks where
  the artifact is code, format and spec checks otherwise — and greps
  its hard-rule bans, before the cycle's closing judgment — the panel
  in asymptotic mode, the Contract verification round in bounded;
  piece-loops keep their own cadence. It fixes nothing; its report
  routes each violation to the owning builder.

## Seat anatomy (detail behind SKILL.md's rule)

Visual authoring needs **hands and eyes in one body**: a seat takes visual
work only if it natively reads images AND gets a fresh capture of its own
output in seconds. An eyeless seat on visual work is guessing by proxy —
it can author shaders forever and never see one frame; relay descriptions
from a sighted helper arrive summarized, stale, and secondhand. Route eyeless
seats to work whose feedback medium is logs and numbers: systems, tests,
tooling, the Contract lane. A warm capture daemon can lend the eyes: a
seat that natively reads images but cannot capture qualifies when a
capture service the run controls feeds it fresh frames in seconds — the
lead's call, per run.

Capture cost is the other half of the same rule: a look must cost seconds,
not a compile-and-launch. Per-builder dev instances where the engine is
cheap to boot; one warm render daemon where it is not (games.md). An
instrument that makes looking expensive silently rations the eye mandate.
