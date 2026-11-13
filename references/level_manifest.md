# UEFN Level Manifest (Anchors, Devices & Gameplay Contracts)

> **ROLE OF THIS DOCUMENT:** Lightweight navigation and contract index for the UEFN level across all collaborating agents (Antigravity, Cursor, Claude Code) and offline/non-MCP sessions. Keep this file strictly under ~150 lines.

## Manifest Contract Rules (Zero-Bloat & Auto-Sync)

1. **Strict Scope (Anchors & Contracts Only):**
   - **INCLUDE:** Stage origins/bounds, Gameplay Tags, core interactive/logic devices, Verse anchor devices, and critical `@editable` wiring contracts.
   - **NEVER INCLUDE:** Static architecture, walls, floors, decorative props, foliage, or non-interactive lights.
2. **Coordinate System:** Store all coordinates in **Unreal Engine Native `XYZ` (cm)** for direct `uefn-mcp` compatibility. *(Note: UEFN Editor UI displays `LUF`; convert `XYZ <-> LUF` when communicating positions to the user per `uefn-mcp/instructions.md`.)*
3. **Locate via Manifest, Verify via Targeted MCP:**
   - Read this manifest at session start instead of running a global level dump.
   - Before modifying an actor via `uefn-mcp`, run a **targeted/filtered query** (by actor label, Outliner folder, or Gameplay Tag) to verify live editor state.
4. **Silent Delta Updates & Auto-Heal:**
   - Whenever an agent creates, renames, moves, or deletes a Stage, Gameplay Tag, core Device, or `@editable` reference, update **only the affected row(s)** immediately.
   - If a targeted MCP query detects manual human edits in the UEFN editor, silently heal the matching row(s) here.
5. **Security & Privacy:** NEVER record Epic Games Account IDs, organization IDs, auth tokens, or full Private Version Codes.

---

## 1. Project & Level Identity

- **UEFN Project Name:** `DirectorsCutRoguelike`
- **Primary Level (`.umap`):** `DirectorsCutRoguelike.umap`
- **Project Directory:** `C:\Users\andre\OneDrive\Documentos\Fortnite Projects\DirectorsCutRoguelike`
- **Suggested Outliner Organization:** `00_CoreManagers`, `01_BackstageHub`, `02_CombatSets/*`, `03_StuntSets/*`, `04_FinaleSet/*`
- **Last Synced (ET):** `2026-11-12T23:21:26-05:00` (floor bases manually placed across all 10 stages; fig05 synced)

---

## 2. Stage Constellation Origins & Bounds

