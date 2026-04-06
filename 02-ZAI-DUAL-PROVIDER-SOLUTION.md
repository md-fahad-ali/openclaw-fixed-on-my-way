# Part 02: Z.AI Dual Provider Solution
**Issue:** Z.AI offers two endpoints. One is slow (Anthropic wrapper), one is fast (OpenAI native).
**Fix:** Configure BOTH in `openclaw.json` to allow switching.

## 1. The Problem
Z.AI's API has two endpoints:
1.  **Anthropic Endpoint:** `https://api.z.ai/api/anthropic` (Slow, acts as a proxy).
2.  **OpenAI Endpoint:** `https://api.z.ai/api/coding/paas/v4` (Fast, native support for GLM models).

By default, the installer might only configure one, or you might get stuck with the slow one.

## 2. The Solution (Dual Config)
Edit `~/.openclaw/openclaw.json`. Add **two** providers under `models.providers`.

### Provider A: `zai` (Anthropic Mode)
```json
"zai": {
  "baseUrl": "https://api.z.ai/api/anthropic",
  "api": "anthropic-messages",
  "models": [
    { "id": "glm-4.7-flash", "name": "GLM-4.7 Flash (Anthropic)", "contextWindow": 200000, "maxTokens": 131072 }
  ]
}
```

### Provider B: `zai-openai` (OpenAI Mode - Recommended)
```json
"zai-openai": {
  "baseUrl": "https://api.z.ai/api/coding/paas/v4",
  "api": "openai-completions",
  "models": [
    { "id": "glm-5", "name": "GLM-5 (Fast)", "contextWindow": 202800, "maxTokens": 131100 },
    { "id": "glm-4.7-flash", "name": "GLM-4.7 Flash (Fast)", "contextWindow": 200000, "maxTokens": 131072 }
  ]
}
```

## 3. Updating Fallbacks
Ensure the fallbacks list in `agents.defaults.model` includes both:
```json
"fallbacks": [
  "zai-openai/glm-5",
  "zai-openai/glm-4.7-flash",
  "zai/glm-4.7-flash"
]
```

## 4. How to Switch
*   **For Speed:** Set primary model to `zai-openai/glm-5`.
*   **For Testing Anthropic Compatibility:** Set primary model to `zai/glm-4.7-flash`.

---
*End of Part 02*
