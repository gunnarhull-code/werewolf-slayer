# Werewolf Slayer — Game Design Plan

2026-09-17

## Concept & Elevator Pitch

**Werewolf Slayer** is a top-down horde-survival roguelite in the Vampire Survivors mold: a cursed hunter stands against endless waves of werewolves and their monstrous kin, armed with a primary weapon they aim themselves, backed by secondary weapons that auto-fire, in a fight built around positioning and reading enemies rather than just circling and holding a direction.

**Premise:** A silver-blooded hunter is bound to a cursed forest that floods with lycanthropes every full moon. Each run is one night's stand against the infestation.

**The hook — the Moon Meter:** A meter fills as the run progresses, driven by both time and kill count. At each threshold, ordinary Wolves begin turning into full Werewolves mid-fight, fog rolls in and reduces vision, and spawn density spikes. This creates a risk/reward tension Vampire Survivors doesn't have: killing fast earns XP faster but also fills the Moon Meter faster, so the player is always trading immediate power for a harder back half of the run.

## Core Gameplay Loop

- **Controls:** movement (WASD / left stick) is separate from aim (mouse / right stick). Weapons auto-fire once you're aimed — no separate fire button — except on hunters with an Auto-Aim trait, who skip aiming entirely and play closer to a classic auto-battler.
- **Primary weapon:** locked to each hunter from the start and never removed. This is where the game's buildcrafting depth lives — modifiers stack onto it (see Weapons, Modifiers & Builds).
- **Secondary weapons:** 2–3 additional slots found during a run. These auto-fire and auto-target the nearest enemy, giving the classic screen-filling spectacle as a support layer rather than the main skill expression.
- **Active Ability:** one equipped slot (a 2nd unlocks later), manually triggered with a cooldown — a heal, a block, a knockback, a dash, a team buff, not just a bigger version of your stats. Swapped only at Ability Cache checkpoints (see Checkpoints & Route System); each swap replaces the current Active permanently.
- **Moon Phases:** the run's timer is broken into phases — Waxing → Full → Waning → Blood Moon — tied to the Moon Meter. Each transition automatically adds a Corruption card to the deck (no choice involved) and triggers a checkpoint: a pause to choose the next stretch of the run from the route pool.
- **Session length:** 15–20 minutes for a standard run; Endless Mode removes the timer entirely (see Meta-Progression & Unlocks).
- **Win condition:** survive the full timer and defeat the final boss. **Lose condition:** HP reaches 0 — Silver Shards and unlocks earned that run are still banked.
- **Design intent:** the aim requirement, capped enemy density, telegraphed attacks, and terrain-driven stages (see Enemies & Wave Design, Stages & Environments) all serve one goal — reward reading a fight and positioning, not circling and holding a direction. Status effects (see Status Effects & Builds) extend that same intent to 4-player co-op, so builds create real teamwork rather than four people surviving in parallel.

**Numbers & rarity convention:** flat bonuses are small whole numbers (**+2 damage**); scaling effects are shown as a factor (**x1.4 damage**); true chance is a percentage (**25% chance**); a guaranteed payoff is cadence-based (**every 4th hit**). Randomly-drawn content (modifiers, Actives, Corruption cards) also carries a rarity tier — Common / Rare / Super Rare — where a higher tier adds a genuinely new effect on top of the base card, not just a bigger number. Exact drop rates are a balancing-pass question, not fixed yet.

## Player Character & Progression

- **In-run leveling:** kills drop Silver Shards (XP); filling the bar offers a draft of 3 cards from the run's deck (see Weapons, Modifiers & Builds).
- **Bloodlines:** picked at run start, each Bloodline locks in a starting weapon (never removed — it's the character's identity), 3–5 Bloodline signature cards (including a capstone), and a distinct personality that colors card-draft lines and Cursed Voice encounters.

| Hunter | Bloodline | Locked Weapon | Trait | Voice |
| --- | --- | --- | --- | --- |
| The Ranger | Silver Line | Silver Crossbow | Auto-Aim | Disciplined, clinical — *"Efficient. I'll take it."* |
| The Ferox | Moon-Touched | Blessed Chain Whip | Manual aim | Hungry, seduced by the curse — *"I can feel it... good."* |
| The Warden | Warded | Holy Water Flask | Manual aim | Weary, dutiful — *"Another ward. Another night survived."* |

Wolfsbane Bomb, Silver Buckshot, and Moonlight Lantern make up the current Secondary Weapon pool (see Weapons, Modifiers & Builds) — found during runs, not locked to any hunter.

