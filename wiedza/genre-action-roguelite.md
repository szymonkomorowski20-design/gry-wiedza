# Genre: action roguelite (Hades-like) — what makes it good

> Part of the gry-wiedza library (`wiedza/`), written for AI agents using the game-builder plugin. Skills and
> recipes named here are game-builder's; read this with `gb doc genre-action-roguelite`. Text: CC BY 4.0 (see
> LICENSE.md).

**What this is:** a reference for building an **original** small action roguelite. That means real-time top-down or
isometric combat, runs made of rooms, random upgrades chosen from offers, and death sending you to a hub with
progress kept. It covers design principles and typical ranges from several games (Hades, Hades II, Dead Cells, Enter
the Gungeon, The Binding of Isaac, Risk of Rain 2, Children of Morta).

**Never copy** their characters, names, story, art, sounds or specific content. Mechanics and genre conventions are
free to use; expression isn't.

**Source quality**, marked on each claim:
- **[dev]**: a developer talk, interview or blog;
- **[analysis]**: design journalism or criticism;
- **[wiki]**: community-documented numbers, not verified against code;
- **[community]**: forum consensus, the lowest confidence.

The full, researched list of claims with URLs is in the Sources section. Numbers are ranges to start from; the
playtest (and recipe 36 simulations) decide.

## The loop at three time scales
- **Seconds:** read an attack, dodge through it, punish in the window after it, combo, dash-cancel.
- **Minutes:** clear a room's waves, then pick a reward. The next door's reward type is shown before you enter.
- **A run (15–40 min for a first clear):** build a direction from offers, survive to the boss, die or win, bank the
  currency. Back at the hub, spend it on permanent options.

Hades is reported at ~15–20 min for an experienced player and ~40 min for a newer one [community]. Isaac and
Children of Morta are at 20–40 min [community/dev]. A run long enough that a late death feels like wasted hours
breaks the "one more try" loop [analysis].

## 1. Combat feel (recipes 47, 43, 32, 33, 03)
- **Every attack has windup → active → recovery.** Only *active* hurts. The player's attacks have the same shape,
  which gives commitment and rhythm. → recipe 47.
- **Input buffer:** writing on action games puts it at roughly 80–250 ms (5–15 frames) [analysis]. Make it
  asymmetric: tolerant for attacks (~6–8 frames), tighter for dodges (~3–4), because a late dodge that fires feels
  worse than a late attack [community]. Recipe 47 uses `buffer_time` 0.15 s for attacks.
- **Dash/dodge** is the main defence.
  - Invulnerability sits on the burst, early to mid animation. Sprinting after it has none [community, Hades].
  - Cancelling the dash into an attack trades its safety for tempo, as a deliberate risk/reward [community].
  - Enter the Gungeon's roll was designed around i-frames to survive dense patterns [dev].
  - → recipe 43 (dash with i-frames); `try_dash_cancel()` in recipe 47 cuts recovery only.
- **Hit feedback:**
  - hit-stop of about 40–80 ms, longer for heavier hits [analysis] → recipe 32;
  - a hit flash → recipe 33;
  - knockback;
  - screen shake scaled to the impact and decaying fast [analysis] → recipe 03.

  "The Art of Screenshake" (Nijman, 2013) is the reference talk [dev].
- **Telegraphs:**
  - Show at least **two simultaneous cues** (animation plus sound or a ground marker), so one missed cue doesn't
    mean an unreadable hit [analysis].
  - A telegraph turns "getting hit" into a question the player can answer. Overlapping tells without priority is
    what makes fights unreadable, not complex single attacks [analysis].
  - Make the visual size of an attack match its danger [analysis].
- **A small verb set is enough** [wiki]. Hades uses attack, special, a limited-charge cast, dash-attack, and a
  gauge-based super. Isaac has one shot and no dodge.

## 2. Enemies and encounters (recipe 49)
- **Archetypes:** rusher, ranged, swarmer, tank. Add summoner/support and area denial for depth. Melee-only
  enemies are dull alone; ranged ones make the level and cover matter [analysis]. Build rooms by **combining** a
  small roster, not by authoring many one-offs.
