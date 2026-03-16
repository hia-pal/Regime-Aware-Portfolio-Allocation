# Regime-Aware Universal Portfolio — Replication & Extension

A replication of Vlasiuk & Smirnov (2025) extended with a comparison of three regime detection methods: Sparse Jump Model (SJM), Hidden Markov Model (HMM), and Regime-Switching GARCH.

---

## Overview

Universal portfolios (Cover, 1991) are model-free strategies that compete with the best constant rebalanced portfolio chosen in hindsight. This project asks: does adding market regime information improve performance?

The answer is yes — but how you detect regimes matters.

We build a value-weighted index from the top-50 US large-cap stocks as of September 2015, infer daily bull/bear regimes using three different models, and implement a simple rule: invest in equities during bull regimes, hold cash during bear regimes. We then compare results across all three detectors.

---

## Results

| Strategy | Return | Vol | Sharpe | Max Drawdown |
|---|---|---|---|---|
| Hold (no regime) | 16.29% | 20.37% | 0.80 | -33.25% |
| Bull-Cash — SJM | 19.59% | 12.34% | 1.59 | -10.60% |
| UP Regime-Aware — SJM | 17.62% | 11.98% | 1.47 | -10.66% |
| Bull-Cash — HMM | 12.67% | 6.40% | 1.98 | -6.45% |
| UP Regime-Aware — HMM | 10.15% | 6.22% | 1.63 | -6.60% |
| Bull-Cash — RS-GARCH | 8.45% | 4.75% | 1.78 | -3.87% |
| UP Regime-Aware — RS-GARCH | 6.89% | 5.01% | 1.38 | -7.06% |

The SJM delivers the best balance — highest absolute return with strong risk reduction. HMM and RS-GARCH reduce volatility more aggressively but give up too much of the equity risk premium by sitting in cash too often.

---

## Pipeline

```
Module 1  →  Data collection & index construction
Module 2  →  Feature engineering (24 features) + SJM regime detection
Module 3  →  Universal portfolio construction & performance analysis
Module 4  →  HMM regime detection + comparison
Module 5  →  RS-GARCH regime detection + full comparison
```

All data is sourced from Yahoo Finance via `yfinance`. No WRDS or Bloomberg access required.

---

## Files

| File | Description |
|---|---|
| `module1_top50.py` | Downloads data, builds top-50 index |
| `module2_features.py` | Computes all 24 features from the paper |
| `module2_sjm.py` | Sparse jump model regime detection |
| `module3_universal_portfolio.py` | Universal portfolio construction |
| `module4_hmm.py` | HMM regime detection |
| `module5_rsgarch.py` | RS-GARCH regime detection |

---

## Requirements

```
yfinance
pandas
numpy
matplotlib
hmmlearn
arch
```

---

## References

- Vlasiuk, D. & Smirnov, M. (2025). *Regime-Aware Universal Portfolio*. Columbia University.
- Cover, T. M. (1991). Universal portfolios. *Mathematical Finance*.
- Shu, Y. & Mulvey, J. M. (2025). Dynamic factor allocation leveraging regime-switching signals. *Journal of Portfolio Management*.
