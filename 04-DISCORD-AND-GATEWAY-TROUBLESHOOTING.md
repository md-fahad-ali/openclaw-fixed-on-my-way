# Part 04: Discord & Gateway Troubleshooting
**Issue:** Common errors during daily use of OpenClaw with Discord.

## 1. Error: "Unknown Channel"
**Symptom:** Sending a message fails.
**Cause:** Using the **Guild ID** (Server ID) instead of the **Channel ID**.
**Fix:**
1.  Right-click the specific Discord channel (e.g., #setup).
2.  Select "Copy Channel ID".
3.  Use that ID in your commands.

## 2. Error: "Pairing Required" (TUI)
**Symptom:** `openclaw tui` shows "not connected".
**Fix:**
1.  Run `openclaw devices list`.
2.  Copy the Request ID.
3.  Run `openclaw devices approve <REQUEST_ID>`.

## 3. Error: "Discord failed (401)"
**Symptom:** Bot is offline or commands fail.
**Cause:** Token expired or invalid.
**Fix:**
1.  Go to [Discord Developer Portal](https://discord.com/developers).
2.  Copy the new Bot Token.
3.  Paste into `~/.openclaw/openclaw.json` -> `channels.discord.token`.
4.  Run `openclaw gateway restart`.

## 4. Error: "Gateway Timeout"
**Symptom:** CLI commands hang.
**Fix:**
```bash
systemctl --user stop openclaw-gateway.service
openclaw gateway restart
```

---
*End of Part 04*
