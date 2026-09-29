# Genre: stealth and parkour in a city (Assassin's Creed / Hitman / Splinter Cell-like) — what makes it good

> Part of the gry-wiedza library (`wiedza/`), written for AI agents using the game-builder plugin. Skills and
> recipes named here are game-builder's; read this with `gb doc genre-stealth-parkour`. Text: CC BY 4.0 (see
> LICENSE.md).

**What this is:** a reference for building an **original**, small third-person stealth-action game set in one city
district. It means:
- climbing buildings and running across roofs;
- guards who see and hear, search and give up;
- a crowd to hide in;
- a fight you can survive but should avoid;
- notoriety that follows you between contracts;
- viewpoints that reveal the district;
- contracts that end with a strike and an escape.

The scale is a vertical slice: a few blocks, a handful of contracts, 1–3 hours of play. The principles and typical
numbers come from the Assassin's Creed series, Hitman, Splinter Cell, Thief, Metal Gear Solid, The Last of Us, Mark
of the Ninja, Shadow Tactics, Dishonored, Mirror's Edge, Dying Light, Uncharted, Tomb Raider, Breath of the Wild,
Batman: Arkham, God of War, Ghost of Tsushima, Watch Dogs, GTA and Marvel's Spider-Man.

**Never copy** their characters, orders and brotherhoods, names, story, cities as they drew them, art or sounds.
Mechanics and genre conventions are free to use; expression isn't.

**Source quality**, marked on each claim:
- **[dev]**: a developer talk, interview, postmortem, blog, manual or patent;
- **[analysis]**: design journalism, criticism or academic work;
- **[wiki]**: community-documented rules and numbers (fandom wikis), not verified against code;
- **[community]**: forum or guide consensus, the lowest confidence.

The claims come from five researched lists of 173 facts (2026-09-28): climbing, perception and stealth,
counter-based melee, crowds, and the open world with its missions. Many fandom wikis refused automated reads and
were read through the Wayback Machine. Numbers are ranges to start from; the playtest decides. Where no reliable
number exists, this document says so (see "Not established") instead of guessing. **No shipped game in these lists
publishes its cone angles or climbing distances, and only The Last of Us gives a detection time.** Every number of
that kind in a game-builder recipe is a starting value to tune, not a quote.

## The loop at three time scales
- **Seconds:** move, read a guard, pick a route (roof, street or crowd), react to a filling awareness meter.
- **Minutes, one contract:**
  - climb a viewpoint and look;
  - choose an approach;
  - reach the target and strike;
  - escape and vanish.

  Viewpoint → synchronise → a leap into the hay is a flow loop: a clear goal and an instant reward, the nearby
  tasks revealed [dev].
- **A session:** district by district, with notoriety carried from one contract to the next (§8).

Detection is where the game starts to be interesting, not where it ends. The designer of Third Eye Crime stresses
that the fun happens after detection, not before it [dev]. The creative director of Assassin's Creed Unity called
detection the fail state of stealth, one that usually means combat, and built ways to regain control and restart
the stealth loop [dev]. Assassin's Creed Origins dropped detection and leaving an area as mission failures [dev].

## 1. Moving and climbing (recipes 66, 67)
- **Handholds from geometry.** In the first Assassin's Creed anything that stuck out about 10 cm could be a hand- or
  foothold [dev, GDC 2006]. Its controls mapped buttons to body parts, and a held "intensity" (a profile) chose
  the action [dev].
- **Sticky or free: the core trade-off.**
  - The first game was deliberately sticky: jumps and grabs were assisted, and the architecture was laid out as
    highways [analysis].
  - inFAMOUS's first fence climbing was so sticky it did not do what the player wanted, and it lacked horizontal
    flow. The sequel rebuilt it to be more fluid [dev].
  - Players of Assassin's Creed Unity missed the manual ledge grabs and wall jumps of the earlier games:
    smoothness had won over responsiveness [community].
  - Assassin's Creed Shadows splits intent in two [dev]:
    - **up** is "high profile", and its climbs, jumps and landings make noise;
    - **down**, pressed without a direction, drops and grabs the ledge; with a direction, it is an acrobatic
      descent.

    Crouching was decoupled from parkour so players stopped running off roofs by accident. A drop from a damaging
    height ends in a ledge hang when one is in reach.

  → recipe 66 gives separate up and down intents and stops at an edge unless asked to go over.
- **Where you may climb.**
  - Assassin's Creed Shadows allows climbing only on surfaces with real handholds. This gave deliberate "parkour
    highways" and control over where each character can go; its more agile character always jumps farther and
    reaches higher [dev].
  - Origins let you climb almost any surface [analysis]. Breath of the Wild's free climbing, limited by stamina, won
    its producers over in an early demo [dev].

  For a small game: put climbable surfaces on their own physics layer and make them read (§12).
