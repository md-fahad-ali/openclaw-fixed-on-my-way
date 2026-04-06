# OpenClaw: The Ultimate Setup & Troubleshooting Manual
**Owner:** Fahad
**Version:** 2026.4.5
**Package Manager:** pnpm (v10.33.0) — *Strictly NO npm allowed.*

---

## 1. System Profile & Environment
*   **OS:** Linux (fahad-HP-ProBook-430-G5)
*   **Node.js:** v22.22.2 (via NVM)
*   **Shell:** Bash/Zsh (Path includes `~/.local/bin`)
*   **Install Location:** `~/.local/share/pnpm/global/5/`

**⚠️ Critical Path Note:**
OpenClaw is installed via pnpm global, which does **not** symlink binaries to `~/.nvm/versions/node/.../bin` automatically.
**FIX:** We use a custom wrapper script at `~/.local/bin/openclaw`.
```bash
#!/usr/bin/env bash
set -euo pipefail
BIN_DIR="/home/fahad/.local/share/pnpm/global/5/node_modules/.bin"
export NODE_PATH="/home/fahad/.local/share/pnpm/global/5/node_modules/.pnpm/node_modules"
exec "$BIN_DIR/openclaw" "$@"
```

---

## 2. Installation Strategy (The "Pnpm" Way)
Standard `install.sh` uses `npm`. This breaks our pnpm-only ecosystem.
**Steps to reproduce this setup:**
1.  **Modify `install.sh`:** Replace all instances of `npm install -g` with `pnpm add -g`.
2.  **Create `.npmrc`:** In the global store directory (`~/.local/share/pnpm/global/5/.npmrc`), add:
    ```ini
    shamefully-hoist=true
    auto-install-peers=true
    ```
    *Why?* OpenClaw bundles plugins that expect a flat `node_modules` (npm style). Pnpm's strict isolation hides these. `shamefully-hoist` fixes the `Cannot find module` errors.

3.  **Wrapper Script:** Ensure `~/.local/bin/openclaw` exists (see Section 1).

---

## 3. The "Dual Provider" Configuration
We use **Z.AI** as the model provider. Z.AI offers two different API endpoints. We have configured **BOTH** to ensure we can test the Anthropic endpoint but fall back to the fast OpenAI endpoint.

**File:** `~/.openclaw/openclaw.json`

### Provider A: `zai` (Anthropic Endpoint)
*   **Purpose:** Testing Anthropic-compatible routing.
*   **Status:** Active but slower (Proxy layer).
*   **Config:**
    ```json
    "zai": {
      "baseUrl": "https://api.z.ai/api/anthropic",
      "api": "anthropic-messages",
      "models": [ ... ]
    }
    ```

### Provider B: `zai-openai` (OpenAI Endpoint)
*   **Purpose:** Production/Fast routing.
*   **Status:** Recommended for daily use.
*   **Config:**
    ```json
    "zai-openai": {
      "baseUrl": "https://api.z.ai/api/coding/paas/v4",
      "api": "openai-completions",
      "models": [ ... ]
    }
    ```

**How to switch models:**
*   **To use Anthropic:** `openclaw config set agents.defaults.model.primary "zai/glm-4.7-flash"`
*   **To use OpenAI (Fast):** `openclaw config set agents.defaults.model.primary "zai-openai/glm-5"`

---

## 4. Dependency Management (The "Missing Plugins" Fix)
`openclaw doctor --fix` often fails because it tries to use `npm`.
**Manual Fix:**
Run this inside `~/.local/share/pnpm/global/5`:
```bash
pnpm add @slack/web-api @slack/logger @slack/oauth @slack/socket-mode @slack/bolt \
         @discordjs/voice @discordjs/opus @larksuiteoapi/node-sdk \
         @opentelemetry/api @opentelemetry/sdk-node \
         @whiskeysockets/baileys silk-wasm mpg123-decoder \
         jimp markdown-it matrix-js-sdk fake-indexeddb music-metadata \
         @aws-sdk/client-bedrock @aws-sdk/client-s3 \
         @pierre/diffs @pierre/theme commander undici ws zca-js
```

**Warning:** You may see `peer dependency` warnings for `react`. Ignore these; they do not affect the bot functionality.

---

## 5. Discord Integration Guide
**Error:** `Error: Unknown Channel`
*   **Cause:** You provided the **Guild ID** (Server ID) instead of the **Channel ID**.
*   **Fix:** Right-click the specific channel in Discord $\to$ "Copy Channel ID". Use that string in the `target` or `to` argument.

**Error:** `Discord: failed (401)`
*   **Cause:** Token expired or invalid.
*   **Fix:** Go to [Discord Developer Portal](https://discord.com/developers), copy the new Bot Token, and paste it into `~/.openclaw/openclaw.json` under `channels.discord.token`. Then run `openclaw gateway restart`.

**Error:** `Pairing required` (TUI)
*   **Fix:** Run `openclaw devices list` $\to$ Copy Request ID $\to$ `openclaw devices approve <ID>`.

---

## 6. Troubleshooting Matrix (LLM Cheat Sheet)

| Symptom | Diagnosis | Action |
| :--- | :--- | :--- |
| `command not found: openclaw` | PATH issue. | Ensure `~/.local/bin` is in PATH. Run wrapper script check. |
| `API provider returned billing error` | Z.AI Key out of credits. | **Action:** Check Z.AI dashboard balance. Top up or switch key. |
| `Bundled plugin runtime deps missing` | Pnpm isolation strictness. | **Action:** Run the `pnpm add` list in Section 4. |
| `openclaw doctor` fails with `npm` error | Doctor uses npm by default. | **Action:** Ignore doctor's install. Run manual `pnpm add` commands. |
| `Gateway timeout` | Service hanging. | **Action:** `systemctl --user stop openclaw-gateway` then `openclaw gateway restart`. |
| `TUI stuck connecting` | Pairing missing or Host header mismatch. | **Action:** `openclaw devices approve`. |
| `Slow responses from LLM` | Using `zai/glm-...` (Anthropic proxy). | **Action:** Switch model to `zai-openai/glm-5`. |
| `Unknown Channel` | Wrong ID type. | **Action:** Use Channel ID, not Server ID. |

---

## 7. Maintenance & Updates
*   **Restart Service:** `openclaw gateway restart` (Always do this after editing JSON).
*   **Check Health:** `openclaw health`.
*   **View Logs:** `tail -f /tmp/openclaw/openclaw-*.log`.

---
*This document serves as the source of truth for this machine's OpenClaw configuration.*