- **Budgets over hand placement.**
  - Risk of Rain 2's director accumulates credits and spends them on groups from the stage's table [wiki].
  - Children of Morta's fully random placement was hard to control for fairness [dev].
  - Dead Cells places enemies by density rules and metadata, e.g. "1 monster per 5 tiles" of combat space [dev].
  - → recipe 49 (a threat budget per depth, mixed waves, the next wave only after the last is dead).
- **Scale by composition and modifiers, not only raw stats.**
  - Elite affixes change how the player must position: a fire trail punishes standing still, a shield punishes
    burst, a healer punishes ignoring priority [analysis on Risk of Rain 2].
  - Mark elites visibly (size, name tag, aura) [wiki, Dead Cells].
  - Gungeon multiplies *returning* enemy HP per floor (reported ~×1.0 → ×2.1) but keeps **newly introduced** types
    at base HP [community]. Never make a new enemy a stat sponge too.
- **Spawn telegraph:** enemies appear after a short warning, never on top of the player.

## 3. Build variety (recipe 48)
- **Rarity tiers plus a synergy tier.** Hades uses Common → Rare → Epic → Heroic/Legendary, plus duo boons that
  need one boon from each of two sources [wiki]. → recipe 48 (`requires_tags`).
- **Conditional, build-shaping effects beat "+X% everything."** Minimising generic stat boosts is cited as why random
  pickups still feel like choices [analysis]. Give a **direction early** (the first boon or two) and reward
  reinforcing it [analysis].
- **Show the options, then choose** ("pre-action" randomness), for anything build-defining. Blind pickups that can
  ruin a run feel unfair [analysis]. Offering 3 is the genre norm (Hades; Risk of Rain 2's 3-item terminal
  [wiki]).
- **Small content × modifiers.** 6 weapons × 4 aspects gives ~24 playstyles [wiki]. Sidegrades that change
  playstyle count as variety too [wiki, Risk of Rain 2 void items].
- **Early picks must stay relevant late** [analysis].
- **Hunt dominant builds with data.** Slay the Spire's team used pick and win rates and targeted nerfs [dev]. In
  game-builder, recipe 36 simulates each boon's gain, and "no dominant boon" is a contract.
- **Soft bias is allowed.** Isaac's hidden item quality steers rerolls [wiki]. Rerolls are a resource for fishing
  out of bad luck [wiki].

## 4. Run structure (recipe 50)
- **Rooms per area:**
  - Hades: 4 areas, each ending in a boss, with low-to-mid teens of chambers in the first [wiki, exact digits
    unconfirmed];
  - Gungeon: 5 floors built from authored "flows" and a pool of ~300 rooms for floor 1 [dev];
  - Dead Cells: a fixed biome graph with procedurally assembled authored chunks [dev].

  Hand-made rooms arranged procedurally worked better than generating room contents [dev, Gungeon].
- **Show the reward type on the door** before committing (boon / currency / shop / rest / challenge) [wiki,
  Hades]. → recipe 50 (`RoomDoor.reward`).
- **Shops and rest:**
  - Hades' shop shows 3 items, is guaranteed after a boss and is absent from the first run [wiki];
  - rest rooms heal a percentage (not full) at fixed points [wiki].
  - → recipe 50 always offers a rest before the boss.
- **An optional risk branch:** pay a cost for a bonus, repeatable [wiki, Hades Chaos gates].
- **Timed rewards** as a nudge rather than a fail state [wiki, Dead Cells timed doors].

## 5. Meta progression (recipe 50)
- **Death is progress.** Hades was built to "take the sting" out of dying: story, relationships and permanent
  upgrades advance because you died [dev]. → recipe 50 banks **all** of the run's currency on death.
- **Options over raw power.**
  - Stat-only permanent upgrades make early runs feel unfairly hard and late runs trivial [community/analysis].
  - Every loss then feels like "an upgrade I haven't bought" [community].
  - Dead Cells' blueprints widen the *pool* of possible items instead of handing them over [wiki].

  Lean meta on new weapons, starting choices and rerolls.
- **Accessibility as small increments.** Hades' God Mode gives ~20% damage resistance, then +2% per death up to
  ~80% [dev]. It helps a stuck player without erasing the game.
