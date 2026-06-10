# AI Content Automation Workflow — Architecture

> Google Gemini + n8n | 8 nodes | 3 error paths | Telegram delivery

---

## Node Pipeline

### 1. Manual trigger `[Input]`
- Starts workflow execution
- User runs it manually; no scheduled or webhook trigger

### 2. Edit fields `[Processing]`
- Stores the user-provided topic
- Example: `Topic: Artificial Intelligence`

### 3. IF node `[Validation]`
- **Empty topic** → halt execution, return validation message
- **Topic present** → continue to AI agent

### 4. AI agent `[Core]`

The central processing node. Coordinates all content generation tasks.

**Connected components:**

| Component | Role |
|---|---|
| Google Gemini Chat Model | Content generation, text formatting, structuring |
| Simple Memory | Stores context; improves AI response consistency |

**Content outputs generated:**
- Blog title
- Blog outline
- Full blog article
- Social media captions
- Hashtags

### 5. Code node `[Processing]`
- Splits long AI-generated output into smaller chunks
- Required because Telegram enforces message length limits

### 6. Telegram send message `[Output]`
- Receives processed chunks from Code node
- Delivers all content to the configured Telegram chat

---

## Error Handling

| Error | Node | Action | Result |
|---|---|---|---|
| Empty input | IF node | Halt workflow | Prevents invalid AI requests |
| AI / API failure | AI agent + Gemini | Display error message | Prevents workflow crash |
| Message too long | Code node | Split into chunks | Prevents Telegram delivery failure |

---

## Workflow Diagram

```
Manual Trigger
      ↓
 Edit Fields
      ↓
   IF Node
   ↙     ↘
STOP    AI Agent
        ├── Simple Memory
        └── Google Gemini Chat Model
              ↓
          Code Node
              ↓
    Telegram Send Message
```

---

## Expected Execution

1. User provides a topic
2. Input validated — empty topics are rejected
3. AI agent generates: title → outline → article → captions → hashtags
4. Memory maintains context throughout
5. Code node splits output to fit Telegram limits
6. Content delivered to Telegram
7. Errors handled gracefully at every stage
