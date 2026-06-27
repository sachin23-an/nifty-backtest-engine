# NIFTY 50 Quantitative Backtesting Engine

Vectorised backtesting and risk analysis framework for systematic 
trading strategies on NSE data. All performance metrics and 
statistical tests implemented from formula — no backtesting 
library used.

## Key Finding

SMA Crossover achieved equivalent returns to Buy and Hold 
(15.10% vs 15.41% CAGR) but with half the maximum drawdown 
(-19.93% vs -38.44%), surviving the COVID crash by exiting 
the market when SMA20 crossed below SMA50. Edge is 
statistically significant (t-test p=0.0049).

Bollinger Bands mean reversion failed on a trending index 
(p=0.542) — confirming that strategy-instrument fit matters 
more than strategy complexity.

## Technical Highlights

- Discovered NIFTY 50 returns have excess kurtosis of 18.86 
  (vs 3.0 for normal distribution) — standard parametric 
  models underestimate tail risk on Indian equity data
- Vectorised signal generation throughout — zero row-level 
  for-loops in backtest core
- Look-ahead bias eliminated by shifting all signals by 1 day 
  before position calculation
- Transaction costs modelled at 0.05% per trade (NSE brokerage 
  + STT realistic estimate)
- 1000-path Monte Carlo simulation using historical mean and 
  std to show outcome distribution, not just point estimate
- T-test on active trading days to distinguish genuine edge 
  from random market drift

## Results (NIFTY 50, January 2019 — December 2023)

| Metric | Buy and Hold | SMA Crossover | Bollinger Bands |
|---|---|---|---|
| Sharpe Ratio (gross) | 0.846 | 1.297 | 0.287 |
| Sharpe Ratio (net) | 0.846 | 1.277 | 0.276 |
| CAGR (net) | 15.41% | 15.10% | 3.24% |
| Max Drawdown | -38.44% | -19.93% | -39.38% |
| Total Return (net) | 101.36% | 98.63% | 16.83% |
| Win Rate | 55.00% | 56.78% | 51.96% |
| Number of Trades | 1 | 23 | 18 |
| T-test p-value | 0.062 | 0.005 | 0.542 |
| Statistically Significant | Borderline | Yes | No |

## Monte Carlo Simulation (1000 paths, 1-year horizon)

Based on historical NIFTY 50 return distribution 
(mean 0.064%/day, std 1.204%/day, kurtosis 18.86):

| Percentile | Outcome |
|---|---|
| 5th (worst case) | -15.6% |
| 25th | +1.1% |
| 50th (median) | +16.3% |
| 75th | +30.9% |
| 95th (best case) | +57.5% |

Probability of profit: 76.5%
Probability of 20%+ gain: 41.5%
Probability of 10%+ loss: 8.5%

## What Each Component Demonstrates

**Signal generation:** Vectorised pandas operations using 
np.where and rolling windows — production-style code, 
not tutorial-style loops

**Performance metrics:** Sharpe ratio, CAGR, Max Drawdown, 
Win Rate all derived from formula. Understand the mathematics 
behind every number, not just the output of a library call

**Transaction cost modelling:** Realistic cost applied on 
every position change. Shows awareness that gross backtest 
results overstate real-world performance

**Statistical testing:** T-test distinguishes genuine alpha 
from noise. SMA passes (p=0.005). Bollinger fails (p=0.542). 
Honest reporting of both

**Monte Carlo:** 1000 simulated paths reveal distribution of 
outcomes — a single backtest is one realisation, not a 
guarantee

## Limitations (Honest)

- Daily close data only — real execution happens intraday
- No shorting — long or flat positions only
- Single asset — not a diversified portfolio
- 5-year window includes COVID crash — unusual tail event
- Survivorship bias not applicable (single index, not stock 
  selection)
- Past performance does not predict future results

## How to Run

Open `backtesting_engine.ipynb` in Google Colab and run 
all cells sequentially. No local setup required.

```bash
# All dependencies installed in first cell
!pip install yfinance
```

## Tech Stack

Python · Pandas · NumPy · Matplotlib · SciPy · yfinance

## Author

Sachin Kumar | IIT Madras — BS Data Science  
github.com/sachin23-an
