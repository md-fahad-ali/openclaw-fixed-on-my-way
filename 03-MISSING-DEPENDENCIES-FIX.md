# Part 03: Missing Dependencies Fix
**Issue:** `openclaw doctor` reports errors for bundled plugins (Discord, Slack, Matrix, etc.).
**Fix:** Manually install missing packages via `pnpm`.

## 1. Why It Fails
`openclaw doctor --fix` often fails because it tries to run `npm install` in a pnpm environment, which breaks the strict isolation or simply doesn't work for global installs in this specific setup.

## 2. The Fix Command
Run this command inside the global store directory:
`cd ~/.local/share/pnpm/global/5`

Then run:
```bash
pnpm add @slack/web-api @slack/logger @slack/oauth @slack/socket-mode @slack/bolt \
         @discordjs/voice @discordjs/opus @larksuiteoapi/node-sdk \
         @opentelemetry/api @opentelemetry/sdk-node \
         @whiskeysockets/baileys silk-wasm mpg123-decoder \
         jimp markdown-it matrix-js-sdk fake-indexeddb music-metadata \
         @aws-sdk/client-bedrock @aws-sdk/client-s3 \
         @pierre/diffs @pierre/theme commander undici ws zca-js
```

## 3. Important Notes
*   **Peer Dependencies:** You may see warnings about `react` or `lodash`. **Ignore these**. They are not needed for the bot functionality.
*   **Restart:** After installing, run `openclaw gateway restart`.

---
*End of Part 03*
