# 🦞 OpenClaw Master Skill Set (pnpm Edition)

**Description:** This repository serves as a comprehensive **AI Skill Set** for setting up, troubleshooting, and configuring **OpenClaw** on Linux using **pnpm**. It is designed to be read by AI assistants (like Qwen/Claude) or developers to quickly resolve issues.

## 🧠 How to use this Skill Set
If you are an AI or a developer tasked with fixing OpenClaw, read the files in order. **Every issue described here (Path, Z.AI, Plugins, Gateway) is actionable and fixed in this environment.**

## 📂 The Files (The Skills)

1.  **️ `01-PNPM-SETUP-AND-PATH-FIX.md` (The Foundation)**
    *   **What it fixes:** The entire `openclaw` binary not working because of `pnpm` path isolation.
    *   **Action:** Replaces `npm` with `pnpm`, creates wrapper scripts, and sets up `.npmrc`.

2.  **⚡ `02-ZAI-DUAL-PROVIDER-SOLUTION.md` (The Core Config)**
    *   **What it fixes:** Slow responses or billing errors with Z.AI.
    *   **Action:** Sets up **Dual Providers** (`zai` for Anthropic mode, `zai-openai` for OpenAI mode) so the system never goes down.

3.  ** `03-MISSING-DEPENDENCIES-FIX.md` (The Plugin Fix)**
    *   **What it fixes:** `openclaw doctor` failing because it can't find Discord, Slack, or Matrix plugins.
    *   **Action:** Provides the exact `pnpm add` command to manually install all missing bundled dependencies.

4.  **📡 `04-DISCORD-AND-GATEWAY-TROUBLESHOOTING.md` (The Operations)**
    *   **What it fixes:** "Unknown Channel" errors, TUI pairing failures, and Gateway timeouts.
    *   **Action:** Gives step-by-step resolution for daily operational errors.

## 📦 Included Scripts
*   **`install.sh`**: The patched installer that uses `pnpm add -g` instead of `npm`.

## 🔒 Security Note
*   **No Secrets:** This repository contains **NO API keys or Tokens**. All sensitive data is stored locally in `~/.openclaw/agents/main/agent/auth-profiles.json`.

---
*Created by Fahad. Optimized for pnpm.*