- **Mastery modifiers.**
  - Many small, toggleable, ranked difficulty modifiers (Hades' Pact of Punishment, ~15) let mastered players set
    their own challenge [wiki].
  - In-fiction framing keeps immersion [analysis].
  - Hades II adds tougher variants to cleared areas [analysis].
- **Daily seeds** add replayable structure cheaply [analysis, Spelunky].

## 6. Bosses (recipe 51)
- **HP-threshold phases** that add moves or adds [community on Hades]. A phase with a rule damage can't bypass (an
  invulnerable add phase) makes fights more than DPS checks [community]. → recipe 51 stops overflow damage at a
  threshold and makes the transition invulnerable.
- **Windows of opportunity:** the gap after an attack is its own difficulty knob, separate from damage and HP
  [analysis]. → recipe 51 `min_window`.
- **Keep a move's visual language constant** as difficulty rises. Change timing, recovery and combinations instead
  [analysis]. → recipe 51 `validate()` (telegraph ≥ 0.4 s by default).
- **The arena is a second opponent:** cover, hazards, a shape change mid-fight [analysis].
- **Plan for mastery.** A fair first fight becomes a formality after many runs, so add harder variants or
  modifiers that change coordination [analysis].
- **Kill order in multi-boss fights** creates decisions [community].

## 7. Onboarding and freshness
- **No forced tutorial.** The first run is short and expected to end in death; the hub explains a little more each
  time; add an optional practice dummy [analysis/community]. This works only because failure is cheap and restart
  is fast [analysis].
- **A stable, learnable core with random surroundings.** Skill must transfer between runs [analysis].
- **Freshness comes from layers:** build variety, encounter variety and optional modifiers, not any one of them
  alone [analysis].

## 8. Pitfalls
- **Unwinnable runs from bad luck.** Test worst-case and best-case rolls deliberately [analysis]. In game-builder:
  simulations (36), level validation (37), and seeds everywhere so any run replays.
- Randomness stacked on randomness with no fairness backstop [analysis].
- Players blaming themselves for luck, or luck for themselves [analysis].
- Grindy, stat-based meta [community].
- Runs too long for the "one more try" loop [analysis].
- Unreadable screens: overlapping telegraphs, and effects hiding attacks [analysis].
- Too little build variety, so one solved strategy wins every time [analysis].

## Principles → game-builder parts
| Principle | Where it lives |
|---|---|
| Windup / active / recovery; buffer; dash-cancel only in recovery | recipe 47 (+ 43) |
| Rarity + synergy tier; show options then choose; seeded offers | recipe 48 |
| Threat budget, mixed waves, new types unlocked by depth, next wave only when clear | recipe 49 |
| Reward on the door, rest before the boss, no shop after a shop, death banks everything, rising upgrade costs | recipe 50 |
| Threshold phases that can't be skipped, invulnerable transition, readable telegraphs, windows to punish | recipe 51 |
| Damage over time and stat statuses through one stat system | recipe 52 (+ 48) |
| Hit-stop, flash, shake | recipes 32, 33, 03 |
| No dominant build; fairness at the extremes | recipes 36, 37 |
| Saves for meta progress | recipe 13 |

## Sources
Researched 2026-09-27. A claim-level list with URLs was compiled for this document; the main sources:
- **Developer:**
  - Game Developer Q&A on Enter the Gungeon;
  - "The Design Challenges of Children of Morta";
  - Slay the Spire's data-driven balancing;
  - Inverse's interview on Hades' God Mode;
  - Deepnight (Sébastien Bénard), "The Level Design of Dead Cells: A Hybrid Approach";
  - PC Gamer on Evil Empire rebuilding combat;
  - GDC Podcast ep. 16 with Greg Kasavin;
  - Nijman, "The Art of Screenshake" (2013);
  - BorisTheBrave, "Dungeon Generation in Enter the Gungeon".
- **Analysis:** Game Developer:
  - "I Hate Roguelikes, And So Should You!";
  - "The Eight Rules of Roguelike Design";
  - "Enemy Attacks and Telegraphing";
  - "Designing for Difficulty: Readability in ARPGs";
  - "Boss Fights Will Never Be The Same";
  - "The 24-hour ticket".
- **Analysis, other:**
  - thom.ee, "What makes or breaks agency in roguelikes";
  - parryeverything.com on Risk of Rain 2 elites;
  - Bugnet on boss arenas.
- **Wikis (community):** Hades, Risk of Rain 2, The Binding of Isaac, Dead Cells and Enter the Gungeon wikis (boons,
  difficulty, items, biomes, doors).

Game names are trademarks of their owners and are used only to identify the source of a design observation.