- **Finding a ledge without markup.**
  - A patent for grabbing ledges without markup (Bungie/Sony, granted 2024) takes:
    - a wall at about 80–100° to the movement;
    - a top plane at about 85–95° to the wall;
    - a height within a per-character range, with clearance above the floor;
    - a recess deep enough for the character's width.

    Different characters grab different ledges [dev].
  - A Breath of the Wild-style climber rebuilt in Unreal (one developer's values) [dev]:
    - sweeps a capsule forward every frame (radius 0.5 m, half-height 0.72 m) and averages the hit normals;
    - enters climbing only within 25° of facing the wall;
    - finds the top of a wall as "nothing at eye height" plus a trace down of 2.5 m;
    - keeps 0.45 m from the wall and climbs at most 1.2 m/s.
  - Dying Light needed more than 200 ray casts a frame for ledge detection, cast in parallel groups [dev]. Its
    sequel detects ledges live on thousands of objects; moving and breakable objects were the hardest [dev].
  - In Godot, `ShapeCast3D` sweeps a shape and returns many hits (32 by default) but costs more than a `RayCast3D`
    [dev].

  → recipe 67: a ledge probe (forward ray at chest height, the wall's angle, a downward ray for the top, a clearance
  check) as a pure function with unit tests, and a climb state machine: hang, shimmy, climb up, drop, jump to the
  next ledge.
- **Jump assists.** Dying Light's first-person jumps needed three assist algorithms, because players jump too early
  or too late [dev]. Celeste's code has 0.1 s of coyote time [dev]; recipe 66 buffers jumps the same way.
- **Animation budget.**
  - Assassin's Creed III had about 280 climbing animations against 3200 for combat, with IK on hands and feet always
    on [dev].
  - Uncharted 4 used IK on all four limbs, and its feet seek edges [dev].
  - Dying Light 2 has about 3000 parkour animations [dev].

  A small game gets by with a handful of clips (hang, shimmy, climb up, vault, drop) moved onto the ledge in code.
  Unreal's motion warping bends root motion onto a world target for vaults and mantles [dev]. One reported bug
  lifted a character to 1 m on any standing mantle onto something lower than 1 m [community], so test several
  mantle heights.
  Godot 4.6 brought IK back as a family of nodes (`TwoBoneIK3D`, `FABRIK3D`, `CCDIK3D` and others) on
  `SkeletonModifier3D` [dev].
- **Stamina and falls.**
  - Dying Light 2 removed the stamina cost of parkour (except dashes) in a 2025 patch, so that you can escape a
    fight on low stamina [dev].
  - Breath of the Wild cut resting on a weapon stabbed into a wall [dev].
  - Uncharted 4 tested stamina and free climbing, then simplified them [dev].
  - Assassin's Creed Odyssey has no death from falling [analysis], and a Kotaku critic calls fall damage mostly
    realism and an artificial barrier [analysis]. Physicists estimated a hay cart cushions a fall of about 13 m
    [analysis].
  - Classic Tomb Raider, in its own units ("clicks", four to a floor square) [wiki]:
    - a step up is 1 click, and a grab reaches 7;
    - a standing jump covers 2 squares, a running jump 3;
    - falls are safe or deadly at 8 / 17 clicks after a jump, 10 / 18 from a drop and 12 / 21 from a hang.

  → recipe 66: a fall rule with named thresholds (no damage, damage, death), and soft landings (hay, water) that
  ignore it. No climbing stamina by default.
- **Slow climbs build scale.** Climbing a cathedral takes minutes even by the fastest route, and that is part of why
  the city feels big [analysis]. Prince of Persia: The Sands of Time made frequent deaths in 3D acrobatics bearable by
  rewinding time [dev].

## 2. The camera (recipe 40, with the traversal rules in 66)
- **Show where the player is going, not only the avatar.**
  - pull the camera behind when running;
  - a side view helps judge vertical distances, a top view horizontal ones;
  - tilt down at a cliff edge;
  - in a jump, look at the landing;
  - when obstacle avoidance fights the player's intent, the intent wins.

  [dev, "50 Game Camera Mistakes", GDC 2014]
- **Fights with a close camera need help** (§11):
  - enemies behind the camera hold back;
  - off-screen attacks are shown around the character [dev, God of War].

## 3. Seeing (recipe 68)
- **Not a plain cone.** A cone widens with distance, so it sees too much far away and too little up close.
  - Splinter Cell: Conviction used a box far away. Blacklist used a "coffin" that widens like a cone and then
    narrows, plus a narrow fast cone in front and a peripheral zone. The detection time range comes from the most
    inclusive shape the player stands in [dev].
  - Uncharted's cone let a guard right beside the player miss him while a far one saw him, so The Last of Us made
    its view angle inversely proportional to distance [dev].
  - Thief uses an ordered set of cones, each with its own angles, length and acuity; the first cone that contains the
    player counts [dev].
  - Shadow Tactics uses sharp zones, not a gradient: a zone you can cross crouching and a zone that is practically
    forbidden. Cone size, turn angles and speed are identical for every guard and every difficulty [dev].
- **What is tested.**
  - The Last of Us tests one point: the chest in stealth, the top of the head in combat. Its earlier weighted rays to
    several joints (about 60% needed) felt unpredictable to players [dev].
  - Blacklist casts rays to 8 bones, and how many must be visible depends on stance [dev].

  → recipe 68: one or two test points, so the player can predict the result.
- **The timer, not an instant check.**
  - The Last of Us: the timer rises every frame the guard sees the player and falls every frame it doesn't. About
    1–2 s for a typical guard, much less in combat, more before the guard has ever seen the player [dev].
  - Blacklist: the time scales linearly with distance inside the shape, and with the player's lighting and the guard's
    state. Inside a shape, detection comes within a few seconds; 1 cm outside, never [dev].
  - Assassin's Creed II: the fill speed depends on the guard type, and running speeds it up [wiki].
- **Light.**
  - Thief combines lighting, movement and exposure (each 0–1). It measures light at the floor under the player, so
    the player can judge their own safety [dev].
  - Mark of the Ninja makes light binary instead of a meter: hidden is drawn black and red, visible in full colour
    [dev].
  - Dishonored's cones lose effect in darkness and with distance [dev].
  - Shadow Tactics has smaller cones at night, but light always makes a bright zone [dev].
- **Difficulty.**
  - Blacklist tuned cone size and shape per difficulty, with more blind spots on easy and sharper hearing on hard
    [analysis].
  - Shadow Tactics kept cones the same on every difficulty [dev].

  Pick one and say which in the settings.

## 4. Hearing and the world's changes (recipe 68)
- **Hearing follows the level, not a circle.**
  - Mark of the Ninja: a guard hears a noise only if it is inside its radius **and** a path through the level's empty
    space connects them. A guard inside the radius without a path hears nothing [dev].
  - Blacklist measures distance over a graph of rooms and openings (doors, windows) [dev].
  - Halving hearing, for some events, for guards off screen and far away made Blacklist feel better at once.
    Halving every sound was rejected, because with instant takedowns you could sprint behind everyone [dev].

  → recipe 68: noise events with a radius measured along the navigation path.
- **Noise sources:** Assassin's Creed Shadows' high-profile climbing, jumping and landing make noise [dev]. Mark of
  the Ninja draws every noise enemies can hear as a ring of its exact range [dev].
- **Changes in the world are stimuli.**
  - A door left open or a light put out becomes an event with a lifetime.
  - The first guard who witnesses it claims it and checks it, with a clear animation and line.
  - Blacklist called it the system with the best effect for its cost [dev].
  - It also remembers how long ago the change happened: a light out for 5 minutes is not one out for 5 seconds
    [analysis].

## 5. Awareness, search and giving up (recipe 69)
- **A few clear states.**
  - Metal Gear Solid:
    1. infiltration;
    2. alert (support called, attack);
    3. evasion (guards leave their routes and search; being seen again means alert);
    4. back to infiltration when the counter runs out.

    Metal Gear Solid 2 added caution, a patrol on raised readiness until its gauge empties [dev, manuals].
  - The first Assassin's Creed shows the player's status [wiki]:
    - anonymous;
    - exposed: fight or flee;
    - unseen: line of sight broken;
    - vanishing: after a few seconds guards check the last seen position and give up if it is empty;
    - vanished: in a hiding spot.
  - Thief: awareness rises through a time filter and may skip states, but falls slowly through every state [dev].
  - Blacklist's meter is in practice two states plus an "I'll go and check" step at some percentage [dev].
- **Honest knowledge.**
  - In The Last of Us guards don't cheat about the player's position. Whoever sees him records a position and time
    and shares it with everyone. While nobody sees him it is not updated [dev].
  - After losing the target, a guard "knows" its position for about 2–3 s more: a trick from Halo, Crysis and
    Crackdown [dev].
- **Who reacts.**
  - Mark of the Ninja: one guard notices, so it checks. When several notice, one stays as the sentry who sends
    others, one or more investigate, and the rest stand by. The player can pull groups apart [dev].
  - The Last of Us sends a single investigator to a distraction [dev].
  - Two kinds of search [dev, Game AI Pro 2]:
    - cautious: a distraction with no known culprit. One guard walks there and stops after checking the spot, so the
      player can lure guards away one at a time;
    - aggressive: the enemy is known. Guards run, and stop after every point is checked or a time limit; at most 2–3
      search at once.
- **Where to search.**
  - A coordinator builds points from cover not visible from the estimated position, plus corners and alleys from the
    navigation mesh. Every 1–2 s each searcher checks line of sight to the unchecked points in view and ticks them
    off.
  - The score mixes distance from the estimate and from the searcher, with a slight pull toward the true position. A
    strong pull would be unfair.
  - After the search, guards return to their work gradually, not all at once [dev].
  - An occupancy map spreads the player's possible position over a grid, blurs it over time and clears cells that
    guards can see. The result is a methodical search with no script [dev, Third Eye Crime].
- **Keep search cycles short.** In The Last of Us one chosen guard went to check after 10 s without contact, and a
  fight → search cycle averaged almost 2 minutes. A "cheat" cut it to about 30 s: if the player moves more than 5 m
  from the suspected spot, the guard goes at once [dev].
- **Priorities.** Mark of the Ninja ranks about 60 kinds of stimulus source [dev]:

  | Stimulus | Priority |
  |---|---|
  | a damaged object | 1 |
  | a missing companion | 2 |
  | a suspicious silhouette, smoke, a body, a noise | 4 |
  | a box, a mine | 5 |
  | a distraction flare | 10 |
  | terror | 20 |

  On equal priority the newest wins, and a guard holds one stimulus at a time. The player's "suspicious silhouette"
  is seen from farther than the player, so it draws a guard to check instead of shoot [dev].
- **Social awareness** [dev, Blacklist]:
  - Two guards chatting shrug off the first small event and check the second together.
  - When one dies quietly, the other goes to look after a while.
  - The "vanished companion" check: if guard A heard guard B for 10 s and B then stays silent for 5 s, A
    investigates (with a long cooldown).
  - A guard who finds a body mid-search calls for help; in the middle of a fight it ignores bodies.
- **No level-wide cascades.**
  - Thief limits how far knowledge spreads between guards [dev].
  - In Metal Gear Solid V the rest learn by a shout or the radio. Silencing the guard who spotted you, in a short
    slow-motion window, keeps them from learning [dev].
- **The player guards can't reach.** A roof is the classic case, and it gets worse when the player has moves the AI
  doesn't [dev, Blacklist]:
  - Blacklist's guards comment, and one throws a grenade under covering fire.
  - With losses they retreat. This stops exploits but frustrates unless it is announced.
  - When the player vanishes they spread out to search.

  Assassin's Creed Mirage adds archers on the roofs at its second notoriety level [community]. A parkour game has to
  answer this in its own design, e.g. with rooftop guards, ladders, or searching at the bottom.

## 6. The crowd and hiding spots (recipe 70)
- **Hiding in plain sight** [wiki]:
  - The first Assassin's Creed: groups of scholars (slow, but safe through guarded gates), benches only when two
    civilians sit on them, haystacks and rooftop gardens.
  - Assassin's Creed II: hay carts, piles of leaves, water, any crowd, and hired companions as moving cover. You can
    leave a hiding spot at any time, and some guards search them.
  - Assassin's Creed III: blend into any group of at least two civilians, and strike from it.
- **Pushing through.** A gentle push draws no attention but is slow in a dense crowd. Shoving is faster but draws
  attention, and some people push back. Knocking into a porter who drops a crate near guards raises notoriety
  [wiki].
- **The player must believe it.** The first game's director said social stealth faded from the series because it
  is hard to make the player believe they are hidden. The crowd has to be rendered, and the player has to understand
  it [dev]. → show a "blended" state explicitly (§12).
- **Disguises (Hitman, 2016–2021).** Only chosen people see through a disguise ("enforcers": supervisors,
  bodyguards, some targets) [wiki]. Standing in a crowd hides the player [wiki]. Hitman 2 added hiding in crowds and
  foliage [dev].

## 7. Crowds: behaviour and cost (recipe 70)
- **Origins and scale.**
  - The first Assassin's Creed had a crowd of about 100–120, which the previous console generation could not hold
    (6–7 characters on screen in Sands of Time) [dev].
  - Early on, a crowd member was a path, an animation and one reaction, e.g. flee when the player climbs. People
    who fled ran far away and the game spawned new ones; if you followed one, they ran forever [dev].
  - Crowd bodies were assembled from heads, hair and upper and lower halves, with a sheet per district for poorer
    and richer streets [dev].
- **Steer by speed** [dev, Hitman: Absolution]:
  - The biggest lesson: people slow down rather than turn, and stopping looks better than a sharp change of
    direction.
  - Moods only get worse from stimuli: ambient < alert < scared < panic < dead.
  - A player's action creates up to three zones (sphere or cone) that push the mood in them.
  - A panicked crowd leaves the area by its exits and never gets in the player's way.
  - Narrow places need hand-placed hints, because shortest paths jam at corners.
- **A reaction has four phases** [dev, Watch Dogs 2]:
  1. a short reaction (posture, glance, shout);
  2. moving to a sensible distance and angle;
  3. the main behaviour for some seconds, or until the cause is gone;
  4. calming down and going back.

  Outcomes are weighted (ignore, watch, fight, flee). Watch Dogs 2's lessons:
  - proportions per population beat pure randomness;
  - cooldowns keep emotions from jumping between extremes;
  - the crowd must be neither over- nor under-reactive;
  - such systems degenerate quickly, so they must stabilise themselves.
- **Don't cheat where the player can see.** Cyberpunk 2077 at launch deleted stopped cars and fleeing people when
  the player looked away. Tom's Hardware named its unresponsive AI one of the launch's most visible problems
  [analysis].
- **Level of detail is the budget** [dev, Assassin's Creed Unity]. Unity's crowd ran at three levels by distance:
  - over 40 m: cheap meshes with no game entity, only basic reactions, about 25 µs each;
  - 12–40 m: a real character's look with cheap logic;
  - under 12 m: full AI and physics, at most 40 at once.

  Unity was bound by the CPU cost of AI and characters on screen, not by graphics [dev]. Players still found its
  level-of-detail switching distracting years later [community].
- **Lanes and slots.**
  - Unreal's City Sample walks its crowd on a hand-drawn network of lanes [dev].
  - Unreal's "smart objects" (a bench, a stall) hold everything about their use, with slots that are reserved and
    then occupied [dev].
  - Watch Dogs 2's "attractors" (activities at hand-placed objects) are a similar idea [dev].
- **Godot 4.7** [dev, documentation]:
  - A `MultiMesh` draws huge numbers of objects but has no per-instance culling, so use several per area. Animation
    in the vertex shader gives thousands of moving objects; skeletons run on the CPU, so thousands of skeletons are
    impossible.
  - RVO avoidance is expensive with many agents; turn it on only where needed. Spread path requests over time.
  - Visibility ranges swap or hide meshes by distance.
  - `VisibleOnScreenEnabler3D` stops processing off screen.
  - `AnimationMixer` in manual mode advances only when told. Using it as an animation level of detail is the
    researcher's inference, not documentation.

  → recipe 70: tens of agents on lanes, full animation only near the camera, fewer updates far away.

## 8. Notoriety and the wanted state (recipe 72)
- **Notoriety as a level** [wiki]:
  - Assassin's Creed II raised it for fights, kills, theft, being seen in a restricted area, bumping a standing guard,
    or tearing down a poster in view.
  - It fell with actions: a poster −25%, bribing a herald −50%, killing an official −75%.
  - Full, guards attack almost at once; empty, they ignore you.
  - Assassin's Creed III had three levels:
    1. guards notice you but turn hostile only if you linger or break the law;
    2. they approach and attack after a moment;
    3. they attack on sight, hunters search actively, and bells ring.
- **Mirage** [community]:
  1. civilians recognise the hero and call guards;
  2. archers appear on the roofs;
  3. an elite hunter comes too.

  A poster takes one level off. A herald or beating the hunter resets it all.
- **The alarm after a strike.** In the first game, exposing yourself to the target or killing it raised a city alarm:
  bells rang and everyone attacked on sight. It lasted until you got back to a safe place unseen [wiki].
- **Escaping.**
  - GTA IV leaves a search circle where the player was last seen. Leaving it for a few seconds ends the chase; at one
    star it spans about two blocks [wiki].
  - Assassin's Creed II's orange circle works the same way: outside it you escape more easily even without a hiding
    spot [wiki].
  - GTA V drops the circle and gives each officer their own view, shown as cones on the radar [wiki].
  - Watch Dogs [wiki]:
    - a witness phones the police, with a visible counter, and can be stopped;
    - killing the witness usually brings more callers;
    - heat falls gradually while you commit no crimes.

  → recipe 72: a level with named effects, witnessed acts that raise it, a search circle at the last seen
  position, and actions and time that lower it.

## 9. The district, viewpoints and contracts (recipe 73)
- **Size.**
  - Fans measured the series' cities (Ubisoft hasn't confirmed the sizes) [community]:
    - the first game's Damascus: about 0.13 km²;
    - Florence and Venice: 0.30–0.37 km²;
    - Rome: 1.4 km²;
    - Unity's Paris: about 2.4 km².
  - Mirage, a deliberately smaller game, has four districts and a 15–20-hour campaign [wiki].
  - Syndicate put London's landmarks roughly where they stand but shortened the distances between them [dev].

  A district a few hundred metres across is on the scale of the first game's Damascus.
- **Density makes the roofs work.** Mirage's designers added "highways" over flat roofs to cross the city fast. Its
  director calls the city's density and a big crowd the key to fast movement over roofs [dev].
- **Viewpoints.**
  - Early in the first game's development, quests unlocked one at a time, by talking to people hidden outside the
    cities. Synchronising at a viewpoint replaced that: it unlocks every nearby task at once. A clear goal and a
    challenge give an instant, large reward for a little effort [dev].
  - A viewpoint is a cheap source of value [analysis]:
    - a landmark to find your way by;
    - the nearby icons revealed;
    - content in portions (100 icons at once overwhelm; ten times ten is digestible).

    It doesn't have to be a tower; what counts is an unusual act tied to revealing the map.
  - From a viewpoint, the first game showed the next viewpoints and the places worth a visit [analysis].
  - Later games changed its job:
    - in Origins the points reveal nearby places and serve fast travel [wiki];
    - in Shadows they become fast-travel points and, instead of revealing the map, only mark nearby places with a
      "?" [community].
  - Far Cry 5 dropped towers and the minimap, because players had fallen into a rhythm where only a tower told them
    about a region [dev].
  - Breath of the Wild's towers first made play linear, and were moved to encourage straying [analysis].

  → recipe 73: a viewpoint reveals the markers within its radius and becomes a fast-travel point.
- **Contracts: from a line to an area.**
  - The first game had 9 targets in 3 cities. Before each kill came a few investigations (eavesdropping,
    interrogation, pickpocketing, tasks for informers) out of 6 per target. Doing all six reportedly revealed escape
    routes, guard posts and the target's movements [wiki].
    - Repeating the same procedure nine times drew complaints of monotony [analysis].
    - Its side activities were added by 4–5 people in about 5 days, just before the game shipped [dev].
  - Unity's "black box" missions let the player find the ways in and the helpful diversions [wiki].
  - Mirage has three phases: guided at first, then an open city with investigations in any order, then narrowing
    again before the finale. One investigation board ties it together [dev].
  - Hitman designs missions from areas, "thinking in circles, or volumes, or areas, rather than in a line" (Toke
    Krainert, IO Interactive). It starts from the targets and the spaces they occupy [dev].
    - About a dozen guided and unguided stories share each map. The best ones open other parts of the map [dev].
    - Guidance comes from dialogue, light that catches the eye, and sound [dev].
    - Levels hold about 300 characters, each with a routine. Overheard conversations tell where the target will be
      [wiki].
- **Keep a target's routine short.** In Hitman's Sapienza, testers were bored waiting for a target's loop through the
  town. Both targets' loops were shortened and kept inside the mansion [dev].
- **Mission rules**, drawn from Assassin's Creed III [analysis]:
  - place a marker instead of forcing a route;
  - characters adapt to the player, not the other way round;
  - optional objectives must not dictate the style of play;
  - fail only as a last resort. Detection should change the situation, as when a fleeing target becomes a chase,
    not end the mission, as its tailing mission did.
- **Distance rules.** Origins' guideline for all its studios [dev]:
  - a quest that leads you on goes at most 1000 m from its giver, and one inside a hub at most 500 m;
  - at most one "kill everyone" quest per hub.

  Scale them down for a district.
- **Teach the sandbox.** Hitman's first level was fun but hard to learn, and players couldn't grasp its scale. IO
  Interactive added a linear guidance system and a prologue [dev]:
  1. arrival;
  2. training: a real sandbox mission with strong guidance;
  3. a test: a small sandbox with no help.
- **Plausible places.**
  - Arkane asks how a guard gets to work, and rejects layouts where someone would walk a mile and climb ten floors.
  - Every backstage area of its Clockwork Mansion is visually connected to the big halls, so players don't get lost
    [dev].
  - Testers obeyed characters who forbade entry and got stuck, so hints were added. Exploits testers found were built
    into the levels instead of blocked [wiki].

  → recipe 73: a target routine as a short loop of stops with waits, and a contract in phases (reach, strike,
  escape) where detection changes the phase instead of failing the contract.
- **Guidance without a screen full of icons.**
  - The first game guided without a HUD [analysis]:
    - investigations gave lists and maps of guard posts;
    - important people stood at the centre of spaces;
    - you heard about the target in the street;
    - a special vision highlighted enemies, targets, allies and informants.
  - Ghost of Tsushima's wind points the way without UI, and a bird leads to a nearby secret. Its developers later
    admitted the wind was criticised as too linear [dev].
  - Origins replaced the minimap with a compass [wiki]. Odyssey offers a guided mode (waypoints) and an exploration
    mode (hints only) [wiki].
  - Breath of the Wild's "triangle rule" [dev]:
    - a rise gives a choice (over or around) and hides what is behind it;
    - large triangles are landmarks, medium ones hide things, small ones set the pace.

    Buildings of different importance "pull" the player in different directions. After changes, the playtest
    heatmap spread out from a few paths.
  - Avoid straight paths from which the whole goal is visible [analysis].
- **Godot.**
  - A third-person game stays precise in single precision within about 4–8 km of the origin. A walkable area up to
    8192 × 8192 m usually needs no large-world coordinates [dev].
  - Visibility ranges give distant buildings a cheaper stand-in [dev].
  - The documentation does not describe open-world streaming [dev].

  One district fits in one scene.

## 10. Level design for stealth
- **The illusion of a well-guarded place** the player slips through by finding gaps. The level's tools [dev, GDC
  2006]:
  - a rhythm of zones friendly and hostile to stealth;
  - safe places to scout from;
  - patrols that open time windows (a guard who stands still gives none);
  - a design for each phase: undetected, suspected, wanted.

  An escape needs loops, not dead ends.
