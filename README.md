# momentum-ml-ic-validated

# ML-Enhanced Momentum Stock Selection

A backtest comparing a Random Forest-based stock selection strategy against pure momentum and an SPY benchmark, with a rolling-retrain version tested against a static (train-once) baseline.

## What this does

1. Builds a monthly momentum pre-filter (top 30 candidates from a ~90-stock universe).
2. Trains a Random Forest to rank those candidates by predicted cross-sectional percentile of next-month return, using point-in-time features with no lookahead.
3. Backtests the resulting top-15 portfolio, gross and net of transaction costs, against pure momentum and SPY.
4. Retrains the model every 6 months on an expanding window, to test whether adapting to recent regimes adds value over a static, train-once model.
5. Validates the model's actual predictive skill using the Information Coefficient (Spearman rank correlation between predicted rank and realized return), rather than relying on portfolio returns alone.

## Key result

The rolling-retrained model shows a genuine, positive, modest Information Coefficient (≈0.01) and a better Sharpe ratio and shallower drawdown than pure momentum, evidence that periodically refreshing the model on new data adds real predictive value, not just a smoother-looking equity curve. The static model, by contrast, shows essentially no skill by the same measure, which is itself a useful finding: it isolates *why* the retrained version works, rather than just observing that it does. Full breakdown and discussion in the notebook.

## Notes on methodology

- The stock universe is a hand-picked list of large, well-known companies, backfilled to 2009, a common simplification in backtests like this, but one that likely inflates absolute returns somewhat (survivorship bias), since it excludes companies that were delisted or fell out of the large-cap universe over that period. Discussed in more depth in the notebook.
- Built with a single random seed and one backtest path; re-running with multiple seeds would be a natural next step to test robustness.

