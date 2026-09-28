# Genre: military FPS campaign (Call of Duty-like) — what makes it good

> Part of the gry-wiedza library (`wiedza/`), written for AI agents using the game-builder plugin. Skills and
> recipes named here are game-builder's; read this with `gb doc genre-military-fps`. Text: CC BY 4.0 (see
> LICENSE.md).

**What this is:** a reference for building an **original**, small single-player first-person shooter campaign
(20–60 minutes). That means:
- guns with learnable recoil, aiming down sights and reloads;
- enemies that take cover, peek, get pinned down and flank;
- regenerating health;
- linear missions paced as a string of combat arenas, quiet moments and set pieces.

It covers design principles and typical numbers from several games: the Call of Duty series, Halo, F.E.A.R.,
Half-Life 2, DOOM (2016), Titanfall 2, Wolfenstein: The New Order, Counter-Strike and Rainbow Six Siege.

**Never copy** their characters, names, story, maps, art, sounds or specific content. Mechanics and genre conventions
are free to use; expression isn't.

**Source quality**, marked on each claim:
- **[dev]**: a developer talk, interview, postmortem or blog;
- **[analysis]**: design journalism or criticism;
- **[wiki]**: community-documented numbers, not verified against code;
- **[community]**: forum or guide consensus, the lowest confidence;
- **[measured]**: measured by game-builder's own bot scenarios (its FPS template, 2026). It is one game and one bot,
  so it shows a mechanism, not a universal number.

The claims come from a researched list of 87 facts from 47 sources (2026-09-28); the main ones are in Sources.
Numbers are ranges to start from; the playtest decides. Where no reliable number exists, this document says so
(see "Not established") instead of guessing.

## The loop at three time scales
- **Seconds:** spot an enemy, aim, fire a burst, duck back when hurt, reload behind cover, re-peek.
- **Minutes:** clear an arena. Read it first (where is the cover, where will they come from), push through it,
  reach the next quiet moment and checkpoint.
- **A mission (10–20 min):** a string of arenas, quiet stretches and one or two set pieces, toward an objective the
  player always knows.

A useful model names four levers a designer turns scene by scene [analysis]:
- **movement impetus** (the urge to push on);
- **threat** (real danger);
- **tension** (felt or unknown danger);
- **tempo** (how fast the player must react).

Combat is high threat and tempo. Alternating it with low-tempo stretches prevents fatigue [analysis]. A scripted
sniper level is described as a strict cycle: guided movement, pauses to observe and plan, tense approaches, short
bursts of action. The player is never long without a new small event, and never long at full intensity
[analysis].

## 1. Gun feel (recipes 53, 54)
- **Recoil is a fixed, learnable pattern, not random.**
  - In Counter-Strike, learning each gun's spray pattern and pulling against it is a core skill [community].
  - Guns differ in kind: some kick straight up, others drift up and to the right. Pulling down against the kick
    beats not correcting, so corrected hip fire can beat uncorrected ADS [dev, Modern Warfare 2019].
  - → recipe 53: `recoil_pattern` is a list of kicks, repeated in the same order and reset after a pause.
- **The first shot is accurate.**
  - Counter-Strike's first shot after a pause is the most accurate. Accuracy drops through a spray and comes back
    after a short pause, which is why bursts beat full auto [community].
  - Rainbow Six Siege: the first ADS shot of most guns is 100% accurate [community].
  - → recipe 53: `first_shot_rest` and bloom that recovers while not firing.
- **Hip fire vs aiming down sights (ADS).** ADS clearly slows the player; hip fire is the fastest shot but clearly
  less accurate almost everywhere [dev, Modern Warfare 2019]. → recipe 53: `hip_spread`, `ads_spread`, `ads_time`,
  `ads_move_scale`.
- **Tune in modifiers.** Siege's muzzle attachments are quoted as ~45% less first-shot vertical kick, or ~45% less
  spray spread [community]. Attachments and upgrades are percentages of a base gun, not new guns.
