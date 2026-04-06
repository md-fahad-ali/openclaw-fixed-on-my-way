# OpenClaw: The Pnpm Solution 🦞

This repository contains the **exact fixes and configurations** used to set up **OpenClaw** using **pnpm** on Linux. It includes the patched installer, the Z.AI dual-provider setup, and detailed troubleshooting guides.

## 📂 Series Documentation
This repo is structured as a "Skill Series". Read the files in order:

1.  **[01-PNPM-SETUP-AND-PATH-FIX.md](./01-PNPM-SETUP-AND-PATH-FIX.md)**
    *   *Fixing the installer, wrapper scripts, and `.npmrc` config.*
2.  **[02-ZAI-DUAL-PROVIDER-SOLUTION.md](./02-ZAI-DUAL-PROVIDER-SOLUTION.md)**
    *   *The core solution for Z.AI: How to run both Anthropic and OpenAI endpoints simultaneously.*
3.  **[03-MISSING-DEPENDENCIES-FIX.md](./03-MISSING-DEPENDENCIES-FIX.md)**
    *   *Manual pnpm commands to fix Discord, Slack, and Matrix plugin errors.*
4.  **[04-DISCORD-AND-GATEWAY-TROUBLESHOOTING.md](./04-DISCORD-AND-GATEWAY-TROUBLESHOOTING.md)**
    *   *Solving "Unknown Channel", "Pairing Required", and 401 Token errors.*

## 📦 Files Included
*   `install.sh`: The fully pnpm-compatible installer script.
*   `README.md`: This file.

## 🛠 Quick Start
```bash
bash install.sh --pnpm
```

---
*Open Source & Detailed by Fahad.*
