---
type: architecture
status: active
created: 2026-09-02
updated: 2026-09-02
confidence: tested
tags:
  - backtester
  - pipeline
  - causality
---

# Backtester Architecture

## Purpose

Describes the current deterministic research/backtesting pipeline and the architectural rules that must remain stable as the system becomes production-capable.

## Core principle

Historical replay, premarket analysis, live alerts, and later post-session evaluation should converge on one shared deterministic strategy engine. Data ingestion remains separate from strategy calculations. The system is analysis/alerts only; it does not place or manage brokerage orders.

## Current pipeline

`run_pipeline.py` currently orchestrates these stages:

1. load
2. validate
3. resample
4. higher-timeframe bias
5. sessions
6. volume
7. signal-to-noise
8. swings
9. liquidity
10. FVG
11. structure
12. draw on liquidity
13. scoring
14. backtest

## Data and time contract

- canonical storage timestamps are timezone-aware UTC
- trading/session interpretation is America/New_York
- production work is moving toward one explicit `as_of` contract
- completed higher-timeframe bars must be respected
- confirmed swings must not appear before their confirmation time
- finalized session levels must not appear before the relevant session window closes

No-lookahead behavior is an architectural requirement, not merely a test preference.

## Strategy input

The main strategy configuration is `config/strategy.yaml`. Session definitions are in `config/sessions.yaml`.

The scoring layer combines interpretable confluence components into a raw 0–100 score. That score is not a calibrated probability of winning.

## Backtest execution model

The current engine:

- operates on completed bars
- treats a signal as known at bar close
- enters on the following bar open
- uses structural stops where available
- applies configured slippage
- resolves ambiguous same-bar stop/target touches conservatively as stop first
- tracks MFE, MAE, R multiples, and TP milestones
- permits at most one open trade under the current config

## Authority

For implemented behavior, authority order is:

1. current `jenozu/trade-alerts` main-branch source and tests
2. current configuration
3. project governance/phase documents
4. second-brain notes

If this note disagrees with implementation, investigate the discrepancy rather than treating this note as source code truth.

## Related notes

- [[Current System State]]
- [[Validated Decisions]]
- [[Risk Management]]
- [[Market Structure]]

## Implementation references

- `jenozu/trade-alerts/run_pipeline.py`
- `jenozu/trade-alerts/src/backtest.py`
- `jenozu/trade-alerts/config/strategy.yaml`
- `jenozu/trade-alerts/config/sessions.yaml`
- `jenozu/trade-alerts/phases.md`