- **Typical numbers** (CoD4, 2007) [wiki]:

  | Archetype | Damage near → far | Rate | Headshot |
  |---|---|---|---|
  | Assault rifle | 40 → 30 | 700 rpm (one fast rifle 1200) | × 1.4 |
  | Sniper rifle (bolt) | 70 | slow, limited by the bolt | × 1.5 |
  | Shotgun | pellets | — | × 1.0 (no bonus) |

  On 100 health a rifle kills in 3 body hits up close. Recipe 53's defaults are this rifle. Write time-to-kill into
  the Tuning table; it is the number the whole campaign is balanced around.
- **"Real, but not frustrating."** A weapons designer on a recent entry: guns should "feel like real weapons, but
  they shouldn't feel frustrating" [dev]. Realism serves fun.
- **Show the numbers the player builds around.** Modern Warfare (2019) shows rate of fire openly [dev].
- **Hit markers** exist for readability: in a fast fight you can't otherwise tell whether a shot landed. Grade them:
  a body hit, a headshot and a kill each get their own mark and sound [analysis]. → recipe 54 returns the zone.
- **Weapon sway and head bob** give the gun physical presence. Too much distracts; too little goes unnoticed. Scale
  sway to the look speed. Walking bobs in a gentle rhythm, sprinting with more amplitude [community].
- **Tracers** show the path of fire, so a shooter can walk shots onto a target [community]. A few at the end of a
  magazine warn that it is nearly empty.

## 2. Enemy AI (recipe 57, tokens from 49)
- **Readable beats clever.** Halo's AI was made predictable, not random. Enemies react to the player, have
  incomplete knowledge, and **show their inner state through dialogue, animation and where they look** [dev, GDC
  2002].
  - Each actor has its own perception (sight, sound, memory), so the player can really lose or fool it [dev].
- **Barks** ("There he is!", "Reloading!", "Grenade!") announce what an enemy is about to do. The player then reacts
  to intent instead of being surprised [analysis]. → recipe 57's `bark` signal.
- **Squads without chatter.** In F.E.A.R., soldiers don't talk to each other. Coordinated flanks come from agents
  sharing the same world state and getting squad-level goals [dev, Orkin, GDC 2006]. Other F.E.A.R. details [dev]:
  - each character runs only three states: go to, animate, use an object;
  - a planner (GOAP) picks from ~120 actions and ~70 goals;
  - plans are kept short (1–2 actions), so replanning is cheap.
- **Flank or fall back.** Ghost Recon: Future Soldier's AI always tries to flank the player; if it can't, it retreats
  to better cover [dev]. Halo 3's designer argued that **retreating** enemies make a fight more believable than
  enemies who fight mindlessly to the death [dev].
