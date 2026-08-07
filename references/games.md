# Domain pack — Games

## Contract patterns (floor)

- Builds and launches clean; zero console errors across a full session.
- A **headless scripted playthrough** completes the core loop start-to-finish
  (script it; it becomes the regression check every cycle).
- FPS floor on the target profile (measure, record, threshold).
- Every declared mechanic reachable and functional (input → observable
  effect, verified by the playthrough script, not by reading the code).
- Persistence/save/chaining systems survive a kill-and-relaunch destructive
  test.
- Asset integrity: no missing textures/models/audio at runtime (scan logs).

## Critic roster (ceiling)

- **Visual critic** — champion–challenger comparison + master A/B per critics.md. Capture
  in-game frames from the actual playable build (not staged renders) at the
  camera angles real play produces. Suggested dimensions: composition,
  palette cohesion, silhouette readability, light direction, edge/material
  quality, atmosphere, UI integration.
- **Feel critic** — judges motion from **sampled frame sequences**, not
  single stills (critics read images; no agent watches video): extract
  frames at fixed intervals (150–250ms) from a scripted traversal, present
  them as ordered strips, and read motion quality from the inter-frame
  deltas — blur, spacing, camera lag, continuity. Camera behavior at speed,
  animation weight, feedback juice, transition smoothness. Motion is where
  AAA lives; a lone still cannot judge it.
- **Playability critic** (the systems critic) — plays a full loop cold and
  fails the round on anything that stalls momentum, breaks the core tension
  mechanic, or makes goals illegible. Where mechanics ARE the identity
  (countdown pressure, emergent behavior), verify by simulation: does the
  designed dynamic actually emerge from the rules, or is it scripted?

Flow metrics are machine-checkable feel: airtime %, chain length, whether a
skilled bot path ever stalls, time-to-first-input-response. Put floors in the
Contract; put "feels like [master]" in the ceiling. Frames for judgment,
scripts for numbers — a mechanical metric never goes to a critic.

## Bar library (unreachable masters by dimension)

- Third-person traversal feel: Marvel's Spider-Man 2; Titanfall 2 (first-
  person chaining); Ghostrunner (speed readability).
- Photoreal outdoor lighting: Forza Horizon 5; Red Dead Redemption 2. (Only
  for photoreal directions — a photoreal bar fights a stylized direction.)
- Stylized image quality: Arcane (painted light); Spider-Verse films.
- Warmth / neighborhood color: Studio Ghibli (Kiki's Delivery Service,
  Whisper of the Heart).
- Suburban / familiar-place dread: Alan Wake 2; The Last of Us Part II.
- Scale awe: Shadow of the Colossus.
- Emotional glide / light: Journey.
- Cinematic composition: actual film stills of the genre's defining
  cinematographer (Spielberg-era Amblin for suburbia, etc.). Film is a legal
  and powerful cross-media bar.

Directions (reachable — never in the bar set): Firewatch, Alto's Odyssey,
Lonely Mountains: Downhill, Knights and Bikes, vanilla-era MMO zones, GBA-era
polish. Use as art-direction vocabulary in the concept paragraphs.

## Notes

- Do not specify engine/tech as a ceiling in the concept ("browser-based"
  levels the ambition down); state the stack once at the end, as an
  implementation note, per the skeleton.
- Third person vs first person: declare it, and reinforce with a matching
  feel bar.
- Original premise + famous quality bars is the sweet spot: the concept
  paragraph carries the originality; the bars carry the judgment.
