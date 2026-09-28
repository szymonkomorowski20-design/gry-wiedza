# Genre: real-time strategy (Warcraft / StarCraft / Age of Empires-like) — what makes it good

> Part of the gry-wiedza library (`wiedza/`), written for AI agents using the game-builder plugin. Skills and
> recipes named here are game-builder's; read this with `gb doc genre-rts`. Text: CC BY 4.0 (see LICENSE.md).

**What this is:** a reference for building an **original**, small real-time strategy game: one player against a
computer opponent, skirmishes on a few maps and/or a short campaign of 3–5 missions, 20–60 minutes of play. That
means:
- selecting units and giving them orders;
- workers gathering resources into a stockpile, with a supply cap;
- buildings that produce units and unlock others;
- armies with counters;
- fog of war;
- an AI that builds, attacks and retreats.

It covers design principles and typical numbers from Warcraft II and III, StarCraft and StarCraft II, Age of Empires
and Age of Empires II, Command & Conquer, Company of Heroes and Supreme Commander.

**Never copy** their factions, units, heroes, names, story, maps, art or sounds. Mechanics and genre conventions are
free to use; expression isn't.

**Source quality**, marked on each claim:
- **[dev]**: a developer talk, interview, postmortem or blog;
- **[analysis]**: design journalism, criticism or academic work;
- **[wiki]**: community-documented numbers (Liquipedia, fandom wikis), not verified against code;
- **[community]**: forum or guide consensus, the lowest confidence.

