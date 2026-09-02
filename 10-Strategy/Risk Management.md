---
type: strategy
status: active
created: 2026-09-02
updated: 2026-09-02
confidence: tested
tags:
  - nq
  - mnq
  - risk
  - exits
---

# Risk Management

## Purpose

Records the current configured stop, target, holding, and backtest execution assumptions.

## Stop loss

Primary stop method: **structural**.

Current structural stop behavior:

- long: below the active internal/external swing low
- short: above the active internal/external swing high
- structural buffer: **2.0 points**

If the backtester cannot derive a structural stop, the current fallback uses the upper end of the preferred fixed range: **25 points**.

Preferred initial stop range: **20–25 points**.

Research fixed-stop values available for comparison:

- 15
- 20
- 25
- 30
- 35 points

## Targets

Four target milestones are configured:

- TP1: +25 points
- TP2: +50 points
- TP3: +75 points
- TP4: +100 points

The current backtester tracks these as milestones rather than enabling partial exits.

## Trade-management baseline

- maximum holding time: **60 minutes**
- maximum one open trade: enabled
- partial exits: disabled
- automatic move to breakeven: disabled

## Backtest execution assumptions

- completed bars only
- signal is known at bar close
- entry on the next bar open
- slippage enabled: 0.25 points on entry and 0.25 points on exit
- commission currently disabled in config
- if stop and target are both touched on the same bar, resolution is conservative: **stop first**

These assumptions materially affect results and must not be changed just to improve backtest performance.

## Room to target

The strategy currently requires a minimum of **25 points** of room to target as a scoring/confluence feature.

## Guardrails

- Preserve realistic sequencing between signal time and entry time.
- Do not use future intrabar information to choose a favorable same-bar outcome.
- Do not rewrite completed trades when future bars are appended.
- Treat changes to stop/target priority, entry timing, holding limits, partial exits, or breakeven behavior as strategy changes requiring explicit review.

## Related notes

- [[Premarket Breakout]]
- [[Market Structure]]
- [[Backtester Architecture]]
- [[Validated Decisions]]

## Implementation references

- `jenozu/trade-alerts/config/strategy.yaml`
- `jenozu/trade-alerts/src/backtest.py`
- `jenozu/trade-alerts/tests/test_backtest.py`
