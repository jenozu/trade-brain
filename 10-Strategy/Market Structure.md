---
type: strategy
status: active
created: 2026-09-02
updated: 2026-09-02
confidence: tested
tags:
  - nq
  - mnq
  - structure
  - swings
---

# Market Structure

## Purpose

Captures the current implemented market-structure rules used by the research and scoring pipeline.

## Current structure settings

- Structure breaks use **candle closes**, not wick-only breaks.
- Break buffer: **0.25 points** beyond the active structure level.
- Wick breaks are recorded for context but do **not** count as confirmation.
- BOS requires a confirmed swing.
- MSS requires a confirmed swing.
- MSS does not currently require a prior liquidity event.
- MSS does not currently require displacement.
- CHoCH is enabled with an internal-structure scope.

## Swing causality

Internal and external swings are only available after their right-side confirmation bars have closed. A pivot must not be exposed to the strategy at the historical pivot timestamp before confirmation actually exists.

Current swing settings:

- internal: 2 left / 2 right bars
- external: 5 left / 5 right bars

This confirmation delay is part of the no-lookahead contract and must be preserved in historical replay and live analysis.

## Internal trend

The current implementation derives internal structure trend from confirmed swing sequences:

- higher high + higher low → bullish
- lower high + lower low → bearish
- mixed sequence → neutral
- insufficient confirmed structure → unknown

## Displacement

Displacement is intentionally maintained as a separate feature from structure so its incremental value can be tested.

Current baseline uses candle body size versus ATR and historical median body size, plus close location near the candle extreme. Relative-volume confirmation for displacement is currently disabled.

## Important guardrails

- Do not redefine a wick through structure as a confirmed break while `break_method: close` remains authoritative.
- Do not expose unconfirmed future swing pivots.
- Do not silently make displacement or a prior sweep mandatory for MSS unless the strategy config and tests are deliberately changed.
- When two reasonable definitions of BOS/MSS/CHoCH would produce different trades, treat that as strategy ambiguity and escalate rather than guessing.

## Related notes

- [[Premarket Breakout]]
- [[Risk Management]]
- [[Validated Decisions]]

## Implementation references

- `jenozu/trade-alerts/config/strategy.yaml`
- `jenozu/trade-alerts/src/swings.py`
- `jenozu/trade-alerts/src/structure.py`
- `jenozu/trade-alerts/tests/test_swings.py`
- `jenozu/trade-alerts/tests/test_structure.py`
