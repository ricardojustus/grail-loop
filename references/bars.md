# Bar Selection — the ceiling's actual craft

Choosing the bar is the highest-leverage decision of an asymptotic run. The original
gauntlet worked because "Call of Duty" was simultaneously the direction AND
unreachable — one reference doing two jobs by accident. Original work forces
the jobs apart:

## The direction / bar split

- **Direction** = what to imitate. A reachable style vocabulary the builders
  aim their choices at (e.g., "painterly realism in the vein of Firewatch").
  Lives in the concept/ambition paragraphs. The builders may depart from it;
  it is a starting language, not a ceiling.
- **Bar** = what to lose to forever. Unreachable masters the critics hold the
  work against, blind. Lives in the HARD-bar sentence and the refs/ folder.

**Never let a reachable reference into the bar set.** The bar is the loop's
stopping condition; the weakest bar defines when pressure relaxes. One
catchable bar = one exit door in a machine designed to have none. And bars
punish deviation while directions permit it: a critic comparing against
Firewatch asks "does this look like Firewatch?" and beats every original
choice back toward a clone. Masters judge *qualities* (composition, warmth,
density); a peer-level reference judges *identity*.

Rule of thumb: if the build could plausibly get within blind-A/B hesitation
distance of a reference during this run, it is a direction, not a bar.

## Choosing the bars

1. **One master per dimension, non-overlapping.** Feel, image quality,
   composition, warmth, dread, density — each gets its own unreachable
   authority. Overlapping bars produce redundant criticism; too many produce
   noise. 3–5 bars plus the systems critic is the ceiling.
2. **Concrete and inspectable.** The critic must be able to hold an artifact
   of yours next to an artifact of theirs. Film stills, shipped-game
   screenshots, real product UI captures, master canvases. If you cannot name
   what artifact gets compared against what reference, the gauntlet is the
   wrong tool for that dimension — route it to the Contract or the systems critic.
3. **Cross-media bars are legal and strong.** Hundred-million-dollar film
   cinematography is a legitimate bar for a game's composition. Master
   animation is a legitimate bar for stylized image quality. The bar's medium
   need not match the build's medium; the *dimension* must.
4. **If the user supplied no bars**: propose them. Ask which comp plays the
   role real Call of Duty screenshots played for the original — the strongest
   concrete unreachable reference per dimension — state each in one sentence,
   confirm only if the choice is genuinely ambiguous.

## Informative-bar diagnostics (mid-run)

Track which bars produce gradient. A bar that never rises above "decisively
loses" across many cycles is pure aspiration — keep one or two of those as
pure-aspiration bars, but they carry no steering information. The gradient lives
in bars producing "narrowly" and "hesitated." Tell critics to spend their
detail budget on informative bars, and exclude non-informative bars from the
altitude-stall plateau test (see plateau.md).

## refs/ lifecycle

- **Offer first, at launch**: ask once whether the user wants to supply
  reference images themselves — captures from products they own are often
  the strongest refs (real gameplay frames beat press glamour shots), and
  user-supplied images take precedence over downloads. Ask at launch only;
  the run goes autonomous after.
- Otherwise populate refs/ by downloading from journalistic, press-kit, or
  official-blog sources. Organized per dimension:

  ```
  refs/
    <dimension-1>/   (~8–10 frames)
    <dimension-2>/   (~8 frames)
    ...
  ```

- **Curate for the shots the build will produce**, not the prettiest images.
  Gameplay/product captures beat hero shots; the critic compares like against
  like. Thirty well-chosen frames beat three hundred random ones — every
  critic sample should be a beating.
- refs/ is **gitignored and never distributed** with the artifact or
  committed to any repository — the images are third-party copyrighted
  material, held locally and used solely for private, transient comparative
  evaluation during the run, then deleted. This handling is what makes
  fetching them appropriate; state it in the .gitignore comment. refs/ is used solely
  for blind comparison.
- **Never delete or modify refs/ during the run** — a sub-agent that "cleans
  up" mid-run silently blinds every later critic, degrading the gauntlet to
  vibes with no alarm. Delete refs/ only as the very final action, after the
  last critic evaluation (see plateau.md finalization).
