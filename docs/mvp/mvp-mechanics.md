# MVP Mechanics

2026-09-22 23:03

Companion to [`mvp-design-doc.md`](mvp-design-doc.md). That document is vision and constraints — what the prototype is for and what it deliberately leaves out. This document is the concrete how: controls, stats, formulas, and the moment-to-moment loop, so the vision doc doesn't get cluttered with numbers and stays focused on the goal.

## Controls

| Input | Action |
| --- | --- |
| WASD / left stick | Move |
| Mouse / right stick | Aim |
| — | Weapon auto-fires once aimed |

Subject to change with prototyping.

## Core Stats & Combat Resolution

- **Core stats:** HP, Armor, Damage, Movement Speed, Mana, Pickup Radius, Crit Chance, Cooldown Reduction. Weapon-specific: Projectile Size, Projectile Speed, Projectile Path, Fire Rate, Damage, Damage Zone Size, Damage Zone Shape, Bounce. Some of these are hidden from the player rather than shown on a stat screen.
- **Combat resolution:** flat damage minus Armor reduction, applied straight to HP. No miss chance — every hit connects and resolves.
- **Aim model:** manual aim — the player aims the weapon themselves.
- **Primary weapon:** locked to the player character, never removed. All build depth in this prototype comes from modifiers stacking onto this one weapon.

## Weapons & Modifiers

The full Modifier pool from `game-design.md` applies here — physical properties on the weapon's projectile/effect (velocity & size, trajectory, split & multiply, terminal behavior, exotic, impact & damage shape), each carrying a real tradeoff, with Common / Rare / Super Rare rarity tiers. This system *is* the thing being prototyped, so it's kept intact rather than trimmed.

## Enemy Archetypes

Three distinct combat problems, not yet fleshed out as specific content:

- A fast, low-HP melee rusher — also the prototype's "punching bag": low-threat enough that a player can feel their current build actually working, not just survive it.
- A ranged threat that punishes standing still.
- A slow, tanky, space-controlling enemy.

Chosen to exercise different parts of the combat/modifier system (raw movement/positioning, aim-under-pressure, and pierce/AoE value) with minimal AI scope. If all three end up feeling equally threatening in testing, that's worth flagging.

## Arena

- **Shape:** a square, fully visible at once — no blocked overview, the whole play space is readable at a glance.
- **Boundary:** invisible walls at the square's edge (solid, not a death zone, no wrap); black emptiness rendered past the boundary.
- **Cover:** a few simple stone blocks placed randomly across the square. They block movement and projectiles, but not line of sight.
- **Regeneration:** the block layout is replaced with a new random set at the start of every wave.

## Wave Loop & Progression

- Enemies spawn in waves. Each wave runs **1 minute** and is harder than the one before it.
- Surviving a wave triggers an **upgrade draft: pick 1 of 3** modifier options, drawn from the current pool of unlocked modifiers.
- After the draft, the player respawns immediately into the next wave — new 1-minute timer, increased difficulty, and a freshly randomized block layout.
- Dying ends the run and triggers a **meta draft: pick 1 of 5** unlock options. The chosen unlock is added permanently to the pool of modifiers available in future runs' 3-choice wave drafts. This persists across runs — it is meta-progression, not a within-run-only mechanic (see `primary-design-document.md`'s Out of Scope section for what's still excluded).

## Win/Lose Condition

No fixed win condition — the run continues wave after wave, escalating in difficulty, until the player dies. **Lose condition:** HP reaches 0, run ends and the death draft (above) fires.