- **Sharp rules make routes.** Shadow Tactics' crouch zone, and the fact that every guard has the same cone, let
  players plan [dev].
- **Many ways in, each one plausible** (§9). Dishonored can be finished without killing anyone, targets included
  [wiki].

## 11. When found: counter-based melee (recipe 71)
- **Defence alone made fights static.**
  - From 2007 to 2011 Assassin's Creed fights were won almost entirely by defence: enemies usually attacked one at
    a time, and a one-button counter won [analysis].
  - Brotherhood added execution streaks, making initiative the stronger play [wiki].
  - Players called the counter an absolute weapon: fights came down to waiting for an attack [community].
- **Harder fights give stealth meaning.** Assassin's Creed Unity removed automatic counters. The reason: if fighting
  is the path of least resistance, every mission ends in a fight [dev]. Its later games moved on:
  - Origins: hitboxes instead of paired animations, so a swing hits everyone in reach [dev];
  - Valhalla: posture that rewards aggression [analysis];
  - Mirage: a glass-cannon hero whose tools avoid fights [dev];
  - Shadows [dev]:
    - a blue flash warns of a combo that goes on through a block, parry or dodge;
    - a red flash warns of an attack to dodge: a block or parry only weakens it, and breaks your guard;
    - the more enemies there are, the fewer defensive moves each makes.
