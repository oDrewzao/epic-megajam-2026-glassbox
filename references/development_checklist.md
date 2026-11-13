# Master Development Checklist (Cross-Agent Roadmap)

> **ROLE OF THIS DOCUMENT:** Shared, persistent execution checklist for `DIRECTOR'S CUT ROGUELIKE` across all chats and agents (Antigravity, Cursor, Claude Code). Update `[ ]` -> `[>]` (active) -> `[x]` (done) as each item is verified in UEFN. Keep synced with `references/living_design_reference.md` and `references/level_manifest.md`.

**Current Active Step:** `3.1` (Film Strip Drafting UI 35mm + Verse UI Kit Audit) -> `3.2` (Extended Remote Tools: `REWIND`, `FAST-FORWARD`, `PLOT ARMOR`)

---

## Phase 1: Foundation, UEFN Setup & Remote Core (Day 1)
> **Goal:** Player spawns in the Backstage Hub, holds the Director's Remote, cycles tools, triggers `CUT!` and `FREEZE FRAME` against a live Guard Spawner, and tracks Film Rolls.

- [x] **1.1. Project Initialization & Outliner Structure**
  - [x] Initialize UEFN project (`DirectorsCutRoguelike.umap`).
  - [x] Create Outliner root folders (`00_CoreManagers`, `01_BackstageHub`, `02_CombatSets`, `03_StuntSets`).
  - [x] Sync project identity & paths in `references/level_manifest.md`.
  - [x] Capture initial editor screenshot (`fig01_uefn_project_initialized.png`).
- [x] **1.2. Backstage Hub (Safe Staging Area)**
  - [x] Block out initial Backstage Hub floor perimeter and prop palette (`fig02`, `fig03`).
  - [x] Place `Player Spawner` inside `01_BackstageHub` and verify coordinates (`XYZ (-4.75, -481.58, 116.00)`).
  - [ ] Add invisible boundary walls / collision perimeter around the Hub *(optional polish before Phase 2)*.
- [x] **1.3. Signal Remote Manager & Core Verse Architecture**
  - [x] Create `Content/shared_data.verse` (`remote_ability` enum, `RollCost()`, `ToString()`, `director_enemy_spawner_tag`).
  - [x] Create `Content/edit_remote_device.verse` (per-agent tool state & Film Roll economy).
  - [x] Place & wire `Signal Remote Manager`, `Item Granter` (Common Signal Remote), and `Edit Remote Device` in `00_CoreManagers`.
- [x] **1.4. Phase 1 Core Abilities (`CUT!` & `FREEZE FRAME`)**
  - [x] **1.4.1. Enemy Tracking:** Tag & array-wire `Hub Guard Spawner` (`XYZ (0, 512, 12)`), subscribe to `SpawnedEvent` / `EliminatedEvent`.
  - [x] **1.4.2. `CUT! (Scissors)` Logic:** Forward aim dot-product query (`<= 2500 cm`, `dot >= 0.45`), `9999.0` damage, refund 2 Rolls if no target in sight.
  - [x] **1.4.3. `FREEZE FRAME` Logic:** Stasis on active enemies (`4.0s`), pause spawners (`Despawn Guards When Disabled = false`), generation counter for overlapping casts.
  - [x] **1.4.4. Input Dispatch Fix (Trigger Bridge):** Add `PrimarySignalTrigger` & `SecondarySignalTrigger` (`trigger_device`) wired from `Signal Remote Manager` Direct Event Binding (verified live in UEFN playtest).
  - [x] **1.4.5. Lightweight Verse HUD Overlay (Tier 1 — Immediate Feedback):** `edit_remote_device.verse` attaches one non-blocking overlay per player (`ui_input_mode.None`) showing Active Tool, Roll Cost, Film Rolls (`Current/Max`), a 2.0s action banner, and a centered crosshair for aimed tools (`Cut` only; white, `Tomato` while a valid target is in sight). Compiled with `VerseToolset.BuildAll` (0 errors on the allowed retry) and verified live (`HudTopOffset = 240.0`). *(Deferred full Cinema UMG + `VerseUIKit` polish to Phase 3.1).*
  - [ ] **1.4.6. Optional VFX/SFX Polish Hooks:** Wire `CutAudio`, `FreezeAudio`, and `FreezePostProcess` (Sepia tint) when ready *(optional polish; deferred to Phase 3.3 or anytime)*.
