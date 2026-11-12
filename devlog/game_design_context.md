# UEFN Game Design Document (Living GDD) - 2026 Epic AI MegaJam

> **INITIAL CONCEPT NOTICE:** This document captures the initial pre-kickoff design specification (`GDD SPEC-2026`). Mechanics, scope, tooling approaches, and features remain living targets subject to iteration and deliberate cuts throughout development.

- **Working Title:** DIRECTOR'S CUT ROGUELIKE *(A Fast-Paced Action Roguelite with Real-Time Timeline Editing Mechanics)*
- **Official Jam Theme:** DIRECTOR'S CUT
- **Platform:** UEFN (Unreal Editor for Fortnite / Verse / Creative 2.0)
- **Language Mandate:** 100% English (Voice & Text)
- **Submission Target:** Private Version Code *(redacted/masked in public logs per security policy)*
- **Primary Award Target:** Best Overall UEFN + Modifiers (`WALKIE-TALKIE`, `GLASS BOX`, `SOLO DRIVER`)
- **Memory Budget Target:** < 100,000 Spatial Thermo units
- **High Concept & Theme Angle:** Casts the player as an expendable action lead and stunt performer trapped inside an escalating, chaotic B-movie production. Rather than relying solely on traditional gunplay, the player's primary weapon is the **Director's Remote**—a diegetic timeline-editing controller capable of cutting threats from the scene, freezing action, rewinding dangerous takes, dashing forward, and forcing script immunity.
- **Core Loop:** 5-step Take Progression Cycle (Backstage Hub & Film Strip Draft → Stage Deployment → Live Scene Execution → Scene Wrap / Cut-Reset Resolution → Grand Finale).
- **Key Verse Systems & Fortnite Devices:** Signal Remote Manager, Native UEFN Conversation Device (LLM Walkie-Talkie NPC), Verse Teleporter Routing, Custom Circular State History Buffer, UMG/Verse UI Drafting Cards, Cinematic Sequence & Audio Feedback Devices.
- **Multi-Agent Stack:** Antigravity (Gemini 3.8 Flash), SpaceXSI (Cursor / Grok Bot), Claude, Hyper3D Rodin, Tripo, PBRgen, fal.ai, WeLoveIndies, MCP Server (`uefn-mcp`).

---

## 1. Executive Overview & Strategic Target Matrix

- **Target Awards (4):** Best Overall UEFN + **Walkie-Talkie** (LLM-powered NPC director), **Glass Box** (comprehensive live development log), and **Solo Driver** (single-creator production).
- **Competition Criteria Alignment:**

| Criterion | Targeted Score | Design & Technical Implementation |
| :--- | :--- | :--- |
| **Ambition & Innovation** | Top Tier (5 pts) | Real-time temporal editing mechanics via a customized `Signal Remote Manager`, moving beyond basic weapon sandboxes into active reality editing. |
| **Theme Utilization** | Top Tier (5 pts) | A literal, mechanical embodiment of *Director's Cut*: playing out cut content, spliced sequences, and unreleased takes under real-time directorial edits. |
| **Walkie-Talkie Modifier** | Category Win | Narrative driven by an interactive LLM NPC Director (**Stanley**) utilizing native UEFN Conversation devices, delivering sarcastic scene debriefs over the studio radio. |
| **Glass Box Modifier** | Category Win | Synchronized documentation capturing the AI-assisted pipeline, Verse circular buffer state design, and Model Context Protocol (MCP) modular layouts. |
| **Visuals & Level Design** | High Polish (10 pts) | A hub-and-spoke constellation of stylized movie sets contrasting distinct film genres, visually defined through atmospheric, diegetic lighting. |

---

## 2. Core Gameplay Loop (The Take Progression Cycle)