- **Who may attack** — the stage manager:
  - Kingdoms of Amalur runs 8 slots around the player [dev]:
    - a capacity of attackers and a capacity of attacks, where every enemy and every attack has a weight (a soldier
      4, a troll 8 in its example);
    - waiting enemies stand opposite free slots, which flanks for free;
    - a slot is released as soon as its attack lands, so attackers rotate;
    - difficulty only raises the two capacities.
  - God of War (2018) scores every enemy's aggression by:
    - whether it can attack at all;
    - its type's priority;
    - whether the player targets it;
    - where it is on screen.

    The best scores take tokens from a pool. On normal difficulty, only 2 of a horde are aggressive at once [dev].
  - Marvel's Spider-Man passes an attacker token around each group, pauses enemies briefly after the player dodges,
    and gives attacks on screen priority [dev]. Its full token budget is not public.
  - On average an enemy attacks every 2–3 s [analysis]. Ghost of Tsushima's enemies feel aggressive but attack one at
    a time, thanks to long opening wind-ups [analysis].

  → recipe 71 extends recipe 49's attack tokens with weights and rotation.
- **Telegraph, then a window.**
  - Human reaction to a visual cue is about 0.3 s. Ghost of Tsushima makes the first blow of a sequence slow enough to
    react to, and the rest fast, because the player anticipates them. Two or three enemies are often mid-sequence at
    once [dev].
  - DmC: Devil May Cry's tell: a pose, a flash on the weapon with a sound, a short second wind-up, then the blow
    [dev].
  - Arkham shows an icon over an attacker who can be countered [wiki]. A critic estimated about 1 s to counter
    [analysis].
  - Arkham Origins stopped players from cancelling their own blow into a counter. When both started together, the hit
    could not be avoided and the player did not know why [analysis]. → let a counter cancel the player's attack.
  - Sekiro's deflect window is about 12 frames (0.2 s), and pressing repeatedly shrinks it [wiki]. For Honor, a PvP
    game, cut some parry windows from 200 to 166 ms [dev].
  - Ghost of Tsushima: a block is held, a parry is pressed just before the hit, and a perfect parry exactly at the hit
    stuns the attacker [dev].