- [x] **1.5. First Playable Sandbox Loop Verification**
  - [x] Verify in live UEFN session: Trigger-bridged Primary & Secondary remote buttons execute `CUT!`, `FREEZE FRAME`, and tool cycling reliably.
  - [x] Verify new Tier 1 Verse HUD overlay sits below the top-left editor chrome (`HudTopOffset = 240.0`), displays live tool swaps, Film Roll balance, and miss/empty feedback, shows the centered crosshair only for `Cut` (white, then tomato on a valid target), and (with `RemoteHeldChecker` wired) appears only while the Signal Remote is held.
  - [x] Log Phase 1 completion in `devlog/telemetry_log.md` and prepare Git checkpoint for user authorization.

---

## Phase 2: Fixed-Stage Constellation & Scene Flow (Day 2)
> **Goal:** Player leaves the Backstage Hub into a randomized room-to-room run. The Hub is only the lobby, Run Over, and Run Victory.

- [>] **2.1. Build Physical Arenas (Fixed-Stage Constellation)**
  - [ ] Build Action Combat Set 1 (e.g., *Western Saloon* or *Sci-Fi Bay*) under `02_CombatSets/*` with cover, lighting, entry teleporter, and tagged Guard Spawners.
  - [ ] Build Action Combat Set 2 (e.g., *Cyberpunk Rooftop* or *Noir Alley*).
  - [ ] Build Stunt & Hazard Set 1 (e.g., *Laser Corridor / Collapsing Floor* obstacle course) under `03_StuntSets/*`.
  - [x] Place one Map Indicator per stage (`STAGE_01`–`STAGE_10`) on a 30720 cm pitch (scaled 2x from the first 15360 cm layout), English label `STAGE_XX: <Name>`, visible on minimap and overview map. Origins registered in `references/level_manifest.md`.
  - [x] Place floor base (`BP_BeefJerky_Floor_A`) at each origin (`STAGE_01`–`STAGE_10`) via manual editor duplication (`fig05_fixed_stage_constellation_floors.png`).
  - [>] Place essential stage device clusters (`EntryTeleporter`, `guard_spawner_device`, `StageTracker`, `DirectorInteractButton`) on each stage floor (`fig06_stage_essential_devices_setup.png` in progress).
  - [ ] Register entry teleporters and Gameplay Tags in `references/level_manifest.md` when those devices exist.
- [x] **2.2. `Scene Flow Router` (`scene_flow_router.verse`)** — *Verified Live (initial stages)*
  - [x] Implement round cycle: hub Action requests a pre-run draft stub, then teleports into a random unvisited stage. A clear enables that room's Director. The Director button drafts, resets the room, and enters the next stage. Hub return is Run Over or Run Victory only.
  - [x] Room clear is `StageTracker.CompleteEvent`. Combat (`TargetEliminations` or spawned-this-Take) and stunt (`FinishTrigger`) remain fallbacks. Dynamic Verse scene HUD mirrors objective/Tracker only (without `STUNT LIVES`).
  - [x] One elimination during a take is Run Over. There is no Stunt Double Lives retry. `RunOver` resets the active stage and Film Rolls, then returns to the Hub.
  - [x] `ClearRollBonus` is awarded when the Director button is used. Run Victory fills rolls to `MaxFilmRolls`. Run Over uses `ResetRolls` with `RunOverFilmRolls`.
  - [x] Wire initial `stage_definition` rows (`STAGE_01`, `STAGE_02`) with `EntryTeleporter`, `StageTracker`, `DirectorSpawner`, `DirectorInteractButton`, `GuardSpawners`, `WildlifeSpawners` (`director_enemy_spawner_tag`), and `EnemyNPCSpawners` — verified live (`fig08_director_npc_spawn_and_interact.png`). *(Remaining stages wired as arenas are built in 2.1).*
- [>] **2.3. Director Stanley Integration (Walkie-Talkie Modifier)** — *Ready for playtest after `StanleyConversation` is assigned in Details*
  - [ ] Place Stanley NPC / Director's Chair prop in `01_BackstageHub`.
  - [x] Configure native UEFN `Conversation Device` with short, frantic 1980s Hollywood director lines (100% English). Bank `CB_StanleyRadio` uses one Speech node (`fig09_stanley_radio_speech_node.png`).
  - [x] Verse debrief: `RunVictory` calls `InitiateConversation(Player)` 0.3s after the hub teleport. `RunOver` sets `PendingStanleyDebrief` and waits for `hub_player_spawner_tag` on `Player Spawner`. `VerseToolset.BuildAll` returned no errors. The `HubPlayerSpawner` editable did not appear in Details, so the tag is the contract.
