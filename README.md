# NIFTY 50 Backtest Engine

Quantitative backtesting and risk analysis engine for NIFTY 50 index strategies.

## What It Does

- Downloads 5 years of NIFTY 50 daily data from Yahoo Finance
- Implements two systematic trading strategies:
  1. **SMA 20/50 Crossover** — trend-following
  2. **Bollinger Bands Mean Reversion** — 20-day, 2 standard deviations
- Calculates all performance metrics from formula (no backtesting library):
  - Sharpe Ratio (annualized)
  - CAGR (Compound Annual Growth Rate)
  - Maximum Drawdown
- Applies realistic transaction costs: **0.05% per trade**
- Runs **1000-path Monte Carlo simulation** to assess outcome distribution
- Performs **t-test** for statistical significance of strategy returns
- Generates equity curve charts saved as PNG

## Key Results (NIFTY 50, 2019-2024)

| Metric | Buy & Hold | SMA Crossover | Bollinger Bands |
|--------|-----------|---------------|-----------------|
| Sharpe Ratio | [run notebook] | [run notebook] | [run notebook] |
| CAGR | [run notebook] | [run notebook] | [run notebook] |
| Max Drawdown | [run notebook] | [run notebook] | [run notebook] |
| Total Return | [run notebook] | [run notebook] | [run notebook] |
| Trades | 1 | [run notebook] | [run notebook] |
| t-test p-value | — | [run notebook] | [run notebook] |

## Technical Decisions

- **Vectorized operations only** — no for-loops in backtest core (except Bollinger signal generation which requires state)
- **Look-ahead bias protection** — all signals shifted by 1 day (trade at next open)
- **Metrics from formula** — Sharpe, CAGR, MaxDD calculated manually, not via library
- **Monte Carlo with parametric bootstrap** — 1000 paths using historical mean/std

## Files

- `project1_backtest.ipynb` — Complete notebook with all code, outputs, and charts
- `backtest_results.png` — Generated equity curve and Monte Carlo charts


## Tools

Python, pandas, NumPy, yfinance, matplotlib, scipy.stats

---
Built as Project 1 of quantitative finance learning path.
