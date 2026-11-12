# MANDATORY PROTOCOL: GLASS BOX TELEMETRY & SECURITY RULES

1. STRICT LANGUAGE ENFORCEMENT:
   All documentation, logs, code explanations, and translated prompts MUST be written in professional, technical ENGLISH. If the human developer inputs instructions in Portuguese or another language, you must translate the prompt and rationale into English before logging it.

2. SECURITY & DATA PRIVACY (CRITICAL):
   NEVER expose sensitive credentials in `telemetry_log.md` or any generated HTML:
   - Redact Epic Games Account IDs, organization IDs, and auth session tokens.
   - Redact full Private Version Codes or treat them with a hash/mask (e.g., `1234-5678-XXXX?v=XX`).
   - Redact all API keys (Anthropic, SpaceXSI, OpenAI, fal, Meshy, GitHub PATs).

3. IMAGE AUTO-LINKING:
   All screenshots, sketches, and charts must be saved to `devlog/images/` with normalized names (`figXX_description.png`). In generated devlog outputs, embed them as:
   `<div style="text-align: center; margin: 20px 0;"><img src="https://raw.githubusercontent.com/oDrewzao/epic-megajam-2026-glassbox/main/devlog/images/figXX_description.png" alt="Description" style="max-width: 100%; border-radius: 8px;"/><p><em>Figure XX: Description</em></p></div>`

4. TELEMETRY LOG SCHEMA & OFFICIAL TIMEZONE:
   All timestamps MUST use the official jam timezone: **Eastern Time (ET / EST / UTC-5)** (format: `[YYYY-MM-DDTHH:mm:ss-05:00] (HH:mm:ss ET)`).
   Append every completed task to `devlog/telemetry_log.md`:
   ### [ET_TIMESTAMP] - [CATEGORY] - [Task Title]
   - **Environment & Exact Model:** (e.g., Antigravity / Gemini 3.8 Flash, Cursor / Claude 3.5 Sonnet)
   - **Subsystem:** (Verse Device, Level Architecture, Asset Pipeline, Camera/Cinematic)
   - **Design Rationale (Director's Intent):** Why this serves the "Director's Cut" theme and scope.
   - **Prompt Used (Translated to English):** `Cleaned prompt without API secrets`
   - **Execution & Code/Assets:** What was built or modified.
   - **AI Hallucinations, Verse Errors & Human Debugging (GLASS BOX TRANSPARENCY):** Transparent breakdown of failures, syntax hallucinations, and manual fixes.

5. LIVING REFERENCES & OFFICIAL RULES (CROSS-AGENT ALIGNMENT):
   To keep chats lean and all tools synchronized across Antigravity, Cursor, Claude Code, and other agents, ALWAYS consult:
   - `references/competition_rules.md`: Mandatory rules, ET deadlines, judging criteria, and modifier rules.
   - `references/living_design_reference.md`: The active, evolving living single source of truth for features, architecture, and roadmap. Keep this file updated dynamically whenever scope, mechanics, or architectural choices change.
   *(Note: `devlog/game_design_context.md` is a frozen historical pre-kickoff snapshot).*
