---
type: decision
status: active
created: 2026-09-03
updated: 2026-09-03
confidence: validated
tags:
  - nq
  - configuration
  - backup
---

# Configuration baseline convention

Before any major trading-strategy change or session-semantic change, copy the current `trade-alerts` files `config/strategy.yaml` and `config/sessions.yaml` into a new dated directory here named `YYYY-MM-DD/`.

Each dated baseline must contain:

- `strategy.yaml`
- `sessions.yaml`
- `SHA256SUMS`, with SHA-256 checksums for both copied files
- `README.md`, recording the source repository and exact source commit

The baseline directory and its manifest must be committed and pushed to the `trade-brain` repository before the corresponding strategy or session change begins. Never overwrite an existing dated baseline; if more than one baseline is needed on the same date, append a descriptive suffix after the date.

These files are recovery snapshots and supporting evidence. Current implementation truth remains the live configuration on the `trade-alerts` `main` branch.
