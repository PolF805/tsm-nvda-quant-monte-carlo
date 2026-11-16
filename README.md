# TSMC vs. NVIDIA: Quantitative Stock Analysis & Monte Carlo Simulation

A quantitative analysis and price simulation project comparing 5 years of daily stock data (**Oct 2021 – Oct 2026**, 1,253 trading days) for **TSMC (`TSM`)** and **NVIDIA (`NVDA`)**.

## What This Project Does
1. **Data Pipeline (SQL):** Pulls historical market data using `yfinance`, cleans out missing or duplicate entries, and aligns trading dates in a local **SQLite** database using `INNER JOIN` and `LAG()` window functions.
2. **Return & Regression Analysis:** Calculates daily log returns, annualized volatility, and 50/252-day moving averages in `pandas`. Uses an **OLS Linear Regression** model (`statsmodels`) to measure how sensitive TSMC's daily returns are to NVIDIA's ($\beta = 0.5087, R^2 = 0.470, p < 0.001$).
3. **Return Distribution Check:** Compares actual daily log returns (via Kernel Density Estimates) against a standard normal distribution using `SciPy` and `Seaborn`, confirming heavy-tailed market behavior ($\text{Kurtosis} = 5.44$).
4. **Out-of-Sample Monte Carlo Simulation:** Splits the data chronologically into a **4-year training period (2021–2025)** and a **1-year test period (2025–2026)** to avoid data leakage. Runs 1,500 **Geometric Brownian Motion (GBM)** simulations in `NumPy` (testing both independent and correlated shocks) to see how well the 90% confidence interval captures actual Year-5 prices and volatility.

## Tools Used
* **Languages:** Python, SQL (SQLite)
* **Libraries:** `numpy`, `pandas`, `statsmodels`, `scipy`, `seaborn`, `matplotlib`, `yfinance`