1. **Backstage Hub (The Director's Chair):** The player spawns in the production studio. The LLM Director calls in over radio to react to the run. The player selects from a 3-choice **Film Strip Draft** (granting game modifiers, editing tools, items, or scene routing).
2. **Stage Deployment:** Teleportation into a self-contained film set (Action Combat Arena or Stunt Sequence).
3. **Live Scene Execution:** Engage threats or complete stunt maneuvers using Fortnite gear augmented by the **Director's Remote** editing powers (consuming *Film Rolls*).
4. **Resolution:**
   - **Scene Wrap (Success):** Rewards bonus *Film Rolls* and triggers a return to Backstage for the next round.
   - **Cut / Reset (Failure):** Costs one *Take*; running out of available Takes ends the production run.
5. **Grand Finale:** Surviving a consecutive series of successful scenes triggers the Final Climax set and rolls the cinematic credits.

---

## 3. Core Mechanic: The Director's Remote

The player holds a non-droppable **Signal Remote Manager** item acting as the primary runtime editing deck:
- **Secondary Fire (Aim / Right-Click):** Cycles forward through the player's array of currently unlocked editing tools, updating the custom HUD in real-time.
- **Primary Fire (Shoot / Left-Click):** Executes the active editing power immediately, deducting the required amount of *Film Rolls* from the player's Verse-managed inventory.

| Tool Name | Roll Cost | Mechanical Effect | Planned Technical Execution |
| :--- | :---: | :--- | :--- |
| **CUT! (Scissors)** | 2 Rolls | Instantly deletes the closest target enemy or obstacle in front of the player. | Spatial query for the closest enemy character within range; triggers elimination with cut-tape visual and sound effects. |
| **FREEZE FRAME** | 1 Roll | Freezes all enemies and environmental hazards in the active stage for several seconds. | Applies brief temporal stun or AI pause to active enemy spawners; activates sepia post-process tint. |
| **REWIND** | 2 Rolls | Rewinds the player's spatial position and health pool back 3 seconds in time. | Continuous circular history buffer sampling player coordinates and health; triggers instant spatial relocation with reverse tape audio. |
| **FAST-FORWARD** | 1 Roll | Launches the player forward with an explosive dash and high-speed momentum. | Applies instant horizontal launch impulse or triggers a temporary speed modulation multiplier. |
| **PLOT ARMOR** | 3 Rolls | Temporary absolute invulnerability; all player weapon shots trigger cinematic explosions. | Applies brief invincibility buff and spawns localized explosive impulses at weapon impact points. |

---

## 4. Narrative Engine & LLM Walkie-Talkie System

- **NPC Director Name:** **Stanley** (integrated through UEFN's native `Conversation Device` powered by an LLM agent).
- **Archetype & Tone:** 1980s eccentric, caffeine-fueled Hollywood action director—neurotic, fast-talking, sarcastic, and demanding impossible cinematic perfection.
- **Contextual Reactions:** Responds dynamically to player performance or run context—teasing players, complaining about budget/takes, and hyping up stunts.
- **Pacing & Language:** Delivers punchy, two-sentence maximum radio lines in English to keep momentum urgent and push the player toward the next film strip choice.
- **Event Integration:** Upon returning to the Backstage Hub, the scene manager automatically initiates the native Conversation Device dialogue, creating an instant walkie-talkie debrief before the player confirms the next scene selection.

---

## 5. Modular Level Design (MCP-Assisted Pipeline)

To maintain rock-solid AI navigation mesh (NavMesh) stability and eliminate game-breaking procedural generation bugs during a rapid jam timeline, the map uses a **fixed-stage constellation topology**: all stages exist as isolated, pre-built spatial volumes connected dynamically through a Verse teleporter routing system.

| Set Class | Thematic Variations | Gameplay Dynamics & Lighting Strategy |
| :--- | :--- | :--- |
| **Action Combat Sets** | Western Saloon, Cyberpunk Rooftop, Sci-Fi Bay, Noir Alley, Haunted Library, Castle Dungeon. | Tight cover-to-cover combat. High visual contrast driven by diegetic illumination (neon signs, swinging chandeliers, emergency strobes, torches) requiring zero bake delays. |
| **Stunt & Action Sets** | High-speed vehicle ramp leap, collapsing floor studio, temporal laser corridor obstacle course. | Adrenaline-fueled break from gunplay. Tests precise movement and editing tool mastery (using *Freeze* or *Fast-Forward* to beat hazards before the timer expires). |
| **Production Hub (Backstage)** | Soundstage green room, monitor stations, director's chair, wardrobe racks, film reels. | Zero-danger drafting zone. Houses the LLM Director conversation post and the Film Strip UI selection station. |

---

## 6. Meta-Progression: Film Strip Drafting

Prior to each scene transition, a custom Verse/UMG UI modal renders three vertical cards styled as physical 35mm film strips, presenting choices from three core pools:
- **Modifiers:** Temporary buffs such as speed or damage increases.
- **Tool Unlocks & Upgrades:** Expands the player's active *Director's Remote* toolkit (unlocking *Rewind* or *Plot Armor*, or reducing Roll costs).
- **Scene Booking (Routing):** Direct control over the upcoming set, allowing players to strategically opt into high-risk stunt stages or specific combat arenas.

---

## 7. Modular System Architecture

Four decoupled gameplay systems guarantee rapid iteration, clean state management, and zero single-point-of-failure build locks:
1. **`Shared Data & Stage Registry`:** Central definitions for editing tool categories, film roll costs, and modular stage configurations (entry teleporters, exit triggers, enemy spawner groups, and scene timers).
2. **`Edit Remote Controller`:** Manages Signal Remote primary and secondary input events, tool cycling, film roll balance validation, and runtime power execution.
3. **`Film Strip UI Controller`:** Dynamically builds and renders the three-card drafting interface on the player's viewport and applies selected script mutators or tool unlocks *(preferred implementation: UMG UI)*.
4. **`Scene Flow Router`:** Coordinates the round progression loop, randomized/booked stage selection, countdown enforcement, and transitions between the Backstage Hub and active sets.

---

## 8. Deliberate Scope Cuts (The "Cut" in Director's Cut)

- **[Pre-Kickoff Architectural Decision] Procedural Level Generation Cut:** Replaced runtime procedural room stitching with a pre-built **fixed-stage constellation topology** routed via Verse teleporters. *Rationale:* Preserves 100% NavMesh integrity, guarantees predictable lighting/spatial thermo budgets (`< 100k`), and avoids unrecoverable collision/navigation bugs under jam time constraints.
- *(Additional runtime scope cuts and pivots will be documented here and in `devlog/telemetry_log.md` as implementation progresses.)*

---

## 9. Progressive Technical Roadmap (Subject to Iteration)

- **Phase 1 — Foundational Sandbox & Remote Core:**
  - Initialize UEFN project under single-player 1vE ruleset; construct basic Backstage Hub envelope.
  - Implement `Edit Remote Controller` binding primary/secondary Signal Remote inputs.
  - Implement foundational tools: `CUT!` (targeted elimination query) and `FREEZE FRAME` (temporal stun effect).
  - Maintain live Glass Box telemetry from day one.
- **Phase 2 — Stage Generation & Scene Flow Infrastructure:**
  - Execute MCP routines to generate modular combat arenas and stunt stages with pre-validated collisions.
  - Install diegetic lighting anchors (neons, lanterns, emergency beacons) across active sets.
  - Construct `Scene Flow Router` managing stage lottery, countdown timers, and teleporters.
  - Integrate Backstage `Conversation Device` with LLM Director (**Stanley**) configuration and English persona guidelines.
- **Phase 3 — Meta-Progression, Audio & Extended Tools:**
  - Deploy `Film Strip UI Controller` rendering selectable 3-card draft overlays (UMG UI).
  - Implement advanced remote mechanics: `REWIND` (circular buffer playback) and `FAST-FORWARD` (launch velocity).
  - Hook audio feedback devices (clapperboards, scissors, reel rewinding, director loudspeaker calls).
  - Run full multi-scene trial passes verifying Game Over (out of Takes) and Victory/Credits triggers.
- **Phase 4 — Validation, Glass Box Compilation & Submission:**
  - Conduct 100% English localization audit (text, UI, audio).
  - Compile final Glass Box devlog deliverable with architecture diagrams, pipeline logs, prompt archives, and deep dives (e.g., Verse circular buffer & UMG UI drafting).
  - Generate Private Version Code in Creator Portal and run validation on the fixed snapshot (redacting full code in public docs).
  - Capture 45–60s 1080p gameplay trailer and submit final package (private island code, trailer URL, itch.io devlog).
