# Portfolio Optimization & Backtesting

**Author:** Dev Patel
**Initial Capital:** $10,000
**Market:** Indian Equities (NIFTY 50 constituents)

This repository contains my solution to the *Portfolio Optimization & Backtesting Challenge*. The goal is to construct an optimal portfolio from a curated universe of stocks, justify the parameters used for allocation, and rigorously backtest the strategy over the past two years.

The core idea is a **multi-factor stock selection** followed by **Eigen Portfolio–based weight allocation**, with full backtesting, performance metrics, and visualizations.

---

## 📌 Project Overview

* Start with an initial capital of **$10,000**.
* Select a universe of stocks from the Indian market.
* Design a **parameter-driven allocation strategy**.
* Construct a portfolio of **10 stocks**.
* Allocate weights using:

  * **Eigen Portfolio Strategy (PCA-based)**
  * **Minimum Variance Portfolio (MVP)** (implemented but not fully backtested)
* Backtest over the **last 2 years** with:

  * Regular rebalancing (monthly)
  * No look-ahead bias
  * Transaction cost awareness
* Evaluate using:

  * Sharpe Ratio
  * Maximum Drawdown
  * Total Return
  * Sortino, VaR, CVaR, Omega

The detailed methodology and results are documented in the attached report fileciteturn0file0.

---

## 🧠 Strategy

### 1. Stock Universe

* Start with the **top 26 components of NIFTY 50**.
* Compute the following factors for each stock:

  * **Momentum**
  * **Volatility**
  * **Liquidity**
  * **ESG Score**

### 2. Multi-Factor Ranking

Each stock is assigned a *Weighted Score*:

```
Weighted Score = 0.5 × Momentum
               + 0.3 × Volatility
               + 0.1 × ESG Score
               + 0.1 × Liquidity
```

Stocks are ranked by this score and the **top 10** are selected for the portfolio.

### 3. Weight Allocation

Two approaches are implemented:

* **Eigen Portfolio Strategy**

  * Perform eigen-decomposition of the covariance matrix of returns.
  * Use eigenvectors as portfolio directions.
  * Produces orthogonal, decorrelated portfolios.
  * High alpha potential, but riskier.

* **Minimum Variance Portfolio (MVP)**

  * Rooted in Modern Portfolio Theory.
  * Minimizes overall portfolio variance.
  * More stable but lower-return profile.

Backtesting is performed using **Eigen Portfolio weights**, as this strategy better demonstrates the risk–reward trade-off.

---

## 📈 Backtesting

* Time period: **Last 2 years**
* Rebalancing frequency: **Monthly**
* Avoids look-ahead bias (only past data used for decisions)
* Metrics computed:

  * Equity Curve
  * Monthly Returns
  * Portfolio Drawdown
  * Sharpe Ratio
  * Sortino Ratio
  * Max Drawdown
  * VaR / CVaR
  * Omega Ratio

### Results

* **Sharpe Ratio:** 0.96
* **Max Drawdown:** -17.96%
* **Total Return:** 26.90%
* **Sortino Ratio:** 1.18
* **VaR:** -0.01%
* **CVaR:** -0.02%
* **Omega Ratio:** 1.19

These demonstrate a strong risk-adjusted performance for a strategy driven by PCA and factor-based selection fileciteturn0file0.

---

## 📂 Repository Structure (Suggested)

```
Portfolio-Optimization/
│
├── data/                 # Cached price / factor data (optional)
├── notebooks/            # Jupyter notebooks (analysis & experiments)
│   └── main.ipynb
├── src/                  # Core Python modules
│   ├── factors.py
│   ├── portfolio.py
│   ├── backtest.py
│   └── metrics.py
├── report/               # PDF report
│   └── Quant_Task.pdf
├── requirements.txt
└── README.md
```

You can keep everything in a single notebook if you prefer, but modularizing the code improves clarity and professionalism.

---

## 🚀 How to Run

```bash
git clone https://github.com/<your-username>/Portfolio-Optimization.git
cd Portfolio-Optimization
pip install -r requirements.txt

# Run notebook
jupyter notebook notebooks/main.ipynb
```

Dependencies typically include:

```txt
yfinance
numpy
pandas
matplotlib
scipy
scikit-learn
```

---

## 🔮 Future Improvements

* Quarterly and adaptive rebalancing
* Benchmark scaling to the same capital base
* Robust / Sparse PCA for noisy covariance matrices
* Multi-factor Eigen Portfolios (combine top-k eigenvectors)
* Transaction cost modeling in more detail
* Walk-forward validation

