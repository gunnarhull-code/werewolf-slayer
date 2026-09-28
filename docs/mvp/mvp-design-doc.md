# MVP Design Doc

2026-09-22 23:03

A minimalist, MVP-scoped design document for the first playable prototype of Werewolf Slayer — one level, one character, single player. This document is vision and constraints only: what the prototype is for and what it deliberately leaves out. Concrete controls, stats, formulas, and the wave/draft loop live in [`mvp-mechanics.md`](mvp-mechanics.md). Full long-term scope (multiplayer, meta-progression, multiple floors, route map, curses, etc.) lives in [`game-design.md`](../game-design.md); this document exists only to define what gets built first.

## Top-Level Design Description

This prototype is a top-down, single-player horde-survival combat sandbox: a player character fights off waves of enemies in one arena, using a primary weapon they aim themselves and a card-draft system that stacks physical modifiers onto that weapon as they level up. **Player fantasy:** a lone fighter standing against overwhelming, escalating odds, growing more capable through their own build choices rather than external help — every other design decision in this prototype should serve that feeling. This prototype exists to answer one question: **is the core combat loop — aiming, positioning against telegraphed threats, and building out a weapon through modifier drafts — fun on its own**, before any of the surrounding game (floors, route maps, multiplayer, meta-progression) gets built on top of it.

## Design Pillars

| Pillar | Why it matters here |
| --- | --- |
| **Sensation** | Combat needs to feel visceral hit-to-hit — satisfying hit-flash, sound, and impact feedback — independent of any build depth. If the base combat doesn't feel good, no amount of modifier depth will save it. |
| **Challenge** | The aim requirement plus telegraphed enemy attacks should reward reading a fight and positioning rather than circling and holding a direction — this is the thing being tested above all else. |
| **Discovery** | The modifier draft system should make each run's build feel like a genuine discovery — different modifier combinations should meaningfully change how the weapon plays, not just how big its numbers are. Concretely: a run should be able to find at least one *mechanical* adjustment (changes what the weapon does — trajectory, split, terminal behavior) and combine it with a *number* adjustment (changes a stat) into a combo that feels different from either alone, not just a pile of stat-up cards. |
| **Low cognitive load** | This prototype exists specifically to test combat and the modifier system in isolation — no tutorial text, no lore, no UI complexity beyond what's needed to read the fight and pick a card. Every other system already cut in Out of Scope is partly in service of this: fewer things competing for the player's attention makes it easier to tell whether the *combat itself* is the problem when something doesn't feel good. |

## Retention Principles Carried From the Full Design

The full design's [Design Pillars — What Keeps Players Coming Back](../game-design.md#design-pillars--what-keeps-players-coming-back) are the guiding forces for the whole game, not something layered on after the prototype — this MVP should already read as an instance of them:

- **Legible variance:** the wave draft (pick 1 of 3, drawn from the unlocked Modifier pool) is the same predictable-shape/surprising-content draft as the full design — nothing scaled down here.
- **Compounding power, not additive power:** stacking Modifiers should read as acceleration, not a flat climb, even with just the base Modifier pool and no status layer yet — this is core to what the Discovery pillar (above) is actually testing.
- **Meta-progression as a safety net against permadeath:** the death draft (pick 1 of 5, permanently added to future runs' pool) is this prototype's version of "a failed run still banks something" — it stays in scope specifically because it's load-bearing for the full game's retention loop, not a nice-to-have.
- **Density as restraint, not spectacle:** the three enemy archetypes (rusher, ranged, tank) stay deliberately sparse rather than swarm-heavy — the same anti-Vampire-Survivors stance as the full design, tested here at its simplest.

**Not yet testable at this scope:** *Build diversity over content volume* needs Bloodline Signature Cards and the status-effect layer (both cut, see Out of Scope) to mean anything — a single weapon and single character can't demonstrate it here. *Long runs, deliberately* is a floor/room-structure decision (also cut) — the wave loop's endless escalation is a different shape entirely and shouldn't be read as validating that pillar one way or the other.

## Audience & Marketing

Not applicable at this stage — this is an internal prototype, not a release candidate, and has no target audience or storefront yet. The eventual audience/platform/monetization plan (PC via Steam, premium one-time purchase, Vampire-Survivors-adjacent roguelite audience) is defined in `game-design.md` and carries over unchanged once this prototype validates the core loop.

## Character Design / Visual Content

Visual style can start as placeholder/programmer art — nothing about the core combat loop depends on final art fidelity. Whatever player character and enemies are used should stay readable at a glance (silhouette and color-coded enough to tell "enemy" from "player" from "projectile" at speed), matching the readability goal already set in `game-design.md`, but a full pixel-art pass is not required to answer this prototype's core question. **Affordance matters even at placeholder fidelity:** the rusher, the ranged threat, and the tanky enemy should each *look* like what they do (small and quick, holding distance, big and slow) — even a gray-box shape communicates intent if its silhouette and movement match its role, and mismatched affordance (a threat that looks harmless, or vice versa) will muddy the combat-feel test.

## Setting & World

One fixed, hand-built arena — a single static space is enough to test combat and the modifier system. No procedural generation, no biome pool, no room tree, no route map, no multiple floors: building generation systems before validating the core loop would be scope creep at this stage (see Out of Scope). See `mvp-mechanics.md` for the arena's concrete shape, boundary, and cover-block behavior.

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
- Day → Night → Blood Moon Moon Meter cycle (the wave loop's per-wave difficulty ramp stands in for it, see `mvp-mechanics.md`)
- Secondary weapons, Active Abilities, Bloodline Signature Cards
- Status effects (Might, Ward, Thorns, Blight, Marked, Hobbled) and the Bloodline Signature Cards / Active Ability tables that depend on them — the base Modifier pool still applies as-is, since none of its example cards reference a status effect by name
- Multiplayer (local or online), co-op-specific mechanics
- Hunter's Lodge, Unlock Tracks, Endless Mode as named systems from `game-design.md` — **meta-progression itself is in scope**: dying triggers a pick-1-of-5 unlock draft that permanently grows the pool of modifiers offered in future runs' wave drafts (see `mvp-mechanics.md`)
- Monetization, release planning

Everything above stays defined in `game-design.md` for later — this document is only the slice needed to build and test the first playable version.
