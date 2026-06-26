# NIFTY 50 Backtesting Engine

Quantitative backtesting and risk analysis engine for NIFTY 50 
index strategies. Built from scratch using Python — no backtesting 
library used.

## What It Does
- Downloads 5 years of NIFTY 50 daily data (2019–2024)
- Implements two systematic strategies:
  - SMA 20/50 Crossover — trend following
  - Bollinger Bands (20-day, 2σ) — mean reversion
- Calculates performance metrics from formula:
  - Sharpe Ratio, CAGR, Maximum Drawdown, Win Rate
- Applies realistic transaction costs (0.05% per trade)
- Runs 1000-path Monte Carlo simulation
- T-test for statistical significance of strategy returns

## Key Results (NIFTY 50, 2019–2024)

| Metric | Buy and Hold | SMA Crossover | Bollinger Bands |
|---|---|---|---|
| Sharpe Ratio (net) | 0.85 | 1.28 | 0.28 |
| CAGR (net) | 15.41% | 15.10% | 3.24% |
| Max Drawdown | -38.44% | -19.93% | -39.38% |
| Total Return | 101.36% | 98.63% | 16.83% |
| Trades | 1 | 23 | 18 |
| T-test p-value | 0.062 | 0.005 | 0.542 |
| Statistically Significant | Borderline | Yes | No |

## Key Finding
SMA Crossover achieved the same returns as Buy and Hold but with 
half the drawdown (-19.93% vs -38.44%). It avoided the COVID crash 
(March 2020) by exiting the market when SMA20 crossed below SMA50. 
The edge is statistically significant (p = 0.0049).

Bollinger Bands mean reversion failed on a trending index — 
confirming that strategy-instrument fit matters more than 
strategy complexity.

## Monte Carlo Simulation (1000 paths, 1-year horizon)
- Median outcome: +16.3%
- Worst 5% scenario: -15.6%  
- Probability of profit: 76.5%

## Tech Stack
Python · Pandas · NumPy · Matplotlib · SciPy · yfinance

## How to Run
Open `backtesting_engine.ipynb` in Google Colab and run all cells.

## Author
Sachin Kumar | IIT Madras | github.com/sachin23-an
