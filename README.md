# 📈 CAPM — Expected Return Analysis

Implementing the **Capital Asset Pricing Model (CAPM)** from scratch in Python to estimate expected stock returns and measure alpha.

Currently covers:
- **META Platforms Inc.** vs S&P 500 (US market)

## What is CAPM?

CAPM estimates the return an investor should expect from a stock given its level of systematic risk (Beta):

$$E(R_i) = R_f + \beta_i \cdot (E(R_m) - R_f)$$

| Symbol | Meaning |
|--------|---------|
| $E(R_i)$ | Expected return of the stock |
| $R_f$ | Risk-free rate |
| $\beta_i$ | Stock's sensitivity to market movements |
| $E(R_m) - R_f$ | Market risk premium |

---

## Project Structure

```
capm-expected-returns/
│
├── capm_expected_returns.ipynb   # US stocks — META vs S&P 500
├── capm_results.png              # Output visualisation
├── requirements.txt              # Python dependencies
└── README.md
```

---

## Methodology

### Step 1 — Data Collection
- Stock prices via `yfinance` (adjusted close)
- Risk-free rate from FRED:
  - US: [DGS10](https://fred.stlouisfed.org/series/DGS10) — 10-Year Treasury Yield

### Step 2 — Returns Calculation
- Daily returns: $r_t = (P_t - P_{t-1}) / P_{t-1}$
- Excess returns: $r_t - R_f$

### Step 3 — Beta Estimation (OLS Regression)
```
Excess Return (Stock) = α + β × Excess Return (Market) + ε
```
Beta is the slope of this regression.

### Step 4 — CAPM Expected Return
```
E(R) = Rf + Beta × (Rm - Rf)
```

### Step 5 — Alpha
```
Alpha = Actual Annualized Return − CAPM Expected Return
```
Positive alpha → stock outperformed its risk-adjusted expectation.

---

## Results

### META Platforms (2020–2024)

| Metric | Value |
|--------|-------|
| Beta | ~ 0.9950 |
| Risk-Free Rate (avg) | ~0.88% |
| Market Return S&P500 | ~12.94% |
| Expected Return (CAPM) | ~12.94% |
| Actual Annualized Return | See notebook |
| Alpha | See notebook |

---

## Setup

### Requirements
```bash
pip install -r requirements.txt
```

### Data Setup
1. Download **DGS10.csv** from https://fred.stlouisfed.org/series/DGS10
2. Update the file paths in the notebooks to match your local directory

### Run
```bash
jupyter notebook capm_expected_returns.ipynb
```

---

## Key Concepts

**Beta**
Measures systematic risk — how much a stock moves relative to the market.
- Beta = 1.0 → moves with the market
- Beta > 1.0 → more volatile than the market
- Beta < 1.0 → less volatile than the market

**Alpha**
Excess return beyond what CAPM predicts. Positive alpha means the stock outperformed its risk-adjusted benchmark.

**Geometric Mean Return**
Used for multi-year market return calculation to account for compounding:
$$\bar{R} = \left(\prod_{t=1}^{n}(1+r_t)\right)^{1/n} - 1$$

---

## Dependencies

- `yfinance` — stock price data
- `pandas` — data manipulation
- `numpy` — numerical computation
- `statsmodels` — OLS regression
- `matplotlib` — visualisation

---

## Limitations

- CAPM is a single-factor model — only captures market risk
- Does not account for size, value, momentum, or other known risk premia (see Fama-French for multi-factor models)
- Beta is estimated from historical data and may not reflect future risk
- Expected returns are backward-looking estimates

---

## Author

**Srinivas**  
