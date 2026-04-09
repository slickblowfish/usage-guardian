---
name: usage-guardian
description: |
  Monitor and optimize Claude session usage to prevent token bloat and maintain context freshness.
  Use this skill whenever you're about to start a new task, beginning a new chat session, or want to check if it's time to start a fresh conversation.
  This skill will check your current context size and token usage, save memory snapshots, and recommend starting a new chat if the conversation is getting too heavy.
  It also maintains a persistent memory file (CLAUDE.md) across sessions so you never lose important context about projects, preferences, and ongoing work.
---

# Usage Guardian Skill

Your lightweight usage management system. This skill keeps you aware of when your conversations are getting heavy and ensures you never lose important context between chats.

## What this skill does

1. **Checks context health** — Measures your current conversation size and token usage
2. **Saves memory snapshots** — Creates summaries, full transcripts, and a persistent CLAUDE.md file for cross-session memory
3. **Recommends fresh starts** — Alerts you when context exceeds healthy thresholds (around 8,000 tokens)
4. **Maintains continuity** — Preserves all important information in your outputs folder so memory persists across chats

## How to use it

### At the start of a chat
Invoke this skill to get a status report and see if you should consider starting fresh:

```
@usage-guardian check
```

You'll get back:
- Current context estimate (tokens + message count)
- Memory status (what's been saved so far)
- Recommendation: whether to continue or start a new chat

### When wrapping up
Before ending a chat, invoke it to save memory:

```
@usage-guardian snapshot
```

This creates:
- A full transcript backup
- A summary of key findings/decisions
- Updates to your CLAUDE.md memory file

### Auto-check mode
By default, this skill runs a quiet check at the start of each session. If context is getting large, you'll see a gentle alert with a recommendation.

## Memory structure

All files are saved to your outputs folder for persistence across chats:

```
outputs/
├── CLAUDE.md              # Your persistent working memory (cross-session)
├── memory/
│   ├── chat-summaries/    # Brief summaries of completed chats
│   └── transcripts/       # Full chat histories (searchable)
└── usage-reports/         # Token and context tracking
```

**CLAUDE.md** is the critical file — it's your "working notes" that carry from chat to chat. It includes:
- Current projects and their status
- Important decisions and preferences
- People, acronyms, and context you use frequently
- Action items and deadlines

## Thresholds

For your Pro plan with minimal usage:
- **Green** (under 7,000 tokens): Continue comfortably, you have room
- **Yellow** (7,000–9,000 tokens): Consider starting fresh soon to keep things snappy
- **Red** (over 10,000 tokens): Recommended to start a new chat and load your CLAUDE.md there

These thresholds are conservative — your plan can handle more, but staying lean keeps responses fast and organized.

## Why this matters

Long conversations accumulate context that Claude has to process on every turn, which:
- Slows down response time slightly
- Uses more tokens for the same tasks
- Makes it harder to keep focused

Splitting into fresh chats when context gets heavy fixes this, and CLAUDE.md ensures you don't lose any important information.

## Common workflows

**Workflow 1: Start a new chat**
1. Near the threshold? Invoke `@usage-guardian snapshot` to save everything
2. Start a new chat
3. Early in the new chat, reference your CLAUDE.md to reload context: "Here's my working memory from the last session: [CLAUDE.md content]"

**Workflow 2: During a long session**
1. Check status: `@usage-guardian check`
2. If it looks heavy, save and wrap up that task
3. Come back with a fresh chat

**Workflow 3: Switching between projects**
- Each project can have its own "thread" of chats
- CLAUDE.md keeps the big picture across all of them

## Technical notes

This skill doesn't collect sensitive data — it only tracks metadata (message count, estimated tokens) and summaries you approve. All files are saved locally in your outputs folder. There's no external tracking or reporting.
