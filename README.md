# momentum-ml-ic-validated

# ML-Enhanced Momentum Stock Selection

A backtest comparing a Random Forest-based stock selection strategy against
pure momentum and an SPY benchmark, with a rolling-retrain version tested
against a static (train-once) baseline.

## What this does

1. Builds a monthly momentum pre-filter (top 30 candidates from a ~90-stock universe).
2. Trains a Random Forest to rank those candidates by predicted cross-sectional
   percentile of next-month return (not raw return — see below), using
   point-in-time features with no lookahead.
3. Backtests the resulting top-15 portfolio, gross and net of transaction costs,
   against pure momentum and SPY.
4. Repeats the comparison with the model retrained every 6 months on an
   expanding window, to test whether adapting to recent regimes adds value.
5. Validates the model's actual predictive skill using the Information
   Coefficient (Spearman rank correlation between predicted rank and realized
   return), not just portfolio-level returns.

## Key result

The static (train-once) model shows essentially no genuine predictive skill
(IC ≈ -0.002) — its backtest performance is attributable to the momentum
pre-filter, not the model. The rolling-retrained model shows a small but
genuine positive IC (≈ 0.01) and a better Sharpe ratio and drawdown profile
than pure momentum, though not a higher raw return. Full writeup in the notebook.

## Key limitations

- **Survivorship bias.** The stock universe is a hand-picked list of large,
  currently-successful companies, backfilled to 2009. Any company delisted,
  bankrupted, or dropped from the large-cap universe over that period is
  excluded — absolute returns here are an upper bound, not a forecast.
- Single random seed, single backtest path — no variance estimate across runs.
- Full discussion in the "Limitations and Open Questions" section of the notebook.
