# Primary Design Document

2026-09-22 22:36

A minimalist, MVP-scoped design document for the first playable prototype of Werewolf Slayer — one level, one character, single player. Full long-term scope (multiplayer, meta-progression, multiple floors, route map, curses, etc.) lives in [`game-design.md`](game-design.md); this document exists only to define what gets built first, and deliberately leaves the rest out.

## Top-Level Design Description

This prototype is a top-down, single-player horde-survival combat sandbox: a player character fights off waves of enemies in one arena, using a primary weapon they aim themselves and a card-draft system that stacks physical modifiers onto that weapon as they level up. **Player fantasy:** a lone fighter standing against overwhelming, escalating odds, growing more capable through their own build choices rather than external help — every other design decision in this prototype should serve that feeling. This prototype exists to answer one question: **is the core combat loop — aiming, positioning against telegraphed threats, and building out a weapon through modifier drafts — fun on its own**, before any of the surrounding game (floors, route maps, multiplayer, meta-progression) gets built on top of it.

## Design Pillars

| Pillar | Why it matters here |
| --- | --- |
| **Sensation** | Combat needs to feel visceral hit-to-hit — satisfying hit-flash, sound, and impact feedback — independent of any build depth. If the base combat doesn't feel good, no amount of modifier depth will save it. |
| **Challenge** | The aim requirement plus telegraphed enemy attacks should reward reading a fight and positioning rather than circling and holding a direction — this is the thing being tested above all else. |
| **Discovery** | The modifier draft system should make each run's build feel like a genuine discovery — different modifier combinations should meaningfully change how the weapon plays, not just how big its numbers are. Concretely: a run should be able to find at least one *mechanical* adjustment (changes what the weapon does — trajectory, split, terminal behavior) and combine it with a *number* adjustment (changes a stat) into a combo that feels different from either alone, not just a pile of stat-up cards. |
| **Low cognitive load** | This prototype exists specifically to test combat and the modifier system in isolation — no tutorial text, no lore, no UI complexity beyond what's needed to read the fight and pick a card. Every other system already cut in Out of Scope is partly in service of this: fewer things competing for the player's attention makes it easier to tell whether the *combat itself* is the problem when something doesn't feel good. |

## Audience & Marketing

Not applicable at this stage — this is an internal prototype, not a release candidate, and has no target audience or storefront yet. The eventual audience/platform/monetization plan (PC via Steam, premium one-time purchase, Vampire-Survivors-adjacent roguelite audience) is defined in `game-design.md` and carries over unchanged once this prototype validates the core loop.

## Core Gameplay

- **Controls:** movement is separate from aim (see Controls below). The weapon auto-fires once aimed — no separate fire button.
- **Primary weapon:** locked to the player character, never removed. All build depth in this prototype comes from modifiers stacking onto this one weapon (see Weapons & Modifiers).
- **Core stats:** HP, Armor, Damage, Movement Speed, Mana, Pickup Radius, Crit Chance, Cooldown Reduction. Weapon-specific: Projectile Size, Projectile Speed, Projectile Path, Fire Rate, Damage, Damage Zone Size, Damage Zone Shape, Bounce. Some of these are hidden from the player rather than shown on a stat screen.
- **Combat resolution:** flat damage minus Armor reduction, applied straight to HP. No miss chance — every hit connects and resolves.
- **Leveling:** kills drop XP; filling the bar offers a draft of 3 modifier cards.
- **Weapons & Modifiers:** the full Modifier pool from `game-design.md` applies here — physical properties on the weapon's projectile/effect (velocity & size, trajectory, split & multiply, terminal behavior, exotic, impact & damage shape), each carrying a real tradeoff, with Common / Rare / Super Rare rarity tiers. This system *is* the thing being prototyped, so it's kept intact rather than trimmed.
- **Enemy archetypes:** three distinct combat problems, not yet fleshed out as specific content — a fast, low-HP melee rusher; a ranged threat that punishes standing still; and a slow, tanky, space-controlling enemy. Chosen to exercise different parts of the combat/modifier system (raw movement/positioning, aim-under-pressure, and pierce/AoE value) with minimal AI scope, rather than for any lore reason. The fast/low-HP rusher should double as the prototype's "punching bag" — low-threat enough that a player can feel their current build actually working, not just survive it — while the other two carry the real challenge; if all three feel equally threatening, that's worth flagging during testing.
- **Aim model:** manual aim — the player aims the weapon themselves, testing the full "aim + position + build" loop together rather than isolating any one part of it.
- **Win/lose condition:** no fixed win condition yet — the prototype is meant to be played until the player dies or chooses to stop, purely to test combat feel and build progression. **Lose condition:** HP reaches 0, run ends.

