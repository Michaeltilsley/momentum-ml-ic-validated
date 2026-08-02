# ML-Enhanced Momentum Stock Selection

A backtest comparing a Random Forest-based stock selection strategy against pure momentum, SPY, and a same-universe equal-weight benchmark, fully out-of-sample (2022-2025).

## What this does

1. Builds a monthly momentum pre-filter (top 30 candidates from a sector-stratified sample of ~180 large-cap stocks).
2. Trains a Random Forest to rank those candidates by predicted cross-sectional percentile of next-month return, using point-in-time features with no lookahead.
3. Backtests the resulting top-15 portfolio, gross and net of transaction costs, against pure momentum, SPY, and an equal-weight benchmark on the same universe, to isolate whether performance comes from stock selection or just universe composition.
4. Validates the model's actual predictive skill using the Information Coefficient (Spearman rank correlation between predicted rank and realized return), rather than relying on portfolio returns alone.

## Key result

The model shows a genuine, positive Information Coefficient (0.0545), meaning its predicted rankings actually correlated with what happened afterward, not just a favourable-looking equity curve. At the portfolio level, it achieved a Sharpe ratio of 1.40 (gross) versus 1.34 for pure momentum, with a shallower max drawdown. Both strategies comfortably beat SPY and the same-universe equal-weight benchmark, confirming the edge comes from active selection rather than just universe composition. Full breakdown and discussion in the notebook.

## Notes on methodology

- The stock universe is a sector-stratified sample of the current S&P 500, which avoids arbitrarily missing large, currently-important companies, but it's still not a full point-in-time reconstruction of a historical index, so some survivorship bias likely remains. Absolute returns should be read as an upper bound, not a forecast. Discussed in depth in the notebook.
- Built with a single random seed and one backtest path; re-running with multiple seeds would be a natural next step to test robustness.

