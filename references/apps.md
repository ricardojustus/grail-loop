# Domain pack — Apps (and sites)

Apps differ from games in one structural way: a large share of app quality is
invisible to screenshots — correctness, state, latency, edge cases,
accessibility, data integrity. The Contract carries more of the weight here, and
the critic roster swaps accordingly.

## Contract patterns (floor)

- Test suite green; build clean; lint clean.
- **Core-journey scripts**: every primary user journey automated end-to-end
  (create → edit → persist → reload → verify). These are the regression spine.
- Destructive tests: kill mid-write, sever the network mid-sync, fill the
  queue and drain it, corrupt an input file. Sacred-data rules ("never lose a
  record") are Contract items with checksum verification.
- Measurable floors: p95 latency thresholds, Lighthouse scores, bundle size,
  zero console errors, WCAG AA contrast minimums.
- Empty states, error states, and loading states exist for every view
  (enumerate views, check each — screenshot evidence).
- If the app hands off to external systems: schema-validated payloads,
  queue-and-retry survives the destructive tests, idempotent re-delivery.

## Critic roster (ceiling)

- **Visual critic** — champion–challenger comparison + master A/B on real screens of the
  running app (not mockups). Suggested dimensions: information density,
  hierarchy clarity, spacing rhythm, type discipline, color restraint,
  empty/edge-state grace, perceived speed.
- **Flow critic** (the systems critic) — drives the actual app through the
  core journeys cold, like a demanding new user: fails the round on friction,
  dead ends, unexplained states, or anything requiring documentation to
  survive. Counts clicks-to-value and moments of hesitation.
- **Engineering critic** — reviews with measurable bars, not taste: coverage
  thresholds, dependency hygiene, error-handling completeness, the metrics
  suite. Optionally: blind comparison of a module against an excerpt from a
  well-regarded open-source codebase in the same domain — "which was written
  by the senior team?"

## Bar library (unreachable masters by dimension)

- Information density + polish: Linear.
- Marketing/landing surfaces: Stripe.
- Native macOS/iOS craft and delight: Things; Family; Apple's own first-party
  apps of the current design language.
- Interaction delight / micro-motion: Arc-era browser chrome; Family's
  transitions.
- Editorial/marketing sites: Vercel, Linear's site, Stripe's docs.
- Cross-media bars: masterful print/editorial design for typography and
  hierarchy dimensions.

Directions (reachable — never in the bar set): any well-executed peer product
in the same category, established design systems (use as vocabulary: "in the
vein of X's settings pages").

## Notes

- The visual A/B compares like against like: your settings screen next to
  Linear's settings screen, your empty state next to theirs. Curate refs/ per
  screen-type, not per brand.
- Perceived speed is a visual dimension (skeletons, optimistic UI) AND a
  Contract floor (real latency) — encode both.
- For vision-doc runs that integrate with existing infrastructure: the
  environment's ground truth outranks the doc's description of it. Grant
  read-only inspection access; forbid modification outside the declared
  workspace (Contract items with checks).