- [ ] **2.4. Phase 2 Full Loop Playtest**
  - [ ] Test full loop: Spawn in Hub -> Action draft -> clear a set -> talk to the room Director -> next random unvisited set -> Run Victory or Run Over returns to the Hub.
  - [ ] Log Phase 2 milestone in `devlog/telemetry_log.md` (+ screenshot).

---

## Phase 3: Meta-Progression (Film Strips), Extended Tools & Audio (Day 3)
> **Goal:** Roguelite Film Strip Drafting UI, advanced temporal/movement editing tools, and diegetic cinema audio/HUD.

- [ ] **3.1. Film Strip Drafting UI (`film_strip_ui_controller.verse` + UMG / Verse UI Kit)**
  - [ ] Audit/check `Verse UI Kit` availability in project before authoring UMG widgets (per `uefn_ui_rules.md`).
  - [ ] Design 35mm Film Strip modal presenting 3 selectable strips between Takes.
  - [ ] Implement selection capture & mutator dispatch:
    - *Modifiers:* Speed boost, max Film Roll capacity, roll regen/bonus.
    - *Tool Unlocks / Upgrades:* Unlock `Rewind`, `Fast-Forward`, `Plot Armor`, or reduce Roll costs.
    - *Scene Booking:* Choose next Combat or Stunt set.
  - [ ] Upgrade Tier 1 temporary Verse HUD into final **Cinema UMG HUD** bound in Verse (`VerseUIKit` SDF Film Roll meter, `UW_Feedback_Toast` alerts, Active Tool, Cost, and Remaining Takes).
- [ ] **3.2. Extended Director's Remote Tools**
  - [ ] **`REWIND` (2 Rolls):** Circular buffer recording player position + health over last 3 seconds; instant rewind on trigger.
  - [ ] **`FAST-FORWARD` (1 Roll):** Explosive horizontal dash / velocity impulse forward (useful in Stunt Sets & dodging).
  - [ ] **`PLOT ARMOR` (3 Rolls):** Temporary invincibility + explosive shot feedback for 4 seconds.
- [ ] **3.3. Diegetic Cinema Audio & VFX**
  - [ ] Clapperboard SFX/UI overlay (*Action! / Cut!*).
  - [ ] Scissors tape-snip SFX + burst VFX on `CUT!`.
  - [ ] Sepia/freeze post-process + shutter click SFX on `FREEZE FRAME`.
  - [ ] Cassette tape-rewind SFX on `REWIND`.
  - [ ] Walkie-talkie radio static SFX for Stanley's calls.

---

## Phase 4: Memory Optimization, Regulatory Audit, Trailer & Submission (Day 4)
> **Goal:** Below 100k Spatial Thermometer, 100% English verified, 30–60s 1080p trailer recorded, Glass Box devlog finalized, Private Version Code submitted before Nov 15, 8:59 PM ET.

- [ ] **4.1. Memory & Performance Audit (Spatial Thermometer)**
  - [ ] Run full Spatial Metrics / Memory Calculation check (`< 100,000` units across all cells).
  - [ ] Prune unused assets, adjust HLODs/draw distances if any cell approaches budget.
- [ ] **4.2. Competition Compliance Audit (`references/competition_rules.md`)**
  - [ ] Verify **100% English** across all UI text, HUDs, Stanley dialogue, device names, and logs.
  - [ ] Verify single-player 1vE flow from spawn to run completion with zero soft-locks.
  - [ ] Record & edit **30–60s 1080p Trailer** (no copyrighted third-party music) showcasing `CUT!`, `FREEZE FRAME`, `REWIND`, Film Strip Drafting, and Stanley.
- [ ] **4.3. Glass Box Devlog Finalization**
  - [ ] Audit `devlog/telemetry_log.md` for rule compliance (ET timestamps, translated prompts, model names, no exposed IDs/secrets, all `figXX` CDN links valid).
  - [ ] Export/render final devlog presentation (HTML/Markdown/GitHub check).
- [ ] **4.4. Publishing & Official Jam Submission**
  - [ ] Upload private island version in UEFN Creator Portal and generate **Private Version Code** (mask in public logs!).
  - [ ] Submit entry form before **Nov 15, 2026, 8:59 PM ET**.