The claims come from a researched list of 88 facts from 47 sources (2026-09-28). Many wiki numbers could only be read
from search snippets, because the wiki refused automated reads. The main sources are listed in Sources. Numbers are
ranges to start from; the playtest decides. Where no reliable number exists, this document says so (see "Not
established") instead of guessing.

## The loop at three time scales
- **Seconds:** select, order, react: a group ordered across the map, a hurt unit pulled back, a worker sent to
  build.
- **Minutes:** the macro round. Queue a unit in every building, place the next farm before supply runs out, send
  idle workers back, scout, then fight.
- **A match (15–30 min for a small game):** open with an economy, tech toward an army, expand, and win the decisive
  fights. A campaign mission replaces "win the fights" with its own goal: escort, defend, destroy.

The early game has two problems: finding out what the opponent does, and committing to a plan. A game that can be
lost to a rush in two or three minutes feels like a dice roll [analysis].

## 1. Hands: selection, orders, camera (recipes 58, 65)
- **Smart right-click.** Select with the left button. The same right-click is a move, an attack, a gather or a repair,
  depending on what is under the cursor [community, Warcraft III].
- **Attack-move vs move.** Attack-move walks to a point and fights whatever it meets. A plain move walks past enemies
  without reacting [wiki]. Both, and patrol, go back to Warcraft II (1995) [community]. Keep "move means move": it is
  how a player retreats.
- **Shift queues an order** after the current one, e.g. build a house, then go back to gathering [community].
- **Control groups:** Ctrl+number assigns, the number recalls. They go back to Command & Conquer (1995)
  [community].
- **Double-click** selects every unit of that type on screen [community].
- **Selection limits:** 12 in the original Warcraft III and StarCraft [community]; 24 after Warcraft III's 3.0 patch
  [dev]; 255, then 500, in StarCraft II [community, wiki]. A small modern game can drop the limit.
- **Rally points:** set on the ground or on a unit. A rally point on the army makes reinforcements follow the fight
  [community].
- **Hotkeys:** a "grid" layout, where keys map to fixed positions on the command card, cuts hunting for keys
  [community].
- **Camera:** edge scrolling, keys, and a minimap click that jumps the view there [community].

## 2. Economy (recipe 59)
- **Saturation is the economy's key number.** In StarCraft II two workers per mineral patch is the efficient point. A
  third waits for the patch and mines at about half the rate [wiki]. A base is fully saturated at 24 workers (3 × 8),
  but 16 is the practical optimum [community]. Two bases with 12 workers each out-earn one base with 24 [community].
  → recipe 59: `max_gatherers` per node, and `income_per_minute` to put in the balance sheet.
- **Walking time is income.** A worker walks to the nearest drop-off. A mill or town hall next to the food raises the
  real gathering rate [community]. In Age of Empires II an unupgraded villager gathering food right by a drop-off makes
  about 0.36 food/s; with every upgrade, about 0.49 [community].
- **Supply:**
  - StarCraft II caps it at 200; each supply building gives 8 [wiki];
  - Age of Empires II caps population at 200, and a house gives +5 for 25 wood [wiki].
- **Upkeep** (Warcraft III): gold income is taxed by army size — 0% up to 50 food, 30% from 51 to 80, 60% above 80 in
  the current version [wiki]. Gold from killing neutral monsters is untaxed [wiki]. It is a cheap lever against giant
  armies ("death balls"); take the mechanism, not the numbers.
- **The start:** StarCraft II went from 6 to 12 starting workers to shorten the slow opening [analysis], then back to 8
  in a 2026 update, to delay saturation and the first expansion [dev]. The number of starting workers sets how fast a
  match gets going.

## 3. Building and production (recipe 60)
- **The macro round:** visit every production building and queue one unit in each, so a round of units finishes
  together [community]. The UI should make this fast: control groups for buildings, a visible queue.
- **Build orders:** openings are known scripts, e.g. an early cavalry rush at population 21–22, or keeping the town
  centre producing villagers up to about 27 before spending elsewhere [community]. The AI's build order (recipe 64) is
  the same idea.
- **Scale check:** Age of Empires took 2–3 years, about 20 people and 220 000 lines of C++. The engine and the game
  logic were separate, and units and buildings were designed as database tables [dev]. Keep units and buildings as
  data from the first day.

## 4. Units and combat (recipe 63)
- **Armour as flat subtraction with a floor.** In StarCraft II armour subtracts a fixed amount per hit, and every
  attack deals at least 0.5 [wiki].
- **Bonus damage comes before armour.** StarCraft II adds bonuses against the target's attributes (light, armored…)
  before subtracting armour [wiki]. Spells ignore armour [wiki].
- **Counters by type.** Warcraft III crosses 7 attack types with 6 armour types in a table of multipliers: normal
  attacks deal 150% to medium armour and less to fortified; piercing does well against light and unarmoured and poorly
  against fortified [wiki]. → recipe 63: a type table, owned by the game's data; write the counter triangle as a
  contract test.
- **High ground:** in StarCraft an attack from low ground at a target on high ground misses about 47% of the time
  [wiki, community]. High ground also gives one-way sight: units below can't see up until something spots for them
  [wiki].
- **Micro:**
  - kiting (attack, step back during the cooldown, attack again) uses range against slower melee;
  - stutter-stepping chases a runner while still firing [community];
  - focus fire pays most against expensive, fragile or decisive targets [community].
- **Squads** (Company of Heroes): persistent squads of 1–10 soldiers the player grows attached to. Suppression pins
  infantry down instead of killing it. Vehicles ignore cover rules and can crush cover [analysis].
- **Balance goal:** StarCraft II's lead balance designer aimed for about 50% win rates between every pair of factions,
  and disliked matches where both sides only mass an army instead of fighting early [dev].

## 5. Movement and pathfinding (recipe 61)
- **Workers jam the economy.** In the original StarCraft, gatherers colliding on their way to and from minerals could
  stall a player's whole economy. The fix, under deadline, was to switch off collision between gatherers while they
  gather [dev]. → recipe 59/61: no avoidance between workers on the gathering loop.
- **Navigation in StarCraft II:** a navmesh from a constrained Delaunay triangulation of the terrain and buildings, A*
  with a funnel that respects the unit's radius, and local steering and collision avoidance on top [dev/community]. In
  Godot: `NavigationRegion3D` and `NavigationAgent3D` with avoidance on.
- **Crowds:**
  - Reynolds' boids steer by three local rules: separation, alignment, cohesion [dev];
  - Supreme Commander 2 replaced "wait until the conflict clears" with flow-field tiles plus hierarchical A* for long
    routes [dev].

  A small game rarely needs flow fields. Formation slots, a crossing-free assignment and an arrival rule (recipe 61) fix
  the classic "twenty units fighting over one point".
- **Scale costs.** Supreme Commander was built for maps up to 80×80 km and hundreds, even around 1000, units per
  player, and was among the first RTS to use many CPU cores [community]. Age of Empires had to run eight players on
  16 MB of RAM [dev]. Measure the heaviest fight early (`gb perf`).

## 6. Fog of war and scouting (recipe 62)
- **Three states.** Never-seen ground is black. Explored ground stays grey, showing terrain and buildings as last
  seen but no movement. Enemy units show only inside live sight [community].
- **Sight lingers** a moment after a unit dies or blinks away [community].
- **Scouting** is one of the early game's two central problems. A dedicated scout unit, like Age of Empires' starting
  scout, teaches and rewards scouting better than sending a worker [analysis].

## 7. The computer opponent (recipe 64)
- **Built from rules, not deep search.**
  - Age of Empires II's AI is a declarative rule script, e.g. "if in the first age and fewer than one barracks and can
    build one → build a barracks" [community].
  - Campaign AIs run build orders as ordered if-then lists checked a few times a second [community].
- **Attack waves.** A typical skirmish AI doesn't path toward the player opportunistically. It waits for an army size,
  picks a target and sends everything with one attack-move. Each wave is bigger and comes sooner, scaled by difficulty
  [community].
- **Difficulty is mostly resources.**
  - Warcraft III's melee AI reportedly runs the same logic on every level; its hardest level gets about twice the
    resources [community].
  - StarCraft II's hardest built-in AI gathers more per trip than a player can [community].
  - Critics note that an AI whose only weakness is total defeat takes away counter-play such as raids [community].

  → recipe 64 names its income multiplier openly and has a retreat, so raids and counter-attacks work.
- **Why it is hard:** RTS AI research calls the genre an unusually hard testbed: a huge state and action space,
  imperfect information (fog), real-time decisions and long-term economic planning [analysis]. Academic bot tournaments
  (AIIDE, CIG, SSCAIT) exist because of it [analysis]. A small game should not try to win there: rules, waves and
  honesty.

## 8. Missions, campaigns and maps
- **One new thing per mission.** Age of Empires II's tutorial campaign teaches the economy first, then early combat
  and production, then allies, then a first big battle with counters [community].
- **Mission types beyond "build and destroy":**
  - escort someone from A to B;
  - destroy N enemy strongholds;
  - defend for N minutes;
  - hero missions.

  Campaigns use these as distinct archetypes [community]. Warcraft III: The Frozen Throne was praised for leaving the
  standard "build a base and destroy the enemy" pattern [wiki].
- **Territory:** Company of Heroes makes the whole map matter from the first minute with control points, not a base
  that slowly grows [analysis].
- **Small maps for 1v1:**
  - a main base with its resources;
  - a natural expansion close by;
  - a choke point between them and the middle.

  (No sourced numbers for map sizes were found; tune in playtests.)

## 9. Readability and feedback
- **Silhouette and size first:** units should be told apart at a glance, not by tooltip [analysis]. Players had to zoom
  in to recognise units in one game, and critics name that a failure [analysis]. Give every unit a distinct role, and
  communicate it by its name and its shape [analysis].
- **Tooltips:** the role, then the mechanic in brief, then the numbers, then the weaknesses [analysis].
- **Health bars and team colour** above the unit; the selection circle at its feet, just above the ground
  [community].
- **Alerts:** "your base is under attack" with a key that jumps the camera to it; minimap pings in a colour that shows
  on black fog [community]. Broadcast overlays mark a drop on the minimap with a ping and an exclamation mark that
  follows the unit for about 5 s [community].
- **Unit responses:** short voice lines when selected or ordered are a genre convention. Some newer games have units
  talk to each other instead [analysis].

## 10. Pitfalls
- **APM walls:** professionals play at 300–500 actions a minute, with spikes past 800, and many of those actions
  are repeats [community]. A small game should reward decisions, not clicking: smart defaults, rally points, auto-cast.
- **The death ball:** everything clumped in one mass concentrates fire but invites area damage. It was one reason for
  StarCraft II's cool first reception among veterans [community]. Upkeep, area damage and multiple objectives spread
  armies out.
- **Economy stalls:** gatherers jamming (§5), supply blocks with no warning, idle workers nobody notices.
- **Early randomness:** a rush that ends a match in 2–3 minutes [analysis].
- **Unreadable fights:** units that look alike, no hit feedback, no alert when the base is attacked.
- **Cheating AI with no counterplay** (§7).

## 11. Measured in a skirmish [measured]
game-builder's `rts-3d` template (2026-09-28): one skirmish against the computer on a mirrored 72 m map, with
workers, gold and wood, farms, barracks and a stable, and footmen, archers and riders. A bot plays the player's side
with a counter-minded build order. One template and one bot, so these show mechanisms, not universal numbers.

- **A counter carried only by range fades as armies grow.** In the engine, 4 archers lost to 4 footmen of equal cost
  with arrows at × 1.75 against heavy armour, and won at × 2.0. A balance sheet (equal budgets, focus fire, the ranged
  side shooting alone while the melee closes the gap) showed × 2.0 was still not enough: archers won at 420 gold and
  lost at 720 and 1260. At 11 damage instead of 10 they keep 40–70% of their budget at every size, and in the engine
  2–4 of 4 archers are left. Riders against archers (0.89–1.0 kept) and
  footmen against riders (0.86–0.93) won by much more; an even triangle needs its own tuning pass.
- **A bonus must name a tag the target carries.** "+6 against light" never applied, because "light" was an armour
  type, not a tag. Test that each counter's bonus matches its prey.
- **The computer's failure modes** (each found by watching a bot game):
  - it never attacked, because its wave size had grown past its largest possible army;
  - it built farms at the supply ceiling;
  - its wave stood idle after winning a fight, because only idle units took new orders, so the attack has to be
    given again on every think;
  - it built a second barracks before the first was finished, because a step waiting for its requirement was skipped.
- **Workers:** a worker waiting at a full tree waited forever. Moving on after twice the gather time fixed it. Workers
  sent to the centre of a mine walked around to its far side, because the path ends at the nearest walkable point.
  Send them to the near side.
- **Speed with about 86 units in GDScript:** units without a target that looked for one every frame cost n² a frame.
  A look every 0.25 s, staggered per unit, fixed it. A fog of 1 m cells cost 3.2 ms an update; 2 m cells cost 1.1 ms.
  After both, the worst physics frame of each second was 8.9 ms at worst in a 40-against-40 battle, with a 1.5 ms
  average frame.
- **Group moves:** twelve footmen going around a rock's corner jammed there. A rule that stopped a unit after 4 s
  without progress left one 15 m from its place in the formation. Asking for a fresh path up to three times before
  stopping fixed it (6 of 6 runs).
- **Pace:** the computer's first wave reached the player's base by 3 minutes (normal difficulty). The bot beat it in
  6–16 simulated minutes; the long games were the ones where both sides ran short of gold.

## Principles → game-builder parts
| Principle | Where it lives |
|---|---|
| Click, box (units over buildings), double-click by type, control groups, smart right-click, shift queue, attack-move, patrol | recipe 58 |
| All-or-nothing costs, supply reserved at start and capped, saturation per resource node, the gathering loop, income per minute | recipe 59 |
| Placement grid with reasons, production queue paid when queued, supply-blocked once, tech tree that locks again | recipe 60 |
| The magic box, formation slots, crossing-free assignment, arrival (crowd rule), group speed | recipe 61 |
| Fog of war: unexplored / explored / visible, an overlay texture | recipe 62 |
| Damage with bonuses before armour, a type table, a damage floor; target priority; leash | recipe 63 |
| Skirmish AI: priority list, farms before supply blocks, waves that grow, retreat, honest difficulty | recipe 64 |
| Camera: edge / key / drag pan scaled by zoom, bounds, jump-to, the ground under the cursor | recipe 65 |
| Health | recipe 05 |
| Minimap | recipe 45 |
| Balance contracts (Monte-Carlo) | recipe 36 |
| Saves and settings | recipes 13, 17 |

## Not established
The research looked for these and found no reliable open source. Don't quote numbers for them; tune in playtests.
- Sight ranges of specific StarCraft II units, from a primary source.
- The high-ground miss chance for StarCraft II specifically, as opposed to the original StarCraft.
- Where the "smart right-click" term comes from.
- A postmortem or conference talk for Northgard or They Are Billions.
- The full content of the GDC 2011 talk "AI Navigation: It's Not a Solved Problem – Yet" (only its title and speakers
  are public).
- A developer talk about RTS UI readability (health bars, team colours, silhouettes) specifically.
- Which game first had double-click-to-select-the-type.
- Map sizes for small 1v1 maps.

## Sources
Researched 2026-09-28. The main sources:
- **Developer:**
  - Patrick Wyatt, "The StarCraft path-finding hack" (codeofhonor.com);
  - Game Developer, "Postmortem: Ensemble's Age of Empires";
  - Game Developer, "Inspired designs in Relic's RTS games" and "On Company of Heroes";
  - Elijah Emerson, "Crowd Pathfinding and Steering Using Flow Field Tiles" (Game AI Pro);
  - Craig Reynolds, "Boids" (red3d.com);
  - GDC Vault, "AI Navigation: It's Not a Solved Problem – Yet" (Anhalt, Kring, Sturtevant, 2011);
  - Blizzard game guides (buildings; simplified controls);
  - PCGamesN on StarCraft II's 2026 starting-worker change, and on David Kim's balance goals;
  - The Click on Warcraft III's 24-unit selection.
- **Analysis:**
  - Wayward Strategy, "Some thoughts about the early game phase of RTS" and "Unit design: clarity of roles and
    redundancy";
  - Terrancraft on starting worker counts and on micro trade-offs;
  - PC Gamer on Homeworld 3's unit chatter;
  - Ontañón et al., "A Survey of Real-Time Strategy Game AI Research and Competition in StarCraft" (IEEE TCIAIG, 2013);
  - Čertický and Churchill on StarCraft AI competitions (AIIDE).
- **Wikis:** Liquipedia StarCraft II (mining, damage calculation, armour, high ground, fog of war, sight, macro,
  patches) and Warcraft (upkeep); StarCraft fandom (attack-move); Age of Empires fandom (house); warcraft.wiki.gg
  (armour and attack types); Wikipedia.
- **Community:** Blizzard and Battle.net forums, GameFAQs, Team Liquid, Steam guides, AoK Heaven ("An Insight About
  Gathering"), the AoE II AI scripting reference, Hive Workshop, dev.to ("An RTS AI opponent that never pathfinds toward
  you"), TV Tropes, Namu wiki, the MIT Game Lab on StarCraft II notifications, Positech on selection outlines,
  Unreal Engine forums on RTS cameras.

Game names are trademarks of their owners and are used only to identify the source of a design observation.
