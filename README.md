# OpenClaw Fixed On My Way (pnpm Edition) 🦞

This is the **OpenClaw** installation and configuration repository, fully optimized for **pnpm** usage. It includes the modified installer, dual-provider configuration (Z.AI OpenAI + Anthropic), and a comprehensive troubleshooting guide.

## 📂 Contents
- `install.sh`: The fully patched OpenClaw installer (replaced all `npm` with `pnpm`).
- `SKILL-DOCUMENTATION.md`: The "AI Skill" file containing every fix, workaround, and configuration detail.

## 🛠 Installation
To install OpenClaw using this pnpm-compatible installer:
```bash
bash install.sh --pnpm
```

## ✨ Key Features & Fixes
- **Pure Pnpm:** No `npm` commands used during installation.
- **Dual Provider:** Pre-configured for Z.AI with both Anthropic and OpenAI endpoints.
- **Wrapper Script:** Includes a custom `~/.local/bin/openclaw` wrapper to handle pnpm global paths.
- **Missing Deps Fix:** Manual pnpm commands to resolve bundled plugin errors.

## 🔒 Security Note
All API keys and tokens are **excluded** from this repository. You must configure your own keys in `~/.openclaw/openclaw.json`.

## 📖 Documentation
See `SKILL-DOCUMENTATION.md` for the complete troubleshooting matrix and LLM cheat sheet.

---
*Built and fixed by Fahad.*
