# ⚡ Skill 02: Z.AI Dual Provider Solution (Model Config)

**Scope:** This skill fixes **slow responses** and **billing errors** by configuring two API endpoints for Z.AI.
**Problem:** Single provider setup is fragile; if one endpoint is slow, the bot hangs.

## 📌 The Solution
We configured **TWO** providers in `openclaw.json`:

1.  **`zai` (Anthropic Mode):** For testing compatibility.
2.  **`zai-openai` (OpenAI Mode):** For **FAST** production use (Native GLM support).

## 🔧 The Config
See `openclaw.json` -> `models.providers`.
*   **Action:** If the bot is slow, switch the primary model to `zai-openai/glm-5`.

---
*End of Skill 02*