- **Enemy types that break the pattern.**
  - Arkham has thugs with knives (stun first) and stun batons (vault over), and puts in at most one or two special
    types at a time [analysis]. Arkham City adds shields (attack from the air) and armour (stun with a fast series
    first) [wiki].
  - Shadow of Mordor's captains have traits such as "can't be countered" and "counters you" [community].
  - Players ask for heavies you must dodge and agile enemies who survive one counter [community].
- **Lethality.**
  - Ghost of Tsushima gives every enemy a hard maximum number of hits to kill, even after upgrades.
  - Health and stagger are the same on every difficulty. Difficulty changes attack speed, group aggression, the timing
    windows and enemy damage.
  - Testers said versions with inflated health felt like hitting enemies with a foam bat.
  - Players could not tell a hit from a block until they got clearly different feedback (sparks against blood).

  [dev]
- **Feel.**
  - Sakurai's hit-stop rules: both sides freeze, longer for bigger hits, with a hard cap. In a group, though, two
    frozen fighters give a third a free moment [dev] (recipe 32).
  - Spider-Man gives the player's attack animations invulnerable frames, so a started attack isn't interrupted [dev].
- **Targeting** [dev, God of War 2018]:
  - if there is any sensible target, attack it instead of the air;
  - attacks turn to the target, and pull toward it by a reach that shrinks with the angle;
  - hit enemies are steered toward the middle of the frame;
  - enemies off screen hold their place until the player looks;
  - off-screen attacks show as arrows around the character. Flashing screen edges were read as damage.

