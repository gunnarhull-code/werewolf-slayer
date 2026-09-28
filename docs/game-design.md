# Werewolf Slayer — Game Design Plan

2026-09-22 22:36

## Contents

- [Concept & Elevator Pitch](#concept--elevator-pitch)
- [Design Pillars — What Keeps Players Coming Back](#design-pillars--what-keeps-players-coming-back)
- [Core Gameplay Loop](#core-gameplay-loop)
- [Player Character & Progression](#player-character--progression)
- [Weapons, Modifiers & Builds](#weapons-modifiers--builds)
- [Status Effects & Builds](#status-effects--builds)
- [Checkpoints & Route System](#checkpoints--route-system)
- [Enemies & Wave Design](#enemies--wave-design)
- [Floors & Environments](#floors--environments)
- [Meta-Progression & Unlocks](#meta-progression--unlocks)
- [Art, Audio & Tone](#art-audio--tone)
- [Platform, Scope & Technical Plan](#platform-scope--technical-plan)
- [Monetization & Release Plan](#monetization--release-plan)

## Concept & Elevator Pitch

**Werewolf Slayer** is a top-down horde-survival roguelite in the Vampire Survivors mold: a cursed hunter stands against endless waves of werewolves and their monstrous kin, armed with a primary weapon they aim themselves, backed by secondary weapons that auto-fire, in a fight built around positioning and reading enemies rather than just circling and holding a direction.

**Player fantasy:** a lone hunter overwhelmed by escalating odds, surviving and growing more powerful through their own build choices rather than outside help — this is the anchor every other system in this document should serve, from combat feel to the Moon Meter's risk/reward curve to the shape of the modifier pool.

**Premise:** A silver-blooded hunter is bound to a cursed forest that floods with lycanthropes every full moon. Each run pushes across 4 floors, clearing rooms picked one at a time from a route map until each floor's boss falls and the next floor opens.

**The hook — the Moon Meter:** Each room runs its own Moon Meter, filling as you fight — driven by both time and kill count — and driving that room's Day → Night (a full moon) cycle, with an occasional Blood Moon on top. As it climbs, ordinary Wolves begin turning into full Werewolves mid-fight, fog rolls in and reduces vision, and spawn density spikes. Once you've found a room's exit you can leave through it at any time — but the meter keeps climbing the whole time you stay, so it's a constant bet: pull out now with what you've got, or hold out for better loot and rarity at rising risk. This is the risk/reward tension Vampire Survivors doesn't have: killing fast earns XP faster but also fills the meter faster, trading immediate power for a harder fight the longer you push your luck in that room.

## Design Pillars — What Keeps Players Coming Back

These are the retention-driving forces this design is built around — reverse-engineered from Brotato, Risk of Rain (1/2), and Vampire Survivors, then deliberately kept, rejected, or bent to fit Werewolf Slayer's own identity. Every system elsewhere in this doc should trace back to one of these; a system that doesn't serve any of them is a candidate to cut.

- **Legible variance:** every draft (level-up, Shrine, meta unlock) should feel *predictable in shape, surprising in content* — the player always knows a card is coming and roughly what kind of thing it might be, never which specific card. This is what the ~30-entry Modifier pool, rarity tiers, and build-weighted (not pity-system) draws exist to protect (see Weapons, Modifiers & Builds).
- **Compounding power, not additive power:** a run should read as an acceleration curve — fragile early, screen-warping late — not a flat climb. Synergy Tiers, Might stacking, and Power-scaled VFX are all in service of this; a Modifier pool that leans too hard on flat number-ups undercuts it (see the number-vs-mechanical design principle under Modifiers).
- **Meta-progression as a safety net against permadeath:** dying should always feel like it banked something — Silver Shards, Unlock Track progress — so a "failed" run still reads as forward motion. This is why meta-progression stays in scope even in the MVP's otherwise stripped-down cut (see Meta-Progression & Unlocks; `mvp-mechanics.md`'s death draft).
- **Build diversity over content volume:** a new card combination should feel like a new game, not a variation on one. This is the job of Bloodline Signature Cards, the status-effect layer, and Synergy Tiers — cheap replay value that doesn't require new floors or enemies to deliver (see Weapons, Modifiers & Builds; Status Effects & Builds).
- **Long runs, deliberately — not the genre norm:** unlike Brotato/VS/RoR's 15–30 minute loops, a Werewolf Slayer run spans 4 floors and can run well past an hour. This is a conscious divergence, not an oversight — the tension/release pacing rhythm (3 rooms → Miniboss → 3 rooms → Floor Boss, see Floors & Environments) and the room-level Moon Meter are the tools doing the "one more push" job that a short overall run timer does in the reference games. Exact session-length numbers and restart-cost mitigations are still open (see Core Gameplay Loop).
- **Density as restraint, not spectacle:** baseline enemy counts stay well below the genre's screen-filling norm on purpose (see Enemies & Wave Design) — the hook here is reading a fight and positioning, not watching a swarm evaporate. This is a deliberate rejection of Vampire Survivors' core spectacle loop in favor of a skill-expression one; true swarm chaos is reserved for deliberate spikes (Elite Den, Blood Moon), not the constant state.

**Open — under active reconsideration:** the Moon Meter, Curse Omens, Room Omens, reward-scaling-by-depth, and Ability Cache's one-way trade are all legible risk/reward toggles stacked on top of each other. Whether all five are meant to coexist at full scope, or whether some should merge or drop once the MVP validates the base loop, isn't decided — worth revisiting as concrete either/or questions once there's a playable build to test against, not settled on paper now.

## Core Gameplay Loop

- **Controls:** movement (WASD / left stick) is separate from aim (mouse / right stick). Weapons auto-fire once you're aimed — no separate fire button — except on hunters with an Auto-Aim trait, who skip aiming entirely and play closer to a classic auto-battler.
- **Primary weapon:** locked to each hunter from the start and never removed. This is where the game's buildcrafting depth lives — modifiers stack onto it (see Weapons, Modifiers & Builds).
- **Secondary weapons:** 2–3 additional slots found during a run. These auto-fire and auto-target the nearest enemy, giving the classic screen-filling spectacle as a support layer rather than the main skill expression.
- **Active Ability:** one equipped slot (a 2nd unlocks later), manually triggered with a cooldown — a heal, a block, a knockback, a dash, a team buff, not just a bigger version of your stats. Swapped only at Ability Cache checkpoints (see Checkpoints & Route System); each swap replaces the current Active permanently.
- **Rooms:** the unit of play — pick one from the route map, get dropped into it, and fight for roughly 6–10 minutes. A room already has a standing population of preexisting spawned mobs on entry — it isn't empty. Each room runs its own Day → Night → occasional Blood Moon cycle (see The Hook — the Moon Meter): halfway through, a timer starts that shifts the room from day to night and adds *more* offscreen spawning on top of the baseline, pushing players toward the exit instead of turtling indefinitely — the room visibly darkens, a full moon rises on screen, an ominous sound cue plays, and a text announcement reads **"THE FULL MOON HAS RISEN."** **Open:** the exact trigger/cadence for a room going all the way to a Blood Moon (rather than stopping at an ordinary Night) isn't decided yet.
- **Exiting a room:** every room has an exit. Once you've found it, you can leave through it at any time, banking whatever Silver Shards and loot you're carrying — clearing it fully (or just outlasting its Moon Meter longer) pays out more than leaving the moment you find the door. Exiting returns you to the route map to pick the next room.
- **Choices pause the game:** any in-room choice screen (level-up draft, Curse Omen draft, Ability Cache swap) pauses the game — including the room's spawn-ramp timer — while it's waiting on the player: players shouldn't be punished by the clock for time spent in a menu.
- **Session length:** open — the old "15–20 minutes, one continuous timer" framing doesn't map cleanly onto "multiple 6–10 minute rooms across 4 floors" anymore; needs a fresh pass once floor size (how many rooms per floor) is decided. Endless Mode removes the timer entirely regardless (see Meta-Progression & Unlocks).
- **Win condition:** clear all 4 floors and defeat the final floor's boss. **Lose condition:** HP reaches 0 — Silver Shards and unlocks earned that run are still banked.
- **Design intent:** the aim requirement, capped enemy density, telegraphed attacks, and terrain-driven floors (see Enemies & Wave Design, Floors & Environments) all serve one goal — reward reading a fight and positioning, not circling and holding a direction. Status effects (see Status Effects & Builds) extend that same intent to 4-player co-op, so builds create real teamwork rather than four people surviving in parallel.

**Numbers & rarity convention:** flat bonuses are small whole numbers (**+2 damage**); scaling effects are shown as a factor (**x1.4 damage**); true chance is a percentage (**25% chance**); a guaranteed payoff is cadence-based (**every 4th hit**). Randomly-drawn content (modifiers, Actives) also carries a rarity tier — Common / Rare / Super Rare — where a higher tier adds a genuinely new effect on top of the base card, not just a bigger number. Exact drop rates are a balancing-pass question, not fixed yet.

## Player Character & Progression

- **In-run leveling:** kills drop Silver Shards (XP); filling the bar offers a draft of 3 cards from the run's deck (see Weapons, Modifiers & Builds).
- **Bloodlines:** picked at run start, each Bloodline locks in a starting weapon (never removed — it's the character's identity), a set of Bloodline signature cards (see Weapons, Modifiers & Builds), and a distinct personality that colors card-draft lines and Cursed Voice encounters.

| Hunter | Bloodline | Locked Weapon | Trait | Voice |
| --- | --- | --- | --- | --- |
| The Ranger | Silver Line | Silver Crossbow | Auto-Aim | Disciplined, clinical — *"Efficient. I'll take it."* |
| The Ferox | Moon-Touched | Blessed Chain Whip | Manual aim | Hungry, seduced by the curse — *"I can feel it... good."* |
| The Warden | Warded | Holy Water Flask | Manual aim | Weary, dutiful — *"Another ward. Another night survived."* |

Wolfsbane Bomb, Silver Buckshot, Moonlight Lantern, and Arcane Beam make up the current Secondary Weapon pool (see Weapons, Modifiers & Builds) — found during runs, not locked to any hunter.

- **Unlock Tracks:** each hunter has a short set of milestones only completable by playing them — a 6th signature card, an alternate weapon skin, a bio fragment advancing their story. Example, The Ranger: survive a room through a Blood Moon → unlock *Relentless Volley* signature card; land Silver Cascade in a completed run → alternate Crossbow skin; crit-kill an Alpha Werewolf → bio fragment.

## Weapons, Modifiers & Builds

Four card categories feed into a build: Modifiers, Secondary Weapons, Bloodline Signature Cards, and Active Abilities. Each is described on its own below.

### Primary Weapon

Locked to each hunter (see Player Character & Progression) and never removed — everything below stacks onto it.

### Modifiers

A curated pool of physical properties on your primary weapon's projectile or effect, drawn on level-up alongside Bloodline signature cards. The pool is universal — every modifier applies to every primary weapon, reinterpreted in that weapon's own flavor (a trajectory modifier becomes the Whip's swing arc rather than a projectile path). Every base card carries a real tradeoff, never a pure number-up — though a Rare or Super Rare roll can shed or soften that tradeoff as part of its upgrade (see Rarity, below).

*Illustrative examples only — not the full pool (currently sized around 30 entries):*

| Category | Example modifiers |
| --- | --- |
| Velocity & Size | Fleetfang Rounds (+2 speed, -1 damage) · Heavy Slugs (+3 size, -1 speed) |
| Trajectory | Serpent's Path (sine wave) · Falling Star (arcs down, small AoE on landing) |
| Split & Multiply | Cloverleaf Split (splits into 3 on impact) · Twinned Shot (x2 projectiles) |
| Terminal Behavior | Ricochet Silver (bounces off the arena edge once) · Deep Bite (+1 pierce, half damage on the pierced hit) |
| Exotic | Orbiting Fang (circles you once, then launches at the nearest enemy) · Gravity Well (impact briefly pulls nearby enemies toward it; travels slower) |
| Impact & Damage Shape | Focused Point (no AoE at all; +3 flat damage on direct hits) · Arc Slash (damage sweeps in a narrow arc instead of a circle, hitting a line of enemies) |

**Design principle — number vs. mechanical adjustments:** every card above is one of two kinds — a *number adjustment* (changes a stat: +2 speed, -1 damage) or a *mechanical adjustment* (changes what the weapon actually does: sine-wave trajectory, splitting on impact, bouncing off walls). Number adjustments are the easiest to add and balance, but a pool that leans too heavily on them risks the build feeling identical run to run regardless of which cards were drawn — a build should be recognizably different to *play*, not just bigger. The Velocity & Size category is intentionally the only pure-number-adjustment category; every other category is mechanical or a mechanical/number hybrid, and that ratio should hold as the pool grows toward its full size.

### Secondary Weapons

2–3 equip slots, found during a run, always auto-fire and auto-target the nearest enemy (no aim needed).

*Current full pool (see Player Character & Progression):* **Wolfsbane Bomb** (delayed AoE explosion), **Silver Buckshot** (short-range cone burst), **Moonlight Lantern** (passive damaging aura, grows with level), **Arcane Beam** (a continuous magic laser that locks onto and sweeps toward the nearest enemy, ramping damage the longer it holds a target).

### Bloodline Signature Cards

3–5 per Bloodline, guaranteed in that Bloodline's deck, always thematic, capped by a capstone.

*Example — the Silver Line's set, not a universal template:*

- Silver Fang Rounds — 15% crit chance
- Piercing Volley — +1 pierce
- Twin Barrel — x2 projectiles
- Marksman's Focus — +2 damage after holding still 1s
- *Silver Cascade* (capstone) — every 4th crit fires a free ricochet bolt

### Active Abilities

A separate 4th card category, filling one equipped slot (a 2nd unlocks later), manually triggered with a cooldown. Deliberately varied in role, not just bigger stat payoffs. Drawn uniformly at random from the full shared pool — not filtered or weighted by class or current build — and swapped only at Ability Cache checkpoints (see Checkpoints & Route System); a swap replaces the current Active permanently.

*Illustrative examples only — not the full pool:*

| Role | Example Actives |
| --- | --- |
| Offense/Burst | Overwhelm (consume all Might for one devastating hit) |
| Defense/Survival | Moonlit Ward (3s full invincibility) · Second Wind (instant heal + regen) |
| Control | Howling Blast (knockback wave) · Silver Snare (roots enemies briefly) |
| Mobility | Wolf's Leap (short dash/blink) |
| Support | Rally Cry (buff nearby allies) · Cleansing Light (strip a debuff from an ally) |

### Rarity

Modifiers and Actives can roll at Common, Rare, or Super Rare. A higher tier isn't just a bigger number — it adds a genuinely new effect on top of the base card, and can shed or soften the base card's downside as part of that upgrade (e.g. Rare Toxic Bloom might add a secondary burst; Super Rare Toxic Bloom might also lose the base card's cooldown penalty). This still has to stay balanced card by card, not a blanket free upgrade. Drop rates are a balancing-pass question, not fixed yet.

### Synergy Tiers

Card synergy across a build falls into three tiers, and a healthy pool needs a mix of all three rather than leaning on just one:

- **Minor synergies:** small stat interactions that reward a build without defining it — a crit-chance modifier feels better alongside Piercing Volley's extra hits, higher fire rate makes a Blight-on-hit modifier proc more often. These are the constant, low-key texture of a run.
- **Major synergies:** cards that actively define a playstyle together, most concentrated in Bloodline Signature Cards and their capstones (see Status Effects & Builds' example builds) — a Blight build isn't just "Blight cards happen to be in the deck," it's several cards whose whole purpose is amplifying that one status. **Design rule:** avoid drifting so far toward major synergies that most drafted cards feel useless outside one specific build (the failure mode of item pools split into narrow archetypes) — every card should have *some* standalone value even off-build.
- **Scripted synergies (future/stretch):** a specific named combo of two or more cards that triggers an explicit bonus effect when both are held together, rather than just their individual effects adding up naturally. Not designed yet, but worth keeping as a stretch goal — these reward players who recognize a set forming, and are memorable because they're rare and explicit rather than emergent.

## Status Effects & Builds

A shared resource layer that almost every card interacts with — this is what turns a pile of separate cards into a real build (a Blight build, a Ward/Thorns build, a Might build), and what lets status synergy create real teamwork in 4-player co-op.

| Status | Effect |
| --- | --- |
| Might | Flat permanent damage bonus, stacks unless a card says otherwise |
| Ward | An absorb shield; regenerates over time |
| Thorns | Flat retaliation damage to anything that hits you in melee range |
| Blight | Stacking damage-over-time on an enemy, ticks down each second |
| Marked | Target takes increased damage for a duration — shared across all players hitting it |
| Hobbled | Target deals reduced damage for a duration |

**Example builds:**

- **Blight (Trapper-style):** Wolfsbane Coating (hits apply 2 Blight) → Festering Wound (Blight ticks twice as often below half HP) → Spreading Rot (Blight spreads to nearby enemies on a Blighted kill) → capstone *Plague Lord* (Blight stacks uncapped; max-stack enemies explode).
- **Ward/Thorns (Warden-style):** totems grant nearby allies Ward on a timer → Barbed Plating (+Thorns while Ward is active) → Unyielding (Ward regenerates faster while standing still) → capstone *Bulwark of the Pack* (Ward that would break instead bursts into Thorns damage).

**Team synergy:** Marked applied by one player boosts everyone's damage on that target; Ward can be cast on an ally, not just yourself. A run's best moments should come from status roles clicking together — someone marking priority targets, someone tanking with Ward/Thorns, someone finishing with Might — not four players circling in parallel.

## Checkpoints & Route System

After clearing or exiting a room, the route map pauses briefly and offers 2–3 next-room choices, drawn from one weighted pool — this is the run's main strategic branching, on top of in-combat positioning:

| Node | Rarity | Effect |
| --- | --- | --- |
| Elite Den | Common | Tougher upcoming wave, guaranteed loot |
| Shrine | Common | A free, curse-free card draft |
| Merchant | Common | Spend Silver Shards |
| Ritual Site | Uncommon | Hold the point (solo or as a group) through a focused wave for a strong reward |
| Sanctuary | Uncommon | Partial heal, slower spawns |
| Ability Cache | TBD (uncommon–rare) | Offered 2 random Actives; swap one for your current Active, or keep it — a permanent, one-way trade |

**Random Events:** a separate category from the node table above — scripted encounters that can appear as a pickable option on the route map rather than a standard room type. **Cursed Voice** (Rare) is the only one designed so far: a wolf-spirit offers a curse bargain — **Accept** (power + cost + reactive dialogue), **Refuse** (small shard consolation), or **Question** (a softer boon instead). Moon-Touched gets an extra **Embrace** option (softened cost); Warded gets a **Cleanse** option (burn an existing curse instead). This 3-option structure is a deliberate **agency** design: none of the three outcomes is strictly correct, so the choice actually has weight, and framing each option with distinct dialogue and tone (not just a plain "yes/no") makes the choice feel heavier than its mechanical effect alone would. More Random Event types are expected but not yet designed — a good design direction for future ones is **subversion**: an event that looks like a known, safe pattern (e.g. a reward chest) but occasionally breaks that pattern, the way a run's danger should never become fully predictable even to a veteran player.

**Reward scaling:** checkpoint and loot rewards get juicier as you push deeper into a floor's room tree — later rooms roll better rarity odds, bigger Silver Shard payouts, and stronger node rewards (Elite Den loot, Ritual Site prizes) than the same node type early on, so the risk/reward curve keeps climbing alongside the difficulty rather than flattening out.

**Build-weighted draws:** card draws (level-up drafts, Shrine offers) lean slightly toward modifiers and cards that synergize with what the player has already picked, rather than a pure uniform roll — a soft nudge, not a hard pity system, so a build can come together without being fully RNG-dependent. **Open:** whether early-run drafts should also lean toward simpler, single-effect cards before introducing denser multi-clause ones later in a run — a **chunking** approach to onboarding a new player into the modifier system gradually rather than handing them the full complexity on the very first level-up — isn't decided yet.

Burns, granted by Alpha Werewolf kills, are the only way to remove a card from your deck, including a curse.

**Room Omens:** beyond the node-type table above, an individual room can also roll a modifier from a shared pool — **Omens** — that curses are just one entry in. Once a room's Omen is set, the route picker shows an icon on that node from **two or more spaces ahead** — a deliberate **signposting** device, giving advance warning of what kind of room is coming (without full detail yet) the same way a lit doorway or a warning color reads at a glance without needing text. Other Omen types raised so far, none fully specified: a "Flood" Omen (effect TBD), and reward-boosting Omens (extra Silver Shards, extra loot — exact form TBD). **Design rule:** any debuff-flavored Omen must carry reward comparable to or greater than a pure-benefit Omen, so risk and reward stay balanced across the whole Omen pool, not just within Curse Omens.

**Curse Omen** (one Omen type): not a per-transition guarantee — each room independently rolls a percentage chance of containing a guaranteed curse (exact odds TBD). Reaching the end of a curse room presents it as a standard card-reward screen — a draft of **3 curse options to choose from**, the same format as a level-up draft, not a single forced card. The curses available across a run are drawn from one **predrawn deck**, generated at run start; in co-op, the deck is shared across the whole party, and a chosen curse can affect everyone, not just the player who picked it. Severity still decides whether a buff comes attached — a major drawback pairs with a real power buff, a minor drawback doesn't.

**Curse pick motivation:** choosing to walk into an Omen'd room in the first place is what's rewarded — a room flagged with an Omen icon typically comes with a better payout attached (extra Silver Shards, better loot, or a benefit baked into the curse card itself) specifically because you knowingly picked the riskier room off the map. The curse draft inside it is still a genuine choice among 3 options, not a tax for entering.

## Enemies & Wave Design

- **Base enemies:** Feral Wolf (fast, weak, baseline) · Werewolf (a Wolf that's turned as a room's Day → Night cycle advances — tankier, hits harder) · Bat Swarm (erratic movement) · Cultist (ranged, punishes standing still) · Ghoul (slow, high HP, area denial).
- **Elites & bosses:** Alpha Werewolf (mini-boss, can spawn as a room's cycle advances, drops a Burn on kill) · a **Floor Boss** caps each floor's room tree — clearing it opens the next floor; the 4th floor's boss, the **Blood Moon Reaver**, ends the run.
- **Telegraphed attacks:** dangerous hits (an Alpha's lunge, a Werewolf's howl-marked target) flash or wind up before landing — dodging should be a read-and-react skill, not passive movement.
- **Affordance:** an enemy's silhouette and movement should telegraph its role before the player ever reads a tooltip — Feral Wolf reads as fast and fragile at a glance, Ghoul reads as slow and heavy, Cultist's static ranged stance reads as "punishes standing still." Mismatched affordance (a dangerous enemy that looks harmless) undercuts the read-and-react intent above.
- **Punching bags:** not every enemy needs to be a real threat — Feral Wolf in particular should stay a low-effort kill throughout a run, existing so players can feel their current build actually working rather than white-knuckling every encounter. A room that's nothing but genuine threats stops feeling like a power fantasy and starts feeling like a slog.
- **Density:** baseline enemy counts stay well below the genre's usual screen-filling swarm — real threats you can read, not wallpaper, keeping the moment-to-moment cognitive load manageable even as the modifier pool and status layer add complexity elsewhere. True swarm chaos is reserved for deliberate spikes (Elite Den, a room's Blood Moon), not the constant state.
- **Curve:** within a room, driven by its Day → Night (Full Moon) → occasional Blood Moon progression rather than a flat timer alone — each transition escalates the fight, and that difficulty compounds again as you push deeper into a floor's room tree.

## Floors & Environments

A run always starts at Floor 1 and progresses linearly through Floors 2, 3, and 4 — picking a hunter is the only choice made before a run begins, distinct from the in-run route/checkpoint picker (see Checkpoints & Route System). Each floor is unlocked by clearing the previous one, giving light structure to first-time progression before the game opens up to free floor select for replaying earlier floors directly.

**Floor room-tree structure:** each floor's room tree is a fixed gauntlet — 3 rooms (each with the normal route-map branching) → **Miniboss Room** → 3 more rooms → **Floor Boss**. The Miniboss Room appears on the route map as the sole option at that point in the tree rather than one of 2–3 choices — reaching it isn't a strategic pick, just the run's next step. Unlike a normal room, it's a dedicated, single-purpose combat space: no standing mob population to clear incrementally, no route-map branching inside it, and little to explore — you're dropped in for one focused fight against the room's miniboss and then move on. **Open:** whether the Miniboss Room runs its own Moon Meter/Day-Night cycle, and whether the miniboss role is filled by the existing Alpha Werewolf or a new enemy per floor, aren't decided yet.

**Pacing rhythm:** the 3-rooms → Miniboss → 3-rooms → Floor Boss shape is a deliberate tension/release cycle, not just a length-padding structure — tension builds across each set of 3 normal rooms (each with its own Moon Meter escalation), spikes and resolves at the Miniboss Room, resets to a calmer baseline, builds again, and spikes harder at the Floor Boss. A floor that was just one long, flat difficulty ramp with no release points would feel exhausting rather than escalating.

**Floor biome pools:** each floor slot doesn't have one fixed setting — it rolls a random biome each run from that slot's own pool, all biomes in a pool being equally likely. Terrain is a deliberate tool everywhere: every biome should give players a reason to choose *where* to fight, not just *when* to move. Natural hazards across every biome are deliberately kept as **friction, not punishment** — a brief slow, stumble, or small damage tick that costs the player a beat of attention, never something severe enough to ruin a run on its own; the goal is a small, constant texture of "pay attention here," not a wall. Interactive objects and buildings are meant to visually anchor a scene and double as cover or a funnel point; traps do minor damage or knockback and can be turned against enemies as often as they threaten the player; puzzles solve with a single attack on the right object — opening a shortcut, a secret room, or granting a small heal, never a multi-step chain.

### Floor 1

| Biome | Setting | Twist |
| --- | --- | --- |
| Cursed Forest | Moonlit woods, the starting biome | Open sightlines, gentlest curve — a few loose chokepoints to learn the positioning game |
| Moonlit Marsh | Waterlogged wetlands | Open sightlines like the Forest, but shallow bog patches add a movement hazard — teaches positioning around terrain before Floor 2's walls do it with geometry |
| Silver Orchard | A hunter's abandoned homestead | Rows of dead trees form loose natural lanes — a gentler, more structured cousin of the Forest's open ground |

- **Cursed Forest** — *Hazard:* loose roots (brief stumble, no damage). *Object/cover:* a ring of moss-covered standing stones. *Building:* a hunter's shack (chest room); an old watchtower ruin (elevated funnel point). *Trap:* a rusted bear trap — snaps on whoever steps in first, so it's as useful for luring a Wolf onto as it is a hazard to the player. *Puzzle:* strike an overgrown shrine to clear the vines blocking a shortcut.
- **Moonlit Marsh** — *Hazard:* shallow bog patches (brief movement slow). *Object/cover:* a half-sunk wagon wreck; tall reed clusters soften sightlines around it. *Building:* a stilted fisherman's hut (chest room). *Trap:* a bubbling gas pocket — minor damage or knockback, usable against enemies standing on it. *Puzzle:* strike a rotted piling to collapse a short bridge, exposing a loot cache underneath.
- **Silver Orchard** — *Hazard:* fallen fruit underfoot (brief slip, no damage). *Object/cover:* a dry stone well at the orchard's center. *Building:* a root cellar (chest room) under a collapsed farmhouse that funnels enemies through one doorway. *Trap:* a rigged scarecrow — topples when struck, minor knockback/damage to anything below it. *Puzzle:* ring the orchard bell to unlock the cellar door.

### Floor 2

| Biome | Setting | Twist |
| --- | --- | --- |
| Abandoned Village | Burned-out town | Tight chokepoints and house walls actively shape fights — funnel Werewolves through doorways into Thorns/Blight builds |
| Frozen Homestead | A snowed-in farm compound | Fences and barns create chokepoints like the Village, but icy patches add a footing hazard on top |
| Sunken Mill Town | A half-flooded village | The water itself is difficult terrain, pairing naturally with a Flood Room Modifier if one rolls here |

- **Abandoned Village** — *Hazard:* rubble piles (brief slow, no damage). *Object/cover:* an overturned market cart and stalls; a well as a central landmark. *Building:* single-doorway houses (funnel/chest rooms); the church is large enough to double as an Elite Den or Miniboss Room. *Trap:* a hanging lantern rig — shoot it down for a small fire AoE on whatever's underneath. *Puzzle:* strike a boarded-up well to lower the bucket and reveal hidden loot.
- **Frozen Homestead** — *Hazard:* icy patches (momentary reduced traction, no damage). *Object/cover:* frozen hay bales and a broken sleigh. *Building:* the barn (chest/Miniboss room); the farmhouse (single-door funnel). *Trap:* icicles hanging from the barn eaves — strike them to drop damage on whatever's below. *Puzzle:* shatter a frozen water trough to release warm steam that heals whoever's standing near it.
- **Sunken Mill Town** — *Hazard:* flooded street sections (brief slow, no damage). *Object/cover:* the half-submerged mill wheel; a beached rowboat. *Building:* the mill (chest room); the sunken chapel (narrow flooded funnel). *Trap:* a rickety plank bridge — collapses under weight, minor fall damage to whoever's on it when it goes. *Puzzle:* strike the mill wheel to open a floodgate, draining a section and exposing a loot cache.

### Floor 3

| Biome | Setting | Twist |
| --- | --- | --- |
| Moonlit Graveyard | Fog-bound graveyard | Fog thickens further as a room's cycle advances toward night, cutting vision hardest here — terrain awareness matters more than reflexes |
| The Catacombs | An underground crypt maze | No fog, but tight sightlines from actual wall geometry instead — the same vision-limited feel, achieved structurally rather than by weather |
| Witch's Bog | A fog-bound, toxic wetland | Fog plus a lingering toxic haze that pairs with Blight builds, the way the Village pairs with Thorns/Blight |

- **Moonlit Graveyard** — *Hazard:* denser local fog patches (further vision dip, no damage). *Object/cover:* mausoleums and rows of headstones. *Building:* a crypt (chest room); a small chapel (special-enemy encounter room). *Trap:* a creaky iron gate — swings on a strike, knocking back anything caught in its arc. *Puzzle:* strike a cracked tombstone to reveal a hidden staircase shortcut.
- **The Catacombs** — *Hazard:* uneven floor sections (brief stumble, no damage). *Object/cover:* stacked bone piles and sarcophagi. *Building:* a burial chamber (chest room); a narrow ossuary corridor (funnel). *Trap:* a loose rubble pile — strike it to collapse the passage behind you, sealing off pursuers. *Puzzle:* strike a sealed sarcophagus lid to open a secret passage.
- **Witch's Bog** — *Hazard:* a toxic haze patch (small DoT tick if lingered). *Object/cover:* gnarled roots and dead trees. *Building:* a witch's hut (chest room); an old watch post (funnel point). *Trap:* a bubbling cauldron — strike it to release a damaging cloud onto enemies caught in it. *Puzzle:* strike a row of hanging charms to dispel a ward blocking the path.

### Floor 4

| Biome | Setting | Twist |
| --- | --- | --- |
| Blood Moon Sanctum | Endgame ritual site | Highest base density, built around multiple Ritual Site nodes rather than one |
| The Hollow Cathedral | A ruined cathedral overrun by the cult | Same endgame density, built around vertical sightlines (balconies, a central nave) instead of ritual-site sprawl |
| Reaver's Keep | A collapsing castle | Same endgame density, name-tied to the Blood Moon Reaver boss for a thematic capstone |

- **Blood Moon Sanctum** — *Hazard:* drifting ember patches (small damage tick if lingered). *Object/cover:* ritual braziers and standing altar stones. *Building:* ritual chambers (Miniboss/chest rooms); the inner sanctum (boss arena). *Trap:* rigged ritual chains — strike to swing them into anything standing nearby. *Puzzle:* strike the central altar to break a ward sealing off the next Ritual Site.
- **The Hollow Cathedral** — *Hazard:* crumbling floor sections (brief stumble, no damage). *Object/cover:* rows of pews and pillars; shattered stained glass on the floor is pure scene accent. *Building:* a bell tower (vertical special room); the sacristy (chest room). *Trap:* a hanging chandelier — shoot it down onto whatever's below. *Puzzle:* strike the organ pipes to open a crypt door beneath the altar.
- **Reaver's Keep** — *Hazard:* small rubble-collapse zones (brief dust burst, no real damage). *Object/cover:* broken battlements and siege debris. *Building:* the armory (chest room); the throne hall (boss antechamber). *Trap:* a rigged portcullis — strike it to drop on pursuing enemies. *Puzzle:* strike the throne room's banner/seal to reveal a hidden passage shortcut.

## Meta-Progression & Unlocks

- **Persistent currency:** Silver Shards earned per run (kept even on a loss) spend in the Hunter's Lodge hub between runs.
- **Permanent unlocks:** new hunters/Bloodlines, permanent stat upgrades (max HP, damage, pickup radius), new Secondary weapons and modifier-pool cards over time.
- **Unlock Tracks:** hunter-specific milestone rewards, see Player Character & Progression.
- **Replayability hooks:** run-specific challenge modifiers unlock secret hunters or floors once cleared.
- **Endless Mode:** clearing a floor's boss for the first time unlocks that floor's Endless variant — no timer, escalating forever, a high-score chase. Clearing all four floor bosses unlocks **Eternal Night** — endless, drawing enemies from all four floors at once.

## Art, Audio & Tone

**Visual style:** pixel art with chibi-proportioned sprites, close to Vampire Survivors' readability, but pushed toward a darker horror palette — deep blues and purples for the night, warm firelight and silver-white for weapon effects, so enemy silhouettes and projectiles stay legible against a busy screen. **VFX render at native (non-pixelated) resolution** rather than snapping to the pixel grid — trails, glows, beams, and particles are smooth, deliberately breaking from the sprite layer's pixel-art rendering the way a modern pixel-art game lets lighting or particles run at full resolution over blocky sprites. This is an intentional contrast, not a mismatch: chunky, readable pixel characters and terrain anchor the world, while smooth, high-resolution VFX carry the escalating magical chaos on top of it (see Power-scaled VFX, below). **Main visual style reference: Terraria** (more references may be added later).

**Audio:** distant howls layered into the ambience, a tense string-and-drum loop that intensifies as the Moon Meter rises, and chunky, satisfying hit/kill sound effects to keep large-scale combat feeling responsive.

**Power-scaled VFX:** every weapon's visual effect — trail width, glow intensity, particle count, screen shake, impact flash — scales with the attack's current power, not just its base rarity: stacked modifiers (Twinned Shot, Cascading Fork), Might stacks, crit tier, and Rare/Super Rare upgrades all feed the same visual budget. Because power climbs with a room's Moon Meter (tougher enemies, denser stacks, better loot the longer you stay), the screen reads as calm and readable by Day and builds toward genuine color chaos by Night and especially a Blood Moon — the VFX becomes a second, purely visual indicator of how far you've pushed a room's escalation, reinforcing the Moon Meter's risk/reward tension rather than just looking cool. Each Secondary weapon and primary-weapon modifier category gets its own consistent hue (e.g. Blight = sickly green, Ward/Thorns = pale blue, Might = deep red, Arcane Beam = violet) so that even at max chaos, a player can still parse *what's* hitting *what* by color alone — this is the one hard constraint on the chaos, since it protects the "read the fight, don't just watch it" design intent (see Core Gameplay Loop) even at Blood Moon density. Exact particle budgets and a performance cap for 4-player co-op are a later technical pass, not decided here.

**Tone:** gothic horror-adventure rather than comedic — closer to a monster-hunting folk tale than a joke-heavy romp.

## Platform, Scope & Technical Plan

- **Target platform:** PC (Steam) first, with local and online multiplayer built in as a core feature; mobile port stays on the backburner until the core loop and netcode are proven.
  - **Multiplayer scope:** both local (same-screen) and online co-op — up to 4 players — are in scope from the start, which adds real netcode work — synchronizing enemy spawns/positions, shared XP and pickups, drop-in/out — on top of the base survivor loop.
- **Engine:** Godot or Unity 2D — both are lightweight enough for a solo or small-team build and have strong support for the bullet-hell-scale enemy counts this genre needs; both also have workable networking layers (Godot's high-level multiplayer API, Unity Netcode for GameObjects) worth prototyping early given the multiplayer requirement.
- **Scope:** the core loop (movement, auto-attack weapons, leveling, wave spawning) is a proven, well-documented pattern, but multiplayer synchronization (enemy state, shared pickups, drop-in/out) is the real technical risk here and is worth a small networking prototype before committing to more content, rather than bolting it on late.
- **Milestones:** single-player vertical slice (1 floor, 1 hunter, 5 weapons) → local multiplayer prototype → online multiplayer prototype → full weapon/enemy roster → all 4 floors → meta-progression and balancing pass → Early Access.

## Monetization & Release Plan

- **Model:** one-time premium purchase (~$4.99–$9.99), matching the genre norm set by Vampire Survivors and its peers — no ads, no in-run purchases.
- **Post-launch:** optional paid content packs (new hunter, weapon set, and floor per pack), plus free balance patches.
- **Release path:** Steam Early Access to gather balance feedback on the Moon Meter curve before a 1.0 launch, followed by a mobile port evaluation.
