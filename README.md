# 📈 Speculate in Order, Diversify in Disorder

📄 **Final report:** [Florio_Messina.pdf](Florio_Messina.pdf)

A reproducible implementation of a rolling Shannon-entropy algorithm for dynamic top-10 equity allocation. The project classifies market conditions as **Bullish**, **Neutral**, or **Bearish** and uses each regime to control the concentration allowed in a long-only mean-variance portfolio.

## 👥 Authors

- [Salvatore Messina](https://github.com/SalvatoreMessina11)
- [Francesco Florio](https://github.com/Francesco-Florio)

## 🎯 Purpose

The strategy follows a simple principle: concentrate more when returns are relatively ordered and diversify more when they are disordered. Rolling normalized Shannon entropy is used as a market-state signal, not as a direct return forecast.

The daily pipeline:

1. selects the causal top-10 equity universe;
2. updates rolling returns, means, covariance matrices, and entropy states;
3. compares average entropy with rolling quantile thresholds;
4. assigns a regime-dependent maximum weight;
5. solves a long-only SLSQP allocation in Bullish and Neutral regimes;
6. uses equal weights in the Bearish regime;
7. compares the strategy with a dynamic equal-weight top-10 portfolio and the S&P 500.

## 🧠 Model

| Component | Configuration |
| --- | --- |
| Return and entropy window | 126 trading days |
| Entropy bins | 8 |
| Regime quantile window | 504 trading days |
| Risk-aversion coefficient | 4.0 |
| Bullish maximum weight | 30% |
| Neutral maximum weight | 15% |
| Bearish maximum weight | 10% |

The 10% Bearish cap implies an equal-weight allocation across the ten active stocks. All rolling inputs are constructed causally to avoid look-ahead bias.

## 🗂️ Repository Structure

```text
.
├── data/                                # Prepared model inputs
│   └── README.md                        # Data dictionary and coverage
├── outputs/                             # Generated tables and diagnostics
│   ├── figures/                         # Generated visualizations
│   └── README.md                        # Output data dictionary
├── Messina_Florio.pdf                   # Final 32-page report
├── unified_entropy_portfolio.ipynb      # Complete executable analysis
├── requirements.txt                     # Python dependencies
└── README.md
```

Detailed documentation:

- [Input data guide](data/README.md)
- [Generated output guide](outputs/README.md)
- [Figure gallery and descriptions](outputs/figures/README.md)

## ⚙️ Setup

Python 3.10 or later is recommended.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

## ▶️ Run

Execute the notebook from the repository root:

```powershell
python -m jupyter nbconvert `
  --to notebook `
  --execute `
  --inplace `
  --ExecutePreprocessor.timeout=3600 `
  unified_entropy_portfolio.ipynb
```

The notebook reads from `data/` and regenerates the CSV and PNG files under `outputs/`.

## 📊 Latest Generated Results

The committed run contains 5,382 out-of-sample daily observations.

| Strategy | Annualized return | Annualized volatility | Sharpe ratio |
| --- | ---: | ---: | ---: |
| Entropy market-phase MVO | 14.05% | 20.08% | 0.700 |
| Equal-weight top-10 | 11.50% | 19.40% | 0.593 |
| S&P 500 | 10.98% | 18.76% | 0.585 |

These values describe the supplied historical backtest and are not forecasts of future performance.

## 🧪 Reproducibility Notes

- The three CSV files in `data/` are prepared inputs; raw-data acquisition is outside this repository.
- The investment universe changes daily and is represented through precomputed top-10 membership.
- Rolling entropy quantiles and portfolio inputs use information available before each allocation date.
- The notebook was executed successfully with all 18 code cells completed and no runtime errors.
- Generated outputs are intentionally versioned for transparent comparison with future runs.

## 📚 Citation

```text
Messina, S., and Florio, F. (2026).
Speculate in Order, Diversify in Disorder: A Rolling Shannon-Entropy
Algorithm for Dynamic Top-10 Allocation.
```

## ⚠️ Disclaimer

This repository is an academic and educational project. It does not constitute investment advice, a trading recommendation, or a guarantee of future performance.