**No item is class-restricted.** Every modifier, Secondary weapon, and Active is available to every Bloodline (see Weapons, Modifiers & Builds and Active Abilities) — nothing in the draft pool checks which hunter you're playing. A Bloodline's edge is that its locked weapon starts partway upgraded already, so it reaches a given power level in fewer drafted cards than another Bloodline building toward that same level from scratch. The class identity is inherent to the starting weapon and signature cards, not a restriction on what you can later equip.

- **Unlock Tracks:** each hunter has a short set of milestones only completable by playing them — a 6th signature card, an alternate weapon skin, a bio fragment advancing their story. Example, The Ranger: survive to Blood Moon → unlock *Relentless Volley* signature card; land Silver Cascade in a completed run → alternate Crossbow skin; crit-kill an Alpha Werewolf → bio fragment.

## Weapons, Modifiers & Builds

**Primary weapon:** locked to each hunter (see Player Character & Progression) and never removed — everything below stacks onto it.

**Modifier pool** — a curated set of 30 physical properties on your primary weapon's projectile or effect, drawn on level-up alongside Bloodline signature cards. The pool is universal — every modifier applies to every primary weapon, reinterpreted in that weapon's own flavor (a trajectory modifier becomes the Whip's swing arc rather than a projectile path). Every base card carries a real tradeoff, never a pure number-up — though a Rare or Super Rare roll can shed or soften that tradeoff as part of its upgrade (see Rarity, below):

| Category | Examples |
| --- | --- |
| Velocity & Size | Fleetfang Rounds (+2 speed, -1 damage) · Heavy Slugs (+3 size, -1 speed) · Whisper Rounds (-1 size, +2 speed, dimmed hit-flash) · Longshot Barrel (+3 range, -1 size) · Momentum Rounds (damage scales with distance traveled, capped; no bonus at point-blank) |
| Trajectory | Serpent's Path (sine wave) · Spiral Rounds (corkscrews outward) · Falling Star (arcs down, small AoE on landing) · Wandering Shot (drifts toward the nearest enemy mid-flight, -1 speed) · Skipping Stone (bounces along the ground in short hops, losing a little damage each hop) |
| Split & Multiply | Cloverleaf Split (splits into 3 on impact) · Twinned Shot (x2 projectiles) · Cascading Fork (splits again on each split's hit, capped at 2 generations) · Echo Rounds (every 3rd shot fires a delayed echo copy at half damage) · Shattershot (splits into 5 weak fragments in a wide cone instead of one strong hit; each can crit independently) |
| Terminal Behavior | Ricochet Silver (bounces off the arena edge once) · Wolf's Return (boomerangs back along its path) · Deep Bite (+1 pierce, half damage on the pierced hit) · Lingering Wound (leaves a small damage zone at the impact point for a few seconds; less initial hit damage) · Anchor Shot (roots the target briefly on hit; the projectile itself deals no direct damage) |
| Exotic | Orbiting Fang (circles you once, then launches at the nearest enemy) · Chain Howl (leaps to the nearest enemy on kill) · Phase Round (passes through the first enemy harmlessly; damage starts from the second hit onward) · Gravity Well (impact briefly pulls nearby enemies toward it; travels slower) · Mirror Shot (fires a shadow-copy at a slight offset; both copies share one pool of bounces/pierces rather than doubling them) |
| Impact & Damage Shape | Widening Impact (damage radius grows with distance traveled; slightly lower base damage) · Focused Point (no AoE at all; +3 flat damage on direct hits) · Arc Slash (damage sweeps in a narrow arc instead of a circle, hitting a line of enemies) · Chain Spark (a weaker spark jumps to one nearby enemy, but only on a crit) · Cratering Blast (a short delay before impact; notably larger AoE when it lands) |

**Secondary weapons** — 2–3 equip slots, found during a run, always auto-fire and auto-target the nearest enemy (no aim needed): **Wolfsbane Bomb** (delayed AoE explosion), **Silver Buckshot** (short-range cone burst), **Moonlight Lantern** (passive damaging aura, grows with level).

**Bloodline signature cards** — 3–5 per Bloodline, guaranteed in that Bloodline's deck, always thematic, capped by a capstone. Silver Line example:

- Silver Fang Rounds — 15% crit chance
- Piercing Volley — +1 pierce
- Twin Barrel — x2 projectiles
- Marksman's Focus — +2 damage after holding still 1s
- *Silver Cascade* (capstone) — every 4th crit fires a free ricochet bolt

**Active Abilities** — a separate 4th card category, filling one equipped slot (a 2nd unlocks later), manually triggered with a cooldown. Deliberately varied in role, not just bigger stat payoffs:

| Role | Examples |
| --- | --- |
| Offense/Burst | Overwhelm (consume all Might for one devastating hit) · Toxic Bloom (detonate all Blight stacks in an AoE) |
| Defense/Survival | Moonlit Ward (3s full invincibility) · Second Wind (instant heal + regen) · Iron Hide (flat damage reduction, 5s) |
| Control | Howling Blast (knockback wave) · Silver Snare (roots enemies briefly) · Blinding Flare (nearby ranged enemies lose accuracy) |
| Mobility | Wolf's Leap (short dash/blink) · Moonlit Step (dash that leaves a damaging trail) |
| Support | Rally Cry (buff nearby allies) · Guardian's Pulse (grant Ward to nearby allies) · Cleansing Light (strip a debuff or active Corruption downside from an ally) |

Actives are drawn uniformly at random from the full shared pool — not filtered or weighted by class or current build — and swapped only at Ability Cache checkpoints (see Checkpoints & Route System); a swap replaces the current Active permanently.

**Rarity:** modifiers, Actives, and Corruption cards can roll at Common, Rare, or Super Rare. A higher tier isn't just a bigger number — it adds a genuinely new effect on top of the base card, and can shed or soften the base card's downside as part of that upgrade (e.g. Rare Toxic Bloom might add a secondary burst; Super Rare Toxic Bloom might also lose the base card's cooldown penalty). This still has to stay balanced card by card, not a blanket free upgrade. Drop rates are a balancing-pass question, not fixed yet.

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
| Ward Sigil | Negates the next debuff applied to you, including a Corruption card's downside |

**Example builds:**

- **Blight (Trapper-style):** Wolfsbane Coating (hits apply 2 Blight) → Festering Wound (Blight ticks twice as often below half HP) → Spreading Rot (Blight spreads to nearby enemies on a Blighted kill) → capstone *Plague Lord* (Blight stacks uncapped; max-stack enemies explode).
- **Ward/Thorns (Warden-style):** totems grant nearby allies Ward on a timer → Barbed Plating (+Thorns while Ward is active) → Unyielding (Ward regenerates faster while standing still) → capstone *Bulwark of the Pack* (Ward that would break instead bursts into Thorns damage).

**Team synergy:** Marked applied by one player boosts everyone's damage on that target; Ward can be cast on an ally, not just yourself. A run's best moments should come from status roles clicking together — someone marking priority targets, someone tanking with Ward/Thorns, someone finishing with Might — not four players circling in parallel.

## Checkpoints & Route System

Every Moon Phase transition pauses the run briefly and offers 2–3 next-phase choices, drawn from one weighted pool — this is the run's main strategic branching, on top of in-combat positioning:

| Node | Rarity | Effect |
| --- | --- | --- |
| Elite Den | Common | Tougher upcoming wave, guaranteed loot |
| Shrine | Common | A free, curse-free card draft |
| Merchant | Common | Spend Silver Shards |
| Ritual Site | Uncommon | Hold the point (solo or as a group) through a focused wave for a strong reward |
| Sanctuary | Uncommon | Partial heal, slower spawns |
| Ability Cache | TBD (uncommon–rare) | Offered 2 random Actives; swap one for your current Active, or keep it — a permanent, one-way trade |
| Cursed Voice | Rare | A wolf-spirit offers a Corruption card bargain — **Accept** (power + cost + reactive dialogue), **Refuse** (small shard consolation), or **Question** (a softer boon instead). Moon-Touched gets an extra **Embrace** option (softened cost); Warded gets a **Cleanse** option (burn an existing Corruption card instead) |

**Reward scaling:** checkpoint and loot rewards get juicier as the run goes on — later Moon Phases roll better rarity odds, bigger Silver Shard payouts, and stronger node rewards (Elite Den loot, Ritual Site prizes) than the same node type early in the run, so the risk/reward curve keeps climbing alongside the difficulty rather than flattening out.

**Build-weighted draws:** card draws (level-up drafts, Shrine offers) lean slightly toward modifiers and cards that synergize with what the player has already picked, rather than a pure uniform roll — a soft nudge, not a hard pity system, so a build can come together without being fully RNG-dependent.

Moon Phase transitions (Waxing → Full → Waning → Blood Moon) also automatically add a Corruption card to the deck, independent of the checkpoint choice — the curse is simply what the night does to you. Burns, granted by Alpha Werewolf kills, are the only way to remove a card from the deck — including a Corruption card.

## Enemies & Wave Design

- **Base enemies:** Feral Wolf (fast, weak, baseline) · Werewolf (a Wolf that's turned as Moon Phases advance — tankier, hits harder) · Bat Swarm (erratic movement) · Cultist (ranged, punishes standing still) · Ghoul (slow, high HP, area denial).
- **Elites & bosses:** Alpha Werewolf (mini-boss, spawns at each Moon Phase transition, drops a burn on kill) · Blood Moon Reaver (stage boss, run timer's end).
- **Telegraphed attacks:** dangerous hits (an Alpha's lunge, a Werewolf's howl-marked target) flash or wind up before landing — dodging should be a read-and-react skill, not passive movement.
- **Density:** baseline enemy counts stay well below the genre's usual screen-filling swarm — real threats you can read, not wallpaper. True swarm chaos is reserved for deliberate spikes (Elite Den, Blood Moon phase), not the constant state.
- **Curve:** driven by Moon Phase progression (Waxing → Full → Waning → Blood Moon) rather than a flat timer alone — each phase both escalates the fight and adds a Corruption card, so difficulty and deck pressure rise together.

## Stages & Environments

| Stage | Setting | Stage-specific twist |
| --- | --- | --- |
| Cursed Forest | Moonlit woods, the starting stage | Open sightlines, gentlest curve — a few loose chokepoints to learn the positioning game |
| Abandoned Village | Burned-out town | Tight chokepoints and house walls actively shape fights — funnel Werewolves through doorways into Thorns/Blight builds |
| Moonlit Graveyard | Fog-bound graveyard | Fog thickens further with each Moon Phase, cutting vision hardest here — terrain awareness matters more than reflexes |
| Blood Moon Sanctum | Endgame ritual site | Highest base density, built around multiple Ritual Site nodes rather than one — unlocked after clearing the other three once |

Each stage is unlocked by clearing the previous one, giving light structure to first-time progression before the game opens up to free stage select. Terrain is a deliberate tool everywhere, not just Abandoned Village — every stage should give players a reason to choose *where* to fight, not just *when* to move.

## Meta-Progression & Unlocks

- **Persistent currency:** Silver Shards earned per run (kept even on a loss) spend in the Hunter's Lodge hub between runs.
- **Permanent unlocks:** new hunters/Bloodlines, permanent stat upgrades (max HP, damage, pickup radius), new Secondary weapons and modifier-pool cards over time.
- **Unlock Tracks:** each hunter has a short set of hunter-specific milestones (see Player Character & Progression) — only completable by playing them — that unlock a 6th signature card, a cosmetic, or a story fragment.
- **Replayability hooks:** run-specific challenge modifiers unlock secret hunters or stages once cleared.
- **Endless Mode:** clearing a stage's boss for the first time unlocks that stage's Endless variant — no timer, escalating forever, a high-score chase. Clearing all four stage bosses unlocks **Eternal Night** — endless, drawing enemies from all four stages at once.

## Art, Audio & Tone

**Visual style:** pixel art with chibi-proportioned sprites, close to Vampire Survivors' readability, but pushed toward a darker horror palette — deep blues and purples for the night, warm firelight and silver-white for weapon effects, so enemy silhouettes and projectiles stay legible against a busy screen.

**Audio:** distant howls layered into the ambience, a tense string-and-drum loop that intensifies as the Moon Meter rises, and chunky, satisfying hit/kill sound effects to keep large-scale combat feeling responsive.

**Tone:** gothic horror-adventure rather than comedic — closer to a monster-hunting folk tale than a joke-heavy romp.

## Platform, Scope & Technical Plan

- **Target platform:** PC (Steam) first, with local and online multiplayer built in as a core feature; mobile port stays on the backburner until the core loop and netcode are proven.
  - **Multiplayer scope:** both local (same-screen) and online co-op — up to 4 players — are in scope from the start, which adds real netcode work — synchronizing enemy spawns/positions, shared XP and pickups, drop-in/out — on top of the base survivor loop.
- **Engine:** Godot or Unity 2D — both are lightweight enough for a solo or small-team build and have strong support for the bullet-hell-scale enemy counts this genre needs; both also have workable networking layers (Godot's high-level multiplayer API, Unity Netcode for GameObjects) worth prototyping early given the multiplayer requirement.
- **Scope:** the core loop (movement, auto-attack weapons, leveling, wave spawning) is a proven, well-documented pattern, but multiplayer synchronization (enemy state, shared pickups, drop-in/out) is the real technical risk here and is worth a small networking prototype before committing to more content, rather than bolting it on late.
- **Milestones:** single-player vertical slice (1 stage, 1 hunter, 5 weapons) → local multiplayer prototype → online multiplayer prototype → full weapon/enemy roster → all 4 stages → meta-progression and balancing pass → Early Access.

## Monetization & Release Plan

- **Model:** one-time premium purchase (~$4.99–$9.99), matching the genre norm set by Vampire Survivors and its peers — no ads, no in-run purchases.
- **Post-launch:** optional paid content packs (new hunter, weapon set, and stage per pack), plus free balance patches.
- **Release path:** Steam Early Access to gather balance feedback on the Moon Meter curve before a 1.0 launch, followed by a mobile port evaluation.
