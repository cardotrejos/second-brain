1. open -e ~/.clawdbot/clawdbot.json update this section
    
    ```
    "models": {
    "mode": "merge",
    "providers": {
      "kimi-code": {
        "baseUrl": "https://api.kimi.com/coding/v1",
        "api": "openai-completions",
        "headers": {
          "User-Agent": "KimiCLI/0.77"
        },
        "models": [
          {
            "id": "kimi-for-coding",
            "name": "Kimi For Coding",
            "reasoning": true,
            "input": ["text"],
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },
            "contextWindow": 262144,
            "maxTokens": 32768,
            "compat": { "supportsDeveloperRole": false }
          },
          {
            "id": "kimi-k2.5",
            "name": "Kimi K2.5",
            "reasoning": true,
            "input": ["text"],
            "contextWindow": 262144,
            "maxTokens": 32768,
            "compat": { "supportsDeveloperRole": false }
          }
        ]
      }
    }
  },
    ```

```

```