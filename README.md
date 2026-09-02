# trade-brain

Persistent second brain for the NQ trading research and alert system.

This repository is an Obsidian-compatible Markdown knowledge base. It stores durable strategy knowledge, architecture decisions, validated research findings, backtest conclusions, data-source notes, and project context that should survive individual AI sessions.

## Authority

This repository is a knowledge layer, not implementation truth. The `jenozu/trade-alerts` repository, its source code, tests, configuration, and current `main` branch remain authoritative for implemented behavior.

If a note here conflicts with current code or tests, the conflict must be investigated rather than silently resolved in favor of the note.

## Structure

- `00-Inbox/` — unsorted notes awaiting review
- `10-Strategy/` — stable trading rules and setup definitions
- `20-Architecture/` — system and software architecture
- `30-Decisions/` — durable design/strategy decisions and rationale
- `40-Research/` — research notes and hypotheses
- `50-Backtests/` — validated backtest findings and summaries
- `60-Data-Sources/` — ProjectX, TopstepX, LSE, TradingView, and other data-source knowledge
- `70-Project-State/` — current system state, known issues, milestones
- `80-Glossary/` — canonical terminology and definitions
- `90-Sources/` — source notes, references, and ingest material
- `Templates/` — note templates

Start with `Home.md` and follow `SCHEMA.md` when creating or updating notes.
