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

4. TELEMETRY LOG SCHEMA:
   Append every completed task to `devlog/telemetry_log.md`:
   ### [UTC_TIMESTAMP] - [CATEGORY] - [Task Title]
   - **Environment & Exact Model:** (e.g., Antigravity / Gemini Flash 3.8, Cursor / Claude 3.5 Sonnet)
   - **Subsystem:** (Verse Device, Level Architecture, Asset Pipeline, Camera/Cinematic)
   - **Design Rationale (Director's Intent):** Why this serves the "Director's Cut" theme and scope.
   - **Prompt Used (Translated to English):** `Cleaned prompt without API secrets`
   - **Execution & Code/Assets:** What was built or modified.
   - **AI Hallucinations, Verse Errors & Human Debugging (GLASS BOX TRANSPARENCY):** Transparent breakdown of failures, syntax hallucinations, and manual fixes.
