# Part 01: Pnpm Setup & Path Fix
**Issue:** OpenClaw standard installer uses `npm`, but we require `pnpm`.
**Fix:** Modified installer and fixed binary path.

## 1. The Installation Problem
The original `install.sh` fails because:
1.  It runs `npm install -g`.
2.  Pnpm global packages are isolated (not in `node_modules` root).
3.  The `openclaw` binary is missing from the system PATH.

## 2. The Wrapper Script Solution
Since `pnpm add -g` installs to `~/.local/share/pnpm/global/5/node_modules/.bin`, the binary is not found by default.

**Fix:** Create a wrapper script at `~/.local/bin/openclaw`.

```bash
#!/usr/bin/env bash
set -euo pipefail
# Point to the pnpm global binary
BIN_DIR="/home/fahad/.local/share/pnpm/global/5/node_modules/.bin"
# Add pnpm's pnpm directory to NODE_PATH so OpenClaw can find its own libs
export NODE_PATH="/home/fahad/.local/share/pnpm/global/5/node_modules/.pnpm/node_modules"
exec "$BIN_DIR/openclaw" "$@"
```
**Permissions:** `chmod +x ~/.local/bin/openclaw`

## 3. Pnpm Configuration
To fix "Module not found" errors for bundled plugins (like Discord/Slack), add a `.npmrc` file to the global store:

**File:** `~/.local/share/pnpm/global/5/.npmrc`
```ini
shamefully-hoist=true
auto-install-peers=true
```
*Reason:* OpenClaw expects a flat `node_modules` structure (like npm). `shamefully-hoist` forces pnpm to flatten the dependencies so bundled plugins can find them.

## 4. Installer Modification
If using `install.sh`, replace all instances of `npm install -g` with `pnpm add -g`.

---
*End of Part 01*