## 12. Readability and feedback
- **The player must see what the guard thinks.**
  - For about 18 months of Thief's development players felt detection was random, because they could not tell what
    a guard thought or how well they were hidden. A light gem that brightens and darkens, with a sound, fixed it
    [dev].
  - Mark of the Ninja: three clear awareness levels, always showing their cause, e.g. guards running to the
    "ghost" of the player's last seen position; every audible noise drawn as a ring; failure made cheap with a
    checkpoint between every two big encounters [dev].
  - Shadow Tactics fills the cone with yellow from the guard's eyes, and detection happens when the yellow reaches
    the character. The start of a fill brings slow motion, a sound and the cone on screen. A pause killed the flow,
    and a rewind gave weak feedback [dev].
  - Assassin's Creed:
    - Unity added a ring around the character that points to the meters of guards off screen, and a silhouette at
      the last known position [dev];
    - Syndicate shows sound waves toward unaware enemies [dev];
    - Assassin's Creed II coloured the minimap's frame by state: conflict, line of sight broken, still searching,
      hidden [wiki].
  - Metal Gear Solid 2 colours radar cones blue (normal), yellow (noticed something) and red (found you) [dev].
- **When the simulation and the player disagree, the player wins.** Blacklist's model is fair, consistent (same
  distances and times, different animations and lines), readable and believable. Where the simulation disagrees with
  what the player believes a guard can see and hear, the player's belief wins. Guard lines go from specific to
  generic, so the player learns the rule without hearing it twice [dev].
- **Traversal must read.**
  - Everything climbable must read at a glance: yellow paint (The Last of Us), distinct handhold blocks (Uncharted),
    white edges (Tomb Raider 2013) [dev].
  - Don't repeat one move more than 2–3 times in a row, avoid 180° turnarounds, and leave room for the camera [dev].
  - The "yellow paint" debate [dev]:
    - playtesters walk past realistic props;
    - a glow is one alternative;
    - a new mechanic must be explained completely.
  - Shadow of the Tomb Raider made paint a difficulty option: blended in on normal, none on hard [dev].
  - A critic calls paint a symptom of "find the spot and press the button" climbing. Mirror's Edge's red highlighting
    instead supports several routes [analysis]. Its developers could tune the highlight's reach by skill, but would
    have preferred the path to read from architecture alone [dev].

  → recipe 67: climbable surfaces on one layer with one visual language, and a highlight the player can turn off.