| Stage ID | Stage Name | Set Class | Outliner Folder | Origin XYZ (cm) | Approx Bounds (X x Y x Z cm) | Entry Teleporter / Spawner | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `STAGE_00` | `Backstage Hub` | `Backstage Hub` | `01_BackstageHub` | `(-4.75, -481.58, 116.00)` *(spawn anchor; LUF: L=481.58, U=116.00, F=-4.75)* | `~1536 x 1536 x 400` *(3x3 tiles, 512 cm)* | `Player Spawner` on Floor A6, yaw `85°` | `In Progress` |
| `STAGE_01` | `Western Saloon` | `Action Combat` | `02_CombatSets/Set01_WesternSaloon` | `(30720.0, -30720.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_01: Western Saloon` at `Z=2060` (minimap + overview). Floor base placed. | `Floor Base Placed` |
| `STAGE_02` | `Cyberpunk Rooftop` | `Action Combat` | `02_CombatSets/Set02_CyberpunkRooftop` | `(30720.0, 0.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_02: Cyberpunk Rooftop` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_03` | `Sci-Fi Bay` | `Action Combat` | `02_CombatSets/Set03_SciFiBay` | `(30720.0, 30720.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_03: Sci-Fi Bay` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_04` | `Noir Alley` | `Action Combat` | `02_CombatSets/Set04_NoirAlley` | `(61440.0, -30720.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_04: Noir Alley` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_05` | `Haunted Library` | `Action Combat` | `02_CombatSets/Set05_HauntedLibrary` | `(61440.0, 0.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_05: Haunted Library` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_06` | `Castle Dungeon` | `Action Combat` | `02_CombatSets/Set06_CastleDungeon` | `(61440.0, 30720.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_06: Castle Dungeon` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_07` | `Ramp Leap Studio` | `Stunt & Hazard` | `03_StuntSets/Set01_RampLeap` | `(-30720.0, -30720.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_07: Ramp Leap Studio` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_08` | `Collapsing Floor Studio` | `Stunt & Hazard` | `03_StuntSets/Set02_CollapsingFloor` | `(-30720.0, 0.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_08: Collapsing Floor Studio` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_09` | `Laser Corridor` | `Stunt & Hazard` | `03_StuntSets/Set03_LaserCorridor` | `(-30720.0, 30720.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_09: Laser Corridor` at `Z=2060`. Floor base placed. | `Floor Base Placed` |
| `STAGE_10` | `Grand Finale` | `Finale` | `04_FinaleSet/Set10_GrandFinale` | `(0.0, 61440.0, 0.0)` | `512 x 512 center slot; 30720 pitch` | Map Indicator `STAGE_10: Grand Finale` at `Z=2060`. Floor base placed. | `Floor Base Placed` |

---

## 3. Gameplay Tags Registry (Contract Layer)

> *Prefer Gameplay Tags for grouped actors (enemy spawners, laser hazards, stage lights, collapsing floors) so 1 row covers dozens of actors with zero maintenance drift.*

| Gameplay Tag | Verse Consumer (File / Class) | Target Actor Group (Summary) | Purpose |
| :--- | :--- | :--- | :--- |
| `director_enemy_spawner_tag` | `shared_data.verse` / `edit_remote_device` | `guard_spawner_device` instances (`Hub Guard Spawner`, stage spawners) | Dynamic discovery of all active enemy spawners for stasis & spawn suppression during `FREEZE FRAME`. |

---

## 4. Core Interactive Devices & Verse Anchors

| Outliner Label | Outliner Folder | Device / Class | Linked Verse / Tag | Role & Critical Config |
| :--- | :--- | :--- | :--- | :--- |
| `Player Spawner` | `01_BackstageHub` | `FortPlayerStartCreative` | — | Hub spawn on Floor A6. Native `XYZ (-4.75, -481.58, 116.00)`, rotator pitch `0` / yaw `85` / roll `0`. Editor LUF `L=481.58, U=116.00, F=-4.75`. |
| `Signal Remote Manager` | `00_CoreManagers` | `signal_remote_manager_device` | `edit_remote_device` | Captures Primary/Secondary fire events from the Signal Remote item. |
| `Item Granter` | `00_CoreManagers` | `item_granter_device` | — | Grants 1x `Signal Remote` on game start / player spawn. |
| `Edit Remote Device` | `00_CoreManagers` | `edit_remote_device` *(Verse)* | `PrimarySignalTrigger`, `SecondarySignalTrigger` | Core controller. Public `ReplenishRolls` / `ResetRolls` update `PlayerRolls` and refresh the HUD. |
| `Scene Flow Router` | `00_CoreManagers` | `scene_flow_router` *(Verse)* | `TakeStartTrigger`, `HubReturnTeleporter`, `Stages` | Round cycle `InHub` -> `InTake` -> `TakeComplete` / `RunOver`. Native `XYZ (270.00, -1266.00, 0.00)`. Editor LUF `L=1266.00, U=0.00, F=270.00`. `@editable` wiring is still open. |
| `Primary Signal Trigger` | `00_CoreManagers` | `trigger_device` | `edit_remote_device.PrimarySignalTrigger` | Place in editor. Bind Signal Remote Manager primary (left click) -> Trigger. |
| `Secondary Signal Trigger` | `00_CoreManagers` | `trigger_device` | `edit_remote_device.SecondarySignalTrigger` | Place in editor. Bind Signal Remote Manager secondary (right click) -> Trigger. |
| `Remote Held Checker` | `00_CoreManagers` | `conditional_button_device` | `edit_remote_device.RemoteHeldChecker` | Placed in `00_CoreManagers`. Key item set to Signal Remote. Verified live: HUD shows only while `IsHoldingItem` succeeds. |
| `Hub Guard Spawner` | `01_BackstageHub` | `guard_spawner_device` | `director_enemy_spawner_tag` | Test guard spawner opposite Player Spawner. Native `XYZ (0.00, 512.00, 12.00)`, yaw `-90°`. Editor LUF `L=-512.00, U=12.00, F=0.00`. "Despawn Guards When Disabled" must be `FALSE`. |

---

## 5. `@editable` Wiring Checklist (Details Panel Contracts)

> *Tracks critical `@editable` properties exposed by Verse devices that must remain wired in the UEFN Details panel to prevent silent runtime failures.*

| Verse Device (Outliner Label) | `@editable` Property | Expected Target (Label / Tag) | Wired in Editor? | Notes |
| :--- | :--- | :--- | :---: | :--- |
| `Edit Remote Device` | `SignalRemoteManager` | `Signal Remote Manager` in `00_CoreManagers` | `[ ]` | Optional (`?signal_remote_manager_device`). Bypassed cleanly by the two `trigger_device` bridges below. |
| `Edit Remote Device` | `PrimarySignalTrigger` | `Primary Signal Trigger` in `00_CoreManagers` | `[x]` | Wired & verified in live UEFN playtest; Direct Event Binding from `Signal Remote Manager` fires `OnPrimarySignal`. |
| `Edit Remote Device` | `SecondarySignalTrigger` | `Secondary Signal Trigger` in `00_CoreManagers` | `[x]` | Wired & verified in live UEFN playtest; Direct Event Binding from `Signal Remote Manager` fires `OnSecondarySignal`. |
| `Edit Remote Device` | `TestGuardSpawners` | `Hub Guard Spawner` in `01_BackstageHub` | `[x]` | Verified working in live UEFN playtest (`CUT!` and `FREEZE FRAME` affect Hub Guard). |
| `Edit Remote Device` | `RemoteHeldChecker` | `Remote Held Checker` in `00_CoreManagers` | `[x]` | Wired & verified in live UEFN playtest; Tier 1 HUD appears only while holding the Signal Remote. |
| `Scene Flow Router` | `EditRemote` | `Edit Remote Device` in `00_CoreManagers` | `[ ]` | Awards `ClearRollBonus` and resets rolls on Run Over. |
| `Scene Flow Router` | `HubReturnTeleporter` | Hub return `teleporter_device` (not placed) | `[ ]` | Hub teleport on Run Over and Run Victory only. Clears chain room to room. |
| `Scene Flow Router` | `TakeStartTrigger` | Action / clapper `trigger_device` (not placed) | `[ ]` | Starts a run from the hub. Ignored while a take or intermission is active. |
| `Scene Flow Router` | `StanleyDebriefTrigger` | Optional trigger for the Phase 2.3 Conversation Device | `[ ]` | Fired on Run Over and Run Victory, when the player is back in the hub. |
| `Scene Flow Router` | `Stages` | One `stage_definition` per set | `[ ]` | Combat: guard spawners and `TargetEliminations`. Stunt: `IsStuntSet` plus `FinishTrigger`. |
| `Scene Flow Router` | `StatusMessage` | Optional `hud_message_device` | `[ ]` | Unwired path still prints the same English lines. |
