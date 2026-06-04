---
title: "OpenCodeでGemmaを使う"
---

「OpenCodeをGemmaで使う」とも言える

[[OpenCode]] / [[Gemma]]

opencode.jsonを置くだけであっさり解決した
opencode.json

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "cybozu": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "***",
      "options": {
        "baseURL": "https://***"
      },
      "models": {
        "gemma-4-31B-it": {
          "name": "Gemma 4 31B IT"
        }
      }
    }
  }
}
```


[[KarpathyのLLM Wiki]]をローカルLLMで動かしたかったので
