# Usage Guardian

A lightweight token and context management system for Claude. Monitor conversation size, get alerts when it's time to start fresh, and maintain persistent memory across sessions.

## What It Does

- **Context Health Check** — See your current token usage and conversation size
- **Smart Alerts** — Get notified when context exceeds healthy thresholds
- **Memory Snapshots** — Save chat transcripts, summaries, and a persistent CLAUDE.md file
- **Cross-Session Memory** — Never lose important context between chats

## Installation

1. Copy the `SKILL.md` file to your Claude skills directory
2. Restart Claude
3. The skill will be available in your skill library

## Quick Start

Check your context health:
```
@usage-guardian check
```

Save a memory snapshot:
```
@usage-guardian snapshot
```

## How It Works

- Tracks your current token usage and message count
- Saves memory to your outputs folder for persistence across chats
- Maintains CLAUDE.md as your working notes (projects, decisions, context)
- Recommends starting fresh when context exceeds ~8,000 tokens

## Thresholds

- **Green** (under 7,000 tokens): Continue comfortably
- **Yellow** (7,000–9,000 tokens): Consider a fresh chat soon
- **Red** (over 10,000 tokens): Recommended to start new chat with CLAUDE.md loaded

## Files Generated

All saved to your outputs folder:
- `CLAUDE.md` — Persistent working memory
- `memory/chat-summaries/` — Chat summaries
- `memory/transcripts/` — Full chat histories
- `usage-reports/` — Token tracking

## License

MIT — Free to use, modify, and distribute.

## Contributing

Got improvements? Fork it, build it, submit a PR.