- **Grenades flush players out of cover** [wiki, Half-Life 2 with Valve's commentary]:
  - a soldier throws one to push the player out of cover, and announces it;
  - enemies near a grenade abandon what they're doing, including shooting, and run;
  - only one soldier per squad may throw at a time (a grenade "slot").

  A token with `limit = 1` per squad does this: recipe 49's `AttackTokens`.
- **Keep a distance band.** Half-Life 2's soldiers hold between a minimum and maximum distance from the player and
  prefer a good position near cover over charging [wiki]. Valve softened its more aggressive flush-out behaviour
  after playtests, because players struggled [wiki]. → recipe 57's `CoverFinder` band (`near` / `far`).
- **Limit simultaneous attackers.** DOOM (2016) changed demons from charging the player to holding position, and
  limited how many fight in melee at once, so the player faces one at a time rather than drowning in a crowd [dev].
  The equivalent for gunfire: at most 2–3 soldiers peek and fire at once (recipe 57 + 49 tokens).
- **Enemies should be there first.** Measured in game-builder's FPS template [measured]:
  - a first wave that spawned out of sight and ran 10+ m across open ground to its cover died before it fired; a whole
    mission produced 21 enemy shots, so the fights were target practice;
  - starting the first wave already crouched at cover hidden from the player ("dug in"), with later waves running in
    as reinforcements, gave real firefights (~75 enemy shots, the bot taking cover when hurt) at the same numbers.
- **Suppress on near misses, not only impacts** [measured, same template]: counting only where a bullet lands
  missed shots that passed close by and hit the wall behind. Measure the distance from the soldier to the bullet's
  path.
- **Mix archetypes:** patroller, flanker, rusher, turret, support, ambusher. Each puts a different pressure on the
  player; combining them forces changing tactics [analysis].
- **Difficulty levers:** AI accuracy, aggression, and the number and weapons of enemies [analysis]. Recipe 57 puts
  difficulty in `accuracy()` (a ramp from `accuracy_min` to `accuracy_max` over `aim_time`, × a difficulty scale),
  not in shorter warnings.

## 3. Health and survival (recipe 55)
- **Regenerating health:**
  - CoD4: above ~55 of 100, health comes back fully about **5 s** after the last hit [wiki];
  - later entries cut the delay from 4 to 3 s [wiki];
  - the delay is a pacing number, not a constant.

  Recipe 55 defaults to 4 s.
- **History:** Halo: CE had a regenerating shield over a fragile health pool that didn't regenerate. Halo 2 and 3
  regenerated fully, and ODST and Reach partly returned to health packs [analysis]. A `segment` in recipe 55 gives
  the in-between (regenerate only to the next quarter).
- **Show danger without a number.** Regen shooters pair it with a red vignette that grows as health drops [analysis].
  → recipe 55's `danger()`.
- **Show where damage came from.** A full-screen flash says "that hurt" but not "from where". Players missed threats
  right behind them [analysis]. Simple flat radial indicators read faster than elaborate 3D ones [analysis]; even a
  3D indicator failed when its shape wasn't readable at a glance [community]. → recipe 55's `DamageIndicators`.
- **Difficulty retunes several things at once** [analysis]:
  - enemy damage;
  - AI accuracy and aggression;
  - ammo and health availability;
  - checkpoint spacing.

  Halo 3's hardest difficulty did not simply multiply enemy health: each mission got its own changes [dev].
- **Checkpoints pace risk.** Dense checkpoints feel relaxed; sparse ones around a dangerous stretch say "slow down"
  [community]. → recipe 41.

## 4. Levels and encounters (recipes 49, 41, 19)
- **Prototype encounters cheap and many.** Titanfall 2's campaign was built from "action blocks" [dev]:
  - rough prototypes, days to a week each, with placeholder art;
  - one designer tests one idea for fun;
  - Respawn made ~100–200 and kept the strongest.

  Its most celebrated level, built around a unique mechanic, took one senior designer about a year [dev]. One
  gimmick per mission is plenty.
- **Pace and difficulty only show when the whole thing is assembled.** Half-Life 2 split the game between three
  near-independent design teams, and its pacing could only be judged at Alpha [dev]. In game-builder: the full-run
  bot scenario and the human playtest.
- **A quiet room before a fight.** Even DOOM and Quake open a new area with a short quiet room, to look around and
  test the controls [community]. Let the player read the arena first: sight lines to likely enemy positions,
  visible cover [community].
- **The door problem** [dev]. Players stop in the doorway between a corridor and an arena and turn the fight into a
  safe shooting gallery. Fixes:
  - cover closer to the arena's middle, as a foothold;
  - convex corners for peek-and-fire;
  - walls that split sight lines, so not every enemy is visible from the door;
  - AI leashed to positions that favour going in;
  - one-way drops or doors with no way back.
- **Corridors need breaks.** A long bare corridor is a bad fight. Add corners, pillars or wall offsets, so both sides
  can break line of sight [community].
- **Let the player choose how to fight** [dev, Wolfenstein: The New Order]:
  - the AI tracks whether the player has been spotted, so a player who hasn't fired can still sneak or flank
    mid-fight;
  - commanders call reinforcements at the start of a fight, and killing the commander first stops them. That is a
    designed incentive, not a fixed number of waves.
- **Linear by necessity.** CoD-style campaigns block alternative routes during a set piece, so the scripted trigger
  always fires the same way. Every extra valid entrance multiplies the encounter variants to build [analysis]. Big
  battle set pieces mix real, reactive soldiers in front with cheap fake ones far away [analysis].
- **Push-forward vs cover.** DOOM (2016) deliberately removed regenerating health tied to hiding. Health, armour and
  ammo drop from enemies instead, so arenas are built around constant movement [dev]. Its guiding motto ("make me
  think, make me move") was used to cut anything that didn't serve forward engagement [dev]. A cover shooter is the
  opposite choice; pick one per game.

## 5. Aim assist, controls, field of view (recipe 56)
- **Aim assist is two parts, pad only** [analysis]:
  - **slowdown**: the view turns slower when the crosshair crosses near a target;
  - **rotational assist or "magnetism"**: the view follows a moving target while the stick roughly tracks it.

  Halo gives each weapon its own magnetism radius, shrinking with zoom [wiki]. Halo: CE's approach became the model
  most console shooters followed [analysis]. Apex Legends and Fortnite use the same two-part pattern; their strengths
  are not published [analysis]. → recipe 56: slowdown and pull in a cone, only while the stick moves.
- **Why:** analogue sticks are less precise than a mouse, and assist keeps pad players effective at the same
  time-to-kill [analysis].
- **Field of view:**
  - console shooters historically defaulted to ~60–70° (the player sits far from the TV);
  - PC shooters default to ~90–100° (the monitor is close);
  - a narrow console FOV on PC is a known cause of discomfort and simulator sickness [wiki].

  Default to ~90° on PC and put a FOV slider in the settings.
- **Mouse:** most competitive players run 400 or 800 DPI [community]. Offer a sensitivity slider and read
  `screen_relative` in Godot (see game-builder's godot-pitfalls).

## 6. Readability and feedback
- **Enemy silhouettes:**
  - contrast with the environment matters more than the colour itself;
  - encode faction or threat on at least three channels: hue, value (light / dark) and shape. A colour-blind player
    then still reads it [analysis].
  - Put the brightest accents where the danger is (the chest and weapon) to speed up threat reading [analysis].
- **Hit markers graded** by body / head / kill, and **damage direction indicators** (§1, §3).
- **Footsteps** are among the most informative sounds and the easiest to lose under gunfire. Sound designers give
  them their own frequency band in the mix [community].
- **Telegraph grenades and charges** with a sound and a visual, early enough to react [analysis, wiki].

## 7. Pitfalls
- **Bullet sponges:** enemies hard only because they soak damage. The difficulty feels forced, not earned
  [analysis]. Make them harder by behaviour (flanks, grenades, suppression), not health.
- **Unfair spawns:** enemies appearing right behind the player, in a blind spot, or with no warning [community].
  Spawn at the point farthest from the player, with a minimum distance (no ambush) and a maximum (time to react)
  [community].
- **Overused scripting** makes combat a shooting gallery that doesn't react to the player [analysis].
- **Invisible damage:** a flash with no direction [analysis] (§3).
- **The door problem** (§4).
- **Everyone shooting at once** (§2, tokens).

## Principles → game-builder parts
| Principle | Where it lives |
|---|---|
| Rate without drift, magazine, tactical / empty reload, spread and bloom, first-shot accuracy, ADS, learnable recoil, falloff | recipe 53 |
| Spread → ray in the camera basis, the shooter excluded, head / body / limb zones | recipe 54 |
| Regenerating health with a delay, a danger effect, damage direction indicators | recipe 55 |
| Slowdown and pull for pads only, inside a cone, while the stick moves | recipe 56 |
| Cover that hides crouched and peeks standing, a distance band, suppression, flanks, barks, an accuracy ramp | recipe 57 |
| At most N soldiers firing at once; one grenade per squad | recipe 49 `AttackTokens` |
| Waves that come only when the last is gone | recipe 49 |
| Checkpoints | recipe 41 |
| Mission objectives the player always knows | recipe 19 (quests) |
| Screen shake on firing and hits | recipe 03 |

A whole mission built from these parts, with a bot that completes it: the `military-fps-3d` template (game-builder
0.25.0).

## Not established
The research looked for these and found no reliable open source. Don't quote numbers for them; tune in playtests.
- ADS times in milliseconds for named guns (sources say only "ADS slows you down").
- Hip-fire spread cone angles or formulas.
- How many F.E.A.R. soldiers may attack at once.
- An accuracy-ramp curve for any named game. The technique is standard, but no source gives numbers.
- Regeneration delays in Modern Warfare (2019) or Halo: Reach.
- CoD4 falloff distances in metres (the wiki gives damage near / far, not distances).
- Aim assist strengths in Apex Legends or Fortnite.
- Squad sizes and reinforcement timing in Wolfenstein: The New Order.
- DOOM Eternal's exact health / armour / ammo drops.
- Headshot multipliers and TTK for Halo or Titanfall 2.

Recipes 53–57 therefore use starting values marked as defaults, not sourced numbers (spread 3° hip / 0.3° ADS,
`ads_time` 0.22 s, accuracy 0.15 → 0.55 over 1.2 s).

## Sources
Researched 2026-09-28. The main sources:
- **Developer:**
  - Jeff Orkin, "Three States and a Plan: The A.I. of F.E.A.R." (GDC 2006), via Game Developer;
  - Damian Isla on Halo 3's encounter design and task system, via Game Developer ("Combat Evolved: The Encounter
    Design of Halo 3");
  - Chris Butcher and Jaime Griesemer, "Creating the Illusion of Intelligence" (GDC 2002);
  - Game Developer, "Flanking and Cover and Flee, Oh My!";
  - Game Developer, "The Door Problem of Combat Design";
  - Game Developer, "Pushing Push-Forward Combat with Gameplay" and "Make Me Think, Make Me Move" (DOOM 2016);
  - Game Developer, "Understanding Titanfall 2's Action Block Level Prototyping Process" and the "Effect and Cause"
    history;
  - Game Developer, "Classic Postmortem: The Making of Half-Life 2";
  - Game Developer Magazine Q&A, "How Halo 3 Got Legendary";
  - Activision blog, "The Basics of Call of Duty: Modern Warfare — Ready, Aim, Fire";
  - TechRadar interview with a Modern Warfare 4 weapons designer;
  - GameRevolution interview with Jens Matthies (Wolfenstein: The New Order).
- **Analysis:**
  - Game Developer, "Examining Game Pace: How Single-Player Levels Tick";
  - Game Developer, "Difficulty Is Difficult: Designing for Hard Modes in Games";
  - Kotaku, "Enough with the Red Screen of Almost Death";
  - GamesRadar, "Stop, Drop and Heal: A History of Regenerating Health";
  - Jasper Stephenson, "A UX Analysis of First-Person Shooter Damage Indicators";
  - Den of Geek on bullet sponges;
  - The Level Design Book (combat encounters, enemies);
  - Wikipedia, "Aim assist" and "Field of view in video games";
  - character readability in Team Fortress 2 and Overwatch (Medium).
- **Wikis (community):** Call of Duty Wiki (weapons, damage multipliers, health system), Halopedia (magnetism),
  Combine OverWiki (Half-Life 2 soldiers, paraphrasing Valve's developer commentary), Dexerto on regeneration
  changes.
- **Community:** Counter-Strike spray-pattern and recoil guides, Rainbow Six Siege Steam discussions, GameDev.net on
  weapon sway, World of Level Design on pacing beats, guides on spawn placement and footstep mixing, DPI statistics.

Game names are trademarks of their owners and are used only to identify the source of a design observation.
