---
type: decision
status: active
created: 2026-09-02
updated: 2026-09-02
confidence: validated
tags:
  - decisions
  - architecture
  - strategy
---

# Validated Decisions

## Purpose

Records durable decisions that are already reflected in the current project configuration, implementation, or canonical phase checklist. This note should not be used to invent new strategy rules.

## Architecture decisions

- Use one shared deterministic strategy engine for historical replay, premarket analysis, live alerts, and post-session evaluation.
- Keep ProjectX/data ingestion separate from strategy calculations.
- Python owns objective numeric calculations.
- The system is analysis/alerts only.
- No automated order placement.
- No automated brokerage position management.
- GitHub `main` is implementation truth.

## Causality decisions

- Future information is prohibited.
- Higher-timeframe values are only available after the relevant bar closes.
- Swing pivots are only available after confirmation.
- Final session levels are only available after their defining window closes.
- Time-of-day RVOL baselines exclude the current session.
- Backtesting uses completed bars only.
- Signals are known at bar close and entries occur on the next bar open under the current backtest model.

## Naming decisions

- `src/snr.py` means **signal-to-noise / market quality**.
- Support/resistance confluence is a separate concept and should be implemented separately rather than redefining SNR.

## Scoring decisions

- Preserve the interpretable internal raw score on a 0–100 scale.
- The raw score is a **confluence score**, not a calibrated probability of winning.
- Do not label the score a win probability until empirical calibration exists.

## Structure decisions

- Current structure confirmation uses candle closes.
- Current break buffer is 0.25 points.
- Wick breaks may be recorded, but they do not count as confirmed structure breaks under the current config.
- BOS and MSS use confirmed swings.
- Displacement is kept as a separate feature so its incremental value can be tested independently.

## Risk/backtest decisions

- Primary stop methodology is structural.
- Preferred initial stop range is 20–25 points.
- Target milestones are 25 / 50 / 75 / 100 points.
- Same-bar stop/target ambiguity is resolved conservatively as stop first.
- Partial exits and automatic initial breakeven moves are currently disabled.

## Session decisions

- Trading/session timezone is America/New_York.
- CME equity-index futures session date rolls at 18:00 ET.
- Current strategy entry window is 09:30–10:30 ET.
- Premarket is currently 04:00–09:30 ET.
- Current London window remains **provisional** and therefore is not a validated production definition.

## Decisions that remain open

Do not promote these to validated rules without explicit evidence and approval:

- exact priority of PMH/PML versus internal breakout structure when the premarket range is wide
- final production London-session definition
- exact 1H/30m/15m versus 4H/Daily bias hierarchy
- which breakout confirmations are mandatory versus scoring-only
- final support/resistance confluence model

## Related notes

- [[Premarket Breakout]]
- [[Market Structure]]
- [[Risk Management]]
- [[Backtester Architecture]]
- [[Current System State]]

## Implementation references

- `jenozu/trade-alerts/phases.md`
- `jenozu/trade-alerts/config/strategy.yaml`
- `jenozu/trade-alerts/config/sessions.yaml`
- `jenozu/trade-alerts/src/structure.py`
- `jenozu/trade-alerts/src/backtest.py`
