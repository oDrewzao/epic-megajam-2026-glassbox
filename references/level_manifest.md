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
- **Suggested Outliner Organization:** `00_CoreManagers`, `01_BackstageHub`, `02_CombatSets/*`, `03_StuntSets/*`
- **Last Synced (ET):** `2026-11-12T08:15:11-05:00` (Phase 1.4 CUT & FREEZE FRAME logic compiled, Hub Guard Spawner placed)

---

## 2. Stage Constellation Origins & Bounds

| Stage ID | Stage Name | Set Class | Outliner Folder | Origin XYZ (cm) | Approx Bounds (X x Y x Z cm) | Entry Teleporter / Spawner | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `STAGE_00` | `Backstage Hub` | `Backstage Hub` | `01_BackstageHub` | `(-4.75, -481.58, 116.00)` *(spawn anchor; LUF: L=481.58, U=116.00, F=-4.75)* | `~1536 x 1536 x 400` *(3x3 tiles, 512 cm)* | `Player Spawner` on Floor A6, yaw `85°` | `In Progress` |

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
| `Edit Remote Device` | `00_CoreManagers` | `edit_remote_device` *(Verse)* | `SignalRemoteManager` | Core controller managing active tool cycling & Film Roll balance. |
| `Hub Guard Spawner` | `01_BackstageHub` | `guard_spawner_device` | `director_enemy_spawner_tag` | Test guard spawner opposite Player Spawner. Native `XYZ (0.00, 512.00, 12.00)`, yaw `-90°`. Editor LUF `L=-512.00, U=12.00, F=0.00`. "Despawn Guards When Disabled" must be `FALSE`. |

---

## 5. `@editable` Wiring Checklist (Details Panel Contracts)

> *Tracks critical `@editable` properties exposed by Verse devices that must remain wired in the UEFN Details panel to prevent silent runtime failures.*

| Verse Device (Outliner Label) | `@editable` Property | Expected Target (Label / Tag) | Wired in Editor? | Notes |
| :--- | :--- | :--- | :---: | :--- |
| `Edit Remote Device` | `SignalRemoteManager` | `Signal Remote Manager` in `00_CoreManagers` | `[x]` | `MaxFilmRolls = 10`, `StartingFilmRolls = 5`. Wired in editor. |
| `Edit Remote Device` | `TestGuardSpawners` | `Hub Guard Spawner` in `01_BackstageHub` | `[ ]` | Array property. Requires manual addition of `Hub Guard Spawner` in Details panel (MCP automated binding rejected). |
