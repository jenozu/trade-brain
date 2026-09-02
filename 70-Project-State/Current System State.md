---
type: project-state
status: active
created: 2026-09-02
updated: 2026-09-02
confidence: observed
tags:
  - project-state
  - trade-alerts
  - baseline
---

# Current System State

## Repository

Implementation repository: `jenozu/trade-alerts`

Primary branch: `main`

Trading VPS project path: `/docker/trade-alerts`

Python environment: `/docker/trade-alerts/.venv`

## Latest observed test baseline

Manual VPS verification on 2026-09-02 reported:

- **200 passed**
- **25 warnings**
- no reported failures

The warnings were non-fatal and were not treated as reasons to weaken or alter strategy behavior.

`phases.md` still contains an older recorded full-suite count of 180 passes in parts of the document. The repository checklist should be reconciled with the newer verified 200-pass baseline before it is used as the authoritative progress count.

## Completed foundation

The current repository already contains the core research modules for:

- data loading and validation
- resampling
- session logic
- volume / RVOL
- signal-to-noise (`snr.py` means signal-to-noise, not support/resistance)
- swings
- liquidity
- FVG / IFVG
- market structure
- HTF bias
- draw on liquidity
- scoring
- historical backtesting
- rollover/stitching
- ProjectX market-data access

ProjectX Phase 1 is recorded in `phases.md` as fully complete and verified on 2026-09-02.

## Current active direction

The project is moving from a historical research framework toward one production-safe deterministic engine for:

- historical replay
- morning/premarket analysis
- live alerts
- post-session evaluation

The next major work remains centered on production-safe time semantics, especially the explicit `as_of` contract, completed-bar visibility, session correctness, additional session/level coverage, and no-lookahead regression protection.

## Important project constraints

- GitHub `main` is implementation truth.
- Do not recreate modules simply because an old roadmap lists them as future work.
- Preserve no-lookahead behavior.
- Keep data ingestion separate from strategy calculations.
- Python owns objective numeric calculations.
- No automated order placement or brokerage position management.
- Support/resistance confluence must remain separate from signal-to-noise.
- Raw 0–100 score is a confluence score, not a calibrated win probability.

## Coordination

`phases.md` is the canonical implementation checklist for coordinating work across agents and conversations, but unchecked items are not blanket authorization to implement everything. Inspect current code/tests first and work from the first genuinely unresolved item in the active phase.

## Related notes

- [[Backtester Architecture]]
- [[Validated Decisions]]
- [[Premarket Breakout]]

## Implementation references

- `jenozu/trade-alerts/phases.md`
- `jenozu/trade-alerts/config/strategy.yaml`
- `jenozu/trade-alerts/config/sessions.yaml`
- `jenozu/trade-alerts/run_pipeline.py`
