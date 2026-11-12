# Living Design Reference & Feature Roadmap

> **ROLE OF THIS DOCUMENT:** This is the **dynamic, living single source of truth** for all active development. While `devlog/game_design_context.md` remains a frozen snapshot of the pre-kickoff concept, **this file must be continuously updated and corrected** by any agent (Antigravity, Cursor, Claude Code, etc.) whenever game directions, scope, mechanics, or architectural choices evolve.

---

## 1. Project Identity & Active Pillars

- **Project Title:** DIRECTOR'S CUT ROGUELIKE
- **Core Concept:** Fast-paced action roguelite set within a chaotic B-movie production. The player plays an expendable action lead / stunt performer whose primary weapon is the **Director's Remote** (diegetic reality editing).
- **Official Jam Theme:** DIRECTOR'S CUT (Theme interpretation: Diegetic cinematic editing + playing out cut scenes / spliced takes).
- **Target Platform:** UEFN (Fortnite Ecosystem) | Single-player 1vE.
- **Current Milestone:** Phase 1: Foundational Sandbox & Remote Core (Day 1 - Jam Active, Kickoff Passed at Nov 12, 12:00 AM ET).
- **Memory Budget Limit:** < 100,000 Spatial Thermo units.

---

## 2. Core Mechanics Status & Technical Matrix

| Mechanic | Status | Key System / Device | Details & Execution Notes |
| :--- | :---: | :--- | :--- |
| **Director's Remote** | `Core Complete (Phase 1.4)` | `edit_remote_device` + Signal Remote Manager | Verse core compiles with SUCCESS. Secondary signal cycles `Cut` / `Freeze Frame`; primary executes active tool and deducts rolls. `Rewind`, `Fast Forward`, and `Plot Armor` enumerated for Phase 3. |
| `CUT! (Scissors)` | `Implemented in Verse (Compiling)` | Verse Spatial Query | Deletes nearest living enemy within 2500 cm and dot product >= 0.45 (2 Rolls, 9999.0 damage). Refunds rolls if no target in sight. |
| `FREEZE FRAME` | `Implemented in Verse (Compiling)` | Spawner Pause / Stun | Temporal stasis on active enemies, disables spawners without despawn, generation counter handles rapid re-casts (1 Roll, 4s duration). |
| `REWIND` | `Planned (Phase 3)` | Circular State Buffer | Rewinds player position and health 3 seconds back in time (2 Rolls). Reverse audio. |
| `FAST-FORWARD` | `Planned (Phase 3)` | Impulse / Velocity Mod | Explosive horizontal dash forward (1 Roll). |
| `PLOT ARMOR` | `Planned (Phase 3)` | Invincibility Buff | Temporary god-mode; weapon shots create cinematic explosions (3 Rolls). |

---

## 3. Narrative & Walkie-Talkie Integration

- **NPC Director:** **Stanley** (1980s eccentric, caffeine-fueled Hollywood action director).
- **Tone:** Fast-talking, neurotic, sarcastic, urgent. English-only 2-sentence radio calls.
- **Integration Device:** Native UEFN `Conversation Device` triggered at Backstage Hub debriefs.
- **Action Item at Jam Start:** Validate live runtime LLM integration mechanics supported in UEFN for the Walkie-Talkie modifier.

---

## 4. Level & Environmental Architecture

- **Topology:** **Fixed-Stage Constellation** (isolated pre-built stage volumes routed via Verse teleporters). Eliminates runtime procedural generation to guarantee 100% NavMesh stability.
- **Stage Classes:**
  1. **Backstage Hub:** Safe staging area, monitor desks, wardrobe/dressing room, director's chair, Film Strip selection station. *(Status: Floor envelope placed, Player Spawner active, diegetic prop palette curated on staging grid).*
  2. **Action Combat Sets:** Thematic arenas (Western Saloon, Cyberpunk Rooftop, Sci-Fi Bay, Noir Alley, Haunted Library, Castle Dungeon). Tight cover, diegetic contrast lighting.
  3. **Stunt & Hazard Sets:** High-speed obstacle courses (ramp leaps, collapsing floors, laser corridors) testing movement editing (*Freeze Frame*, *Fast-Forward*).

---

## 5. Meta-Progression: Film Strip Drafting

- **UI Interface:** Custom modal rendering three 35mm film strips prior to stage transitions.
- **Implementation Strategy:** Preferred via **UMG UI** using Verse UI Kit best practices.
- **Card Pools:**
  - *Modifiers:* Run-specific stat buffs (speed, damage, roll capacity).
  - *Tool Unlocks / Upgrades:* Unlocking advanced tools (`Rewind`, `Plot Armor`) or discounting roll costs.
  - *Scene Booking:* Strategic routing into specific combat or stunt sets.

---

## 6. Decoupled Architecture Modules

1. **`Shared Data & Stage Registry`:** Tool costs, stage IDs, spawner configurations, countdown limits.
2. **`Edit Remote Controller`:** Signal Remote bindings, inventory roll deduction, tool execution pipeline.
3. **`Film Strip UI Controller`:** Viewport card presentation, selection capture, mutator dispatch.
4. **`Scene Flow Router`:** Round cycle management, teleporter routing, win/loss (Take depletion) conditions.

---

## 7. Scope Tracker & Deliberate Scope Cuts ("Director's Cuts")

*Log architectural pivots, feature reductions, and deliberate cuts here to maintain a tight, polished delivery within the 93-hour jam window:*

- **Cut #01 (Pre-Kickoff): Procedural Generation Cut:** Procedural tile generation was cut in favor of a fixed-stage constellation topology with teleporter routing. Prevents AI NavMesh breakdown and unvalidated physics collisions.

---

## 8. Development Phases & Current Progress

- **[>] Phase 1: Foundational Sandbox & Remote Core (ACTIVE)**
  - *Hub Environment:* Floor envelope placed, Player Spawner active, dressing room prop palette curated.
  - *Remote Logic:* `edit_remote_device.verse` compiles cleanly with full `CUT!` (aim dot-product query, refund on miss) and `FREEZE FRAME` (enemy stasis, generation-counter timeout).
  - *Pending Playtest:* Manual wiring of `TestGuardSpawners` to `Hub Guard Spawner` in Details panel; in-session verification pass.
- **[ ] Phase 2: Stage Generation & Scene Flow Infrastructure** *(Modular arena sets, diegetic lighting, Scene Flow Router, Stanley Conversation Device)*
- **[ ] Phase 3: Meta-Progression, Audio & Extended Tools** *(Film Strip UMG UI, `REWIND` circular buffer, `FAST-FORWARD`, audio SFX)*
- **[ ] Phase 4: Validation, Trailer & Submission** *(100% English audit, Glass Box devlog export, Private Version Code generation, 30-60s 1080p trailer)*
