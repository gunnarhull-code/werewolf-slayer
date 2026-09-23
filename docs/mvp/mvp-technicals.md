# MVP Technicals

2026-09-22

Companion to [`mvp-design-doc.md`](mvp-design-doc.md) and [`mvp-mechanics.md`](mvp-mechanics.md). Where those two cover what the prototype is and how it plays, this covers what it's built with — engine, language, and project layout. These choices are meant to carry forward into the full-scope game in [`../game-design.md`](../game-design.md), not just the prototype; nothing here is MVP-only unless stated.

## Engine & Language

- **Engine:** Godot 4.x (latest stable). Free/open-source, strong 2D renderer, native support for manual mouse/stick aiming, and a built-in high-level multiplayer API (ENet-based) that covers the full game's later local/online co-op plan without needing a third-party networking library.
- **Language:** GDScript. Built into the editor with instant hot-reload and no external build step — the most direct path for working solo, in the editor, without AI assistance. The genre's performance needs (a 2D survivor-like with intentionally capped enemy density, per the design doc) don't require C#'s raw speed, and the GDScript-first tutorial/community ecosystem matters for a solo dev learning the engine.

## Renderer

**Forward+** (Godot 4's default desktop renderer). The MVP and near-term plan target PC only (see `mvp-design-doc.md` / `game-design.md`'s Platform section — mobile is explicitly backburner). Forward+ gives the best visual quality and is the renderer Godot 4 development is centered on. **Revisit before any mobile port**: Godot's Mobile renderer trades some visual fidelity for phone-class GPU performance, and switching later mainly means re-checking shaders/materials for compatibility, not a full rebuild.

## Project Location & Structure

- **Same repository**, not a separate one — a solo project doesn't have the multi-team reasons (separate CI, access control, release cadence) that usually justify splitting code from docs, and keeping them together means a design change and its implementation can land in the same PR when useful.
- **Godot project root:** `game/` at the repo root, alongside `docs/`.
- **Folder layout inside `game/`** (standard Godot convention):
  - `scenes/` — `.tscn` scene files, organized by feature (`player/`, `enemies/`, `arena/`, `ui/`)
  - `scripts/` — `.gd` scripts, mirroring the `scenes/` structure
  - `assets/` — sprites, audio, fonts, organized by type
  - `addons/` — only if a third-party plugin becomes necessary; none anticipated for the MVP
- **Version control:** plain Git (already in use for this repo). Godot's project settings should have `.godot/` (the local editor cache) gitignored — it's regenerated automatically and shouldn't be committed.

## Deferred to Full-Game Scope

Not needed for the MVP (single-player, one arena — see Out of Scope in `mvp-design-doc.md`), but noted here so the engine choice is validated against them:

- **Multiplayer networking:** Godot's High-Level Multiplayer API (`MultiplayerSpawner`, `MultiplayerSynchronizer`) is the intended approach when local/online co-op gets built — no separate networking library needed.
- **Mobile export:** revisit the renderer choice (above) and touch-input handling once a mobile port is actually scheduled.
