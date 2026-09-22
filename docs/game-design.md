# Werewolf Slayer — Game Design Plan

2026-09-17

## Contents

- [Concept & Elevator Pitch](#concept--elevator-pitch)
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

**Premise:** A silver-blooded hunter is bound to a cursed forest that floods with lycanthropes every full moon. Each run pushes across 4 floors, clearing rooms picked one at a time from a route map until each floor's boss falls and the next floor opens.

**The hook — the Moon Meter:** Each room runs its own Moon Meter, filling as you fight — driven by both time and kill count — and driving that room's Day → Night (a full moon) cycle, with an occasional Blood Moon on top. As it climbs, ordinary Wolves begin turning into full Werewolves mid-fight, fog rolls in and reduces vision, and spawn density spikes. Once you've found a room's exit you can leave through it at any time — but the meter keeps climbing the whole time you stay, so it's a constant bet: pull out now with what you've got, or hold out for better loot and rarity at rising risk. This is the risk/reward tension Vampire Survivors doesn't have: killing fast earns XP faster but also fills the meter faster, trading immediate power for a harder fight the longer you push your luck in that room.

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

**Random Events:** a separate category from the node table above — scripted encounters that can appear as a pickable option on the route map rather than a standard room type. **Cursed Voice** (Rare) is the only one designed so far: a wolf-spirit offers a curse bargain — **Accept** (power + cost + reactive dialogue), **Refuse** (small shard consolation), or **Question** (a softer boon instead). Moon-Touched gets an extra **Embrace** option (softened cost); Warded gets a **Cleanse** option (burn an existing curse instead). More Random Event types are expected but not yet designed.

**Reward scaling:** checkpoint and loot rewards get juicier as you push deeper into a floor's room tree — later rooms roll better rarity odds, bigger Silver Shard payouts, and stronger node rewards (Elite Den loot, Ritual Site prizes) than the same node type early on, so the risk/reward curve keeps climbing alongside the difficulty rather than flattening out.

**Build-weighted draws:** card draws (level-up drafts, Shrine offers) lean slightly toward modifiers and cards that synergize with what the player has already picked, rather than a pure uniform roll — a soft nudge, not a hard pity system, so a build can come together without being fully RNG-dependent.

Burns, granted by Alpha Werewolf kills, are the only way to remove a card from your deck, including a curse.

**Room Omens:** beyond the node-type table above, an individual room can also roll a modifier from a shared pool — **Omens** — that curses are just one entry in. Once a room's Omen is set, the route picker shows an icon on that node from **two or more spaces ahead**, so players get advance warning of what kind of room is coming without full detail yet. Other Omen types raised so far, none fully specified: a "Flood" Omen (effect TBD), and reward-boosting Omens (extra Silver Shards, extra loot — exact form TBD). **Design rule:** any debuff-flavored Omen must carry reward comparable to or greater than a pure-benefit Omen, so risk and reward stay balanced across the whole Omen pool, not just within Curse Omens.

**Curse Omen** (one Omen type): not a per-transition guarantee — each room independently rolls a percentage chance of containing a guaranteed curse (exact odds TBD). Reaching the end of a curse room presents it as a standard card-reward screen — a draft of **3 curse options to choose from**, the same format as a level-up draft, not a single forced card. The curses available across a run are drawn from one **predrawn deck**, generated at run start; in co-op, the deck is shared across the whole party, and a chosen curse can affect everyone, not just the player who picked it. Severity still decides whether a buff comes attached — a major drawback pairs with a real power buff, a minor drawback doesn't.

**Curse pick motivation:** choosing to walk into an Omen'd room in the first place is what's rewarded — a room flagged with an Omen icon typically comes with a better payout attached (extra Silver Shards, better loot, or a benefit baked into the curse card itself) specifically because you knowingly picked the riskier room off the map. The curse draft inside it is still a genuine choice among 3 options, not a tax for entering.

## Enemies & Wave Design

- **Base enemies:** Feral Wolf (fast, weak, baseline) · Werewolf (a Wolf that's turned as a room's Day → Night cycle advances — tankier, hits harder) · Bat Swarm (erratic movement) · Cultist (ranged, punishes standing still) · Ghoul (slow, high HP, area denial).
- **Elites & bosses:** Alpha Werewolf (mini-boss, can spawn as a room's cycle advances, drops a Burn on kill) · a **Floor Boss** caps each floor's room tree — clearing it opens the next floor; the 4th floor's boss, the **Blood Moon Reaver**, ends the run.
- **Telegraphed attacks:** dangerous hits (an Alpha's lunge, a Werewolf's howl-marked target) flash or wind up before landing — dodging should be a read-and-react skill, not passive movement.
- **Density:** baseline enemy counts stay well below the genre's usual screen-filling swarm — real threats you can read, not wallpaper. True swarm chaos is reserved for deliberate spikes (Elite Den, a room's Blood Moon), not the constant state.
- **Curve:** within a room, driven by its Day → Night (Full Moon) → occasional Blood Moon progression rather than a flat timer alone — each transition escalates the fight, and that difficulty compounds again as you push deeper into a floor's room tree.

## Floors & Environments

| Floor | Setting | Floor-specific twist |
| --- | --- | --- |
| Cursed Forest | Moonlit woods, the starting floor | Open sightlines, gentlest curve — a few loose chokepoints to learn the positioning game |
| Abandoned Village | Burned-out town | Tight chokepoints and house walls actively shape fights — funnel Werewolves through doorways into Thorns/Blight builds |
| Moonlit Graveyard | Fog-bound graveyard | Fog thickens further as a room's cycle advances toward night, cutting vision hardest here — terrain awareness matters more than reflexes |
| Blood Moon Sanctum | Endgame ritual site | Highest base density, built around multiple Ritual Site nodes rather than one — unlocked after clearing the other three once |

Each floor is unlocked by clearing the previous one, giving light structure to first-time progression before the game opens up to free floor select. Terrain is a deliberate tool everywhere, not just Abandoned Village — every floor should give players a reason to choose *where* to fight, not just *when* to move.

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