## Controls

| Input | Action |
| --- | --- |
| WASD / left stick | Move |
| Mouse / right stick | Aim |
| — | Weapon auto-fires once aimed |

Subject to change with prototyping.

## Gameplay Balance & Pacing

- There should be some form of escalation over time so the modifier build actually gets tested against rising pressure, not a flat difficulty forever — this could be as simple as enemy spawn rate increasing steadily on a timer, without the full Day → Night → Blood Moon cycle from the main design (that system stays out of scope for this prototype; see Out of Scope, below).
- No formal balance numbers are set here — this is a balancing-pass question once the loop itself is confirmed to be fun.

## Character Design / Visual Content

Visual style can start as placeholder/programmer art — nothing about the core combat loop depends on final art fidelity. Whatever player character and enemies are used should stay readable at a glance (silhouette and color-coded enough to tell "enemy" from "player" from "projectile" at speed), matching the readability goal already set in `game-design.md`, but a full pixel-art pass is not required to answer this prototype's core question. **Affordance matters even at placeholder fidelity:** the rusher, the ranged threat, and the tanky enemy should each *look* like what they do (small and quick, holding distance, big and slow) — even a gray-box shape communicates intent if its silhouette and movement match its role, and mismatched affordance (a threat that looks harmless, or vice versa) will muddy the combat-feel test.

## Setting & World

One fixed, hand-built arena — open sightlines, a few loose chokepoints, and simple cover pieces for basic positioning play. No procedural generation, no biome pool, no room tree, no route map: a single static space is enough to test combat and the modifier system, and building generation systems before validating the core loop would be scope creep at this stage (see Out of Scope). **Signposting the exit:** even with no route map, the arena's own exit (or the point where a playtest session is meant to end) should be visually obvious — light, contrast, or negative space marking it clearly — so confusion about "what do I do now" never contaminates a read on whether the *combat* felt good.

## Tone & Aesthetics

Same tone as the main design: gothic horror-adventure rather than comedic. No specific art direction needs to be locked for this prototype beyond "readable in combat" (see Character Design, above).

## (No) Narrative

None. No dialogue, no story beats — this prototype is combat-and-systems only.

## Business Model

Not applicable — internal prototype, not a shippable or sellable product. The main design doc's business model carries over unchanged once this prototype validates the core loop.

## Out of Scope for This Prototype

Explicitly excluded, to keep this to a true MVP:

- Multiple floors, biome pools, route map/checkpoints, Miniboss Rooms, Floor Bosses
- Room Modifiers (Curse / Flood / Blood Moon), Curse Omen drafts, Random Events
- Day → Night → Blood Moon Moon Meter cycle (a simple spawn-rate ramp stands in for it, see Gameplay Balance & Pacing)
- Secondary weapons, Active Abilities, Bloodline Signature Cards
- Status effects (Might, Ward, Thorns, Blight, Marked, Hobbled) and any modifier cards that depend on them — the base Modifier pool still applies, but any example card referencing a status effect should be swapped for a non-status variant in the prototype
- Multiplayer (local or online), co-op-specific mechanics
- Meta-progression, Hunter's Lodge, permanent unlocks, Unlock Tracks, Endless Mode
- Monetization, release planning

Everything above stays defined in `game-design.md` for later — this document is only the slice needed to build and test the first playable version.