## 13. Pitfalls
- **Parkour that does what the player didn't mean:** too sticky (inFAMOUS) or too smooth to control (Unity), running
  off roofs [dev, community].
- **Detection that ends the mission.** Stealth fails steeply: whoever starts losing usually loses all the way. Every
  encounter needs at least one path that can't fail, suggested but not spelled out [dev, "Level Building for
  Stealth", GDC 2006]. Tailing missions that fail on sight are the classic case [analysis].
- **Combat as the easy way out** (§11), or counters so strong that fights become waiting [dev, community].
- **The same procedure nine times:** identical investigations before every target [analysis].
- **Waiting for a target's routine** to come round [dev].
- **A map full of icons**, or viewpoints as the only way to learn about a place [analysis, dev].
- **Detection that feels random:** unpredictable test points, no gauge, no cause shown [dev].
- **Alarms that spread across the level** [dev].
- **A player on a roof who can't be answered** [dev].
- **Long searches:** a 2-minute cycle cut to 30 s [dev].
- **Crowds:**
  - vanishing when the player looks away [analysis];
  - popping between levels of detail [community];
  - swinging between calm and panic [dev];
  - fleeing forever [dev].
- **Fall damage as an invisible wall** [analysis].

## 14. Measured in a district [measured]
game-builder's `stealth-parkour-3d` template (2026-09-29) is one 70 m greybox district:
- houses with lipped faces and 2 m alleys, a 15 m viewpoint tower over hay;
- five guards and fourteen townspeople;
- one assassination contract.

A bot plays it through the real input actions. One template and one bot, so these show mechanisms, not universal
numbers.
- **The contract is a window, not a route.** The bot finished it unseen by waiting, hidden in hay, until the target
  stood at its quiet stop and both patrols were over 14 m away. The target's 90 s loop gave that window about once a
  loop; its 10 s wait at the quiet stop was what made the strike possible. Routines are level design.
- **Holds need to be usable, not only found.** From a roof under a taller wall, the lowest hold in reach was a lip at
  knee height: too low to stand on, too low to hang from. The grab failed until the climber learned to look above such
  holds.
- **A body stopped dead at a corner.** Godot stops a character pushing within 15° of a wall's normal instead of
  sliding it along. Both players and bots feel this at crates and hay piles.
- **Honest guards need the sighting's own position.** Guards look ten times a second. Read with the player's live
  position, a sighting recorded where the player went a moment later. The position must come from the look itself.
- **Unreachable places end searches.** A player seen standing on a stall left a last seen place off the navigation
  mesh. The guard never arrived there, and so never searched. "Arrived" has to mean "as close as the paths allow".
- **Radii reveal by the metre.** A viewpoint's 40 m sync revealed a poster 39.99 m away. Test what a sync reveals.
- **Cost:** with every guard hunting and the crowd panicking, the worst frame of each second measured 5.5 ms (process,
  p95) and 0.65 ms (physics, p95) over 120 s. The five guards' scripts took about 0.14 ms a frame. A 60 s run measured
  the scene's start instead (89 ms p95): measure long enough.

## Principles → game-builder parts
| Principle | Where it lives |
|---|---|
| Walk / run / sprint / sneak profiles with a noise radius each, separate up and down intents, stop at edges, jump buffer and coyote time, a fall rule with soft landings | recipe 66 |
| Ledge probe (wall angle, top, clearance) as a pure function, hang / shimmy / climb up / drop / jump to the next ledge, climbable layer and highlight | recipe 67 |
| Vision shapes (near, far, peripheral) with a timer that rises and falls, one or two test points, light and stance and crowd modifiers; noise along the navigation path with priorities | recipe 68 |
| Awareness states, shared last known position, roles (one investigator, 2–3 searchers), search points, bodies and missing companions, a gradual return | recipe 69 |
| Crowd on lanes, moods that only worsen from stimuli, four-phase reactions, flee to exits, level of detail by distance, blend groups and benches | recipe 70 |
| Weighted attack tokens that rotate, telegraph → counter window, unblockable attacks, a counter that cancels the player's attack, a hard hits-to-kill cap | recipe 71 |
| Notoriety levels with named effects, witnessed acts, a search circle at the last seen position, ways to lower it | recipe 72 |
| Viewpoints that reveal nearby markers and become fast-travel points, a target's routine as a short loop of stops, contracts in phases (reach, strike, escape) where detection changes the phase instead of failing | recipe 73 |
| Third-person orbit camera | recipe 40 |
| Animation state machine | recipe 44 |
| Attack tokens | recipe 49 |
| Hit-stop, hit flash | recipes 32, 33 |
| Health | recipe 05 |
| Minimap or compass | recipe 45 |
| Checkpoints | recipe 41 |
| Navigation | recipe 26 |
| Saves and settings | recipes 13, 17 |

## Not established
The research looked for these and found no reliable open source. Don't quote numbers for them; tune in playtests.
- **Assassin's Creed metrics:** jump distance, grab reach, climbing speed, vault and mantle heights, fall-damage
  heights.
- **Whether the series' handholds are marked up by hand or detected**, and whether its parkour uses motion
  matching.
