# 🛠 Skill 01: PNPM Setup & Path Fix (Universal)

**Scope:** This skill fixes the **entire OpenClaw installation** so it works with `pnpm` instead of `npm`.
**Problem:** `command not found: openclaw` and npm dependency errors.

## 📌 Why this exists
Standard `install.sh` fails because:
1.  It uses `npm`, which we are replacing with `pnpm`.
2.  `pnpm` isolates binaries, so `openclaw` disappears from the PATH.

## 🔧 The Fix Steps

### Step 1: Wrapper Script
We created a custom launcher at `~/.local/bin/openclaw` so the system can find the binary.

```bash
#!/usr/bin/env bash
set -euo pipefail
BIN_DIR="/home/fahad/.local/share/pnpm/global/5/node_modules/.bin"
export NODE_PATH="/home/fahad/.local/share/pnpm/global/5/node_modules/.pnpm/node_modules"
exec "$BIN_DIR/openclaw" "$@"
```

### Step 2: Pnpm Hoisting
We added `.npmrc` with `shamefully-hoist=true` to fix "Module Not Found" errors for **ALL** plugins.

---
*End of Skill 01*
