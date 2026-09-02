---
type: strategy
status: active
created: 2026-09-02
updated: 2026-09-02
confidence: tested
tags:
  - nq
  - mnq
  - breakout
  - premarket
---

# Premarket Breakout

## Purpose

Defines the current implemented baseline for the NQ/MNQ breakout-retest setup used during the morning trading window.

## Current implemented sequence

The configured primary entry sequence is:

1. important level
2. breakout close
3. retest
4. hold
5. confirmation

The breakout model currently requires a close beyond the level and requires a retest for the primary model. Signals are treated as known at bar close.

## Relevant levels

The strategy currently tracks multiple liquidity/location references, including:

- PMH / PML
- PDH / PDL
- overnight high / low
- London high / low
- internal swings
- external swings
- fair value gaps

PMH/PML are therefore important references, but the current config does **not** define them as the only valid breakout level. The generic entry sequence begins from an `important_level`.

## Session context

The configured strategy window is 09:30–10:30 ET for new entries.

Premarket is currently defined as 04:00–09:30 ET. PMH/PML become finalized at 09:30 ET.

## Confirmation context

The current system can use confluence from:

- higher-timeframe bias
- draw on liquidity
- key location
- liquidity sweep
- displacement
- structure shift
- FVG/retest context
- relative volume
- signal-to-noise
- premium/discount
- room to target

The raw score is a confluence score, not a calibrated win probability.

## Important unresolved question

The repository does not yet encode a final rule for how to prioritize PMH/PML versus more internal structure when the premarket range is unusually wide. Do not silently assume that a PMH/PML break is always required. This needs explicit strategy validation before becoming a production rule.

## Related notes

- [[Market Structure]]
- [[Risk Management]]
- [[Validated Decisions]]
- [[Current System State]]

## Implementation references

- `jenozu/trade-alerts/config/strategy.yaml`
- `jenozu/trade-alerts/config/sessions.yaml`
- `jenozu/trade-alerts/src/liquidity.py`
- `jenozu/trade-alerts/src/structure.py`
- `jenozu/trade-alerts/src/scorer.py`

## Open questions

- Which internal levels qualify as the preferred breakout trigger when PMH/PML are far away?
- Should breakout confirmation be evaluated primarily on 5m, or should 1m/2m confirmation participate in production logic?
- Which confirmation factors are mandatory versus score-enhancing only?
