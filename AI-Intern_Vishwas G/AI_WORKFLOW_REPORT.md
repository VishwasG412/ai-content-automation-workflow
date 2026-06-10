# AI Content Automation Workflow

> Powered by Google Gemini + n8n, delivered via Telegram

---

## Overview

This workflow automates end-to-end content creation from a single topic input. It uses Google Gemini as the AI backbone, n8n for orchestration, and Telegram for delivery — with memory-aware context across interactions and error handling at every stage.

---

## Metrics

| Stat | Value |
|---|---|
| Content outputs | 5 |
| Workflow nodes | 7 |
| Error handlers | 3 |
| Delivery channel | Telegram |

---

## Node Pipeline

```
Manual Trigger → Edit Fields → IF Node → AI Agent → Simple Memory → Gemini Model → Telegram Send
```

---

## Features

### Content Outputs

- Blog title generation
- Blog outline generation
- Full article generation
- Social media caption generation
- Hashtag generation

### Error Handling

- Empty input validation
- API failure protection
- Invalid response handling

### Optimizations

- Improved prompt engineering
- Clean node organization
- Structured output formatting

### Additional

- **AI agent memory** — maintains context across interactions
- **Telegram integration** — auto-delivers all generated content

---

## Expected Result

Generates a complete content package from a single topic input, with memory-aware context across interactions, and auto-delivers all outputs via Telegram — errors handled gracefully at each stage.