- **Breath of the Wild's climbing numbers** (stamina per second, jump cost, speed, slipping in rain).
- **Input buffers in 3D traversal** of any big game; Celeste's are 2D.
- **Cone angles and ranges** of any shipped stealth game, in degrees and metres.
- **Detection fill times** beyond The Last of Us (1–2 s) and Blacklist ("a few seconds").
- **Alarm, search and "vanishing" durations** (Metal Gear Solid, Assassin's Creed, GTA V).
- **Passive notoriety decay** and how much each act adds, in any Assassin's Creed.
- **How many guards react** to an event in Assassin's Creed or Hitman.
- **Counter and parry windows** in Assassin's Creed, Arkham, Sleeping Dogs, Shadow of Mordor or Ghost of Tsushima,
  from a developer or a measurement.
- **How Arkham's free-flow combat picks a target**, and how far it lunges.
- **How many enemies attack at once** in Arkham or the early Assassin's Creed games; how many tokens Spider-Man
  uses.
- **Hit-stop durations** in 3D action games, and enemy wind-up times in milliseconds (only For Honor, a PvP game).
- **Crowd budgets** of the first Assassin's Creed, Hitman's later cities, Spider-Man and GTA: spawn radius, levels of
  detail, milliseconds.
- **Onlookers gathering around a body, and a witness walking to tell a guard**: no documented mechanic.
- **Godot 4.7 numbers** for instanced skeletal animation, vertex-animation textures for humanoids, or how many RVO
  agents fit in a frame. Whether Godot 4.7 has built-in open-world streaming: its documentation doesn't say.
- **City sizes from Ubisoft** (only fan measurements), the time to cross a city, and how long an assassination
  mission or a Hitman level typically takes.
- **Content density**: points of interest per km² or per minute of walking, in any open-world game.
- **The first game's exact numbers:** how many investigations were required (sources disagree: 2 or 3 of 6), and
  how many viewpoints it had.

## Sources
Researched 2026-09-28. The main sources:
- **Developer:**
  - Game Developer, "Post-GDC: Defining the Assassin" (2006); Ubisoft News on the evolution of the series' parkour
    (2024) and stealth (2024); Ubisoft, Assassin's Creed Shadows parkour (2025) and combat (2024) overviews; Ubisoft
    News on Mirage's tools (2023);
  - Edge, "The Making of Assassin's Creed"; Polygon, "Assassin's Creed: An oral history" (2018);
  - F. Cournoyer, "Massive Crowd on Assassin's Creed Unity: AI Recycling", and C. Blondeau, "Postmortem: Developing
    Systemic Crowd Events on Assassin's Creed Unity" (GDC 2015); TechRadar and The Escapist on Unity;
  - Game AI Pro: M. Dawe, "Beyond the Kung-Fu Circle"; B. Miles, "How to Catch a Ninja"; M. Walsh, "Modeling
    Perception and Awareness in Splinter Cell: Blacklist"; T. McIntosh, "Human Enemy AI in The Last of Us"; R. Welsh,
    "Looking for Trouble: Making NPCs Search Realistically"; E. Emerson, "Crowd Pathfinding and Steering Using Flow
    Field Tiles";
  - T. Leonard, "Building an AI Sensory System" (Thief, GDC 2003); P. Neurath on Thief's light gem; N. Anderson on
    Mark of the Ninja; M. Wagner, "Dynamic detection in Shadow Tactics"; R. Smith, "Level Building for Stealth
    Gameplay" (GDC 2006); D. Isla, "Third Eye Crime" (AIIDE 2013); Metal Gear Solid manuals (Konami);
  - K. Fauerby, "Crowds in Hitman: Absolution" (GDC 2012); R. Blouin-Payer, "Managing Crowd AI in Watch Dogs 2"
    (GDC 2017); D. Santiago on procedural Manhattan (GDC 2019);
  - M. Sheth, "Evolving Combat in God of War for a New Perspective" (GDC 2019); A. Noonchester on Marvel's Spider-Man
    AI (GDC 2019); C. Zimmerman and T. Fishman on Ghost of Tsushima (PlayStation Blog, GDC 2021); M. Sakurai on
    hit-stop (Famitsu); For Honor patch notes; M. de Plater, Shadow of Mordor postmortem;
  - GDC talks on Mirror's Edge (2009), Dying Light (2018) and camera mistakes (J. Nesky, 2014); S. Clavet on motion
    matching (2016); PlayStation Blog and Game Informer on Uncharted 4; M. Hoffstetter, "Traversal Level Design
    Principles";
  - A. Mandryka, "Assassin's Creed Flow"; Xbox Wire and GamingBolt on Mirage; J. Dumont on Syndicate's world design;
    Kotaku on Origins' quest rules; Push Square on the first game's side activities; IO Interactive, "Level Design in
    HITMAN: Guiding Players in a Non-Linear Sandbox" (GDC Europe 2016), with interviews in TheGamer and GamingBible
    and Game Developer on Elusive Targets; H. Smith and C. Carrier on Dishonored's levels; the translated CEDEC 2017
    talks on Breath of the Wild's world, and H. Fujibayashi on its map; N. Fox on Ghost of Tsushima's guidance; Epic
    documentation on World Partition;
  - US patent 12097432 B2 ("Markup free ledge grab"); V. Cantão, "Climbing system"; Celeste's player code; Epic
    documentation (City Sample, Smart Objects, motion warping, animation budget); GPU Gems 3, "Animated Crowd
    Rendering"; Game Informer's developer interviews; Godot 4.7 documentation.
- **Analysis:** S. Costiuc (Assassin's Creed scale, the first game's HUD-less design, Assassin's Creed III's
  missions, Arkham, Ghost of Tsushima); M. LoPresti on the first game's investigations; JB Oger on open-world
  towers; R. Yang on Breath of the Wild's spatial composition; B. Vossen on melee enemy design; S. Young on Arkham
  Origins; T. Thompson on Hitman and Blacklist; C. Wagar on climbing highlights; Kotaku, Game Rant, NVIDIA's GTA V
  guide, Tom's Hardware, Playfront; Dobbyn et al., "Geopostors" (I3D 2005).
- **Wikis:** Assassin's Creed Wiki (social stealth), Hitman Wiki (crowds, disguises), GTA Wiki (wanted levels),
  Watch Dogs Wiki (heat), Tomb Raider level-editing wikis, Sekiro wiki, Wikipedia.
- **Community:** The Hidden Blade, Steam discussions, Unreal Engine forums, DSOGaming, Gamepressure, GamersHeroes,
  MajorSlack.

Game names are trademarks of their owners and are used only to identify the source of a design observation.
