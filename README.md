# German Electricity Demand — Time-Series Forecasting

A case study forecasting **German national electricity load** (Open Power System Data) using a
progression of models — classical benchmarks, SARIMA/SARIMAX, a feature-based Random Forest, and an
LSTM — and comparing them on a **2-year (104-week) hold-out horizon**.

The primary deliverable is [`version1_fixed.ipynb`](version1_fixed.ipynb) (clean, runnable).
[`version-1-output-results.ipynb`](version-1-output-results.ipynb) is a saved run with all figures
and printed outputs.

---

## 1. Data

- **Source:** [Open Power System Data — time series](https://data.open-power-system-data.org/time_series/) (60-minute file, up to Oct 2020).
- **Series:** `DE_load_actual_entsoe_transparency` (German actual load, MW).
- **Window:** 1 Jan 2015 → 30 Sep 2020, aggregated to **daily** and **weekly** means.
- **Exogenous data:** Berlin 2 m temperature from the [Open-Meteo archive API](https://archive-api.open-meteo.com/v1/archive) and German public holidays (`holidays` package).

> The raw CSV is read from the Kaggle path `/kaggle/input/datasets/rishiande/german/opsd_60min_raw.csv`. Change this path if you run elsewhere.

---

## 2. Pipeline (assignment Parts 1–8)

| Part | Content |
|------|---------|
| 1 | Data prep + EDA: daily/weekly aggregation, seasonal decomposition, ADF/KPSS stationarity tests, ACF/PACF |
| 2 | Benchmarks: Mean, Naive, **Seasonal Naive**, Drift |
| 3 | **SARIMA**: full grid search `p∈[0,6]`, `d∈[0,2]`, `q∈[0,6]`; valid within-`d` AIC selection + parsimony; seasonal `(P,D,Q)` search at `s=52`; automatic selection report + residual diagnostics |
| 4 | **SARIMAX**: temperature, temperature², 1-week temperature lag, holiday flag (conditional forecast) |
| 5 | **Random Forest**: recursive multi-step forecast (comparable to SARIMA) **and** a 1-step reference |
| 6 | **LSTM** (hourly): 5-config hyperparameter search, rolling vs open-loop evaluation |
| 7 | Analytical answers to the 6 assignment questions |
| 8 | Consolidated RMSE / MAE / MAPE table + comparison figures |

### Methodological notes
- **AIC is only compared within a fixed differencing order** — comparing across `d` is invalid because the likelihood is computed on the differenced series. `d=1` is chosen from the stationarity tests (`d=2` over-differences).
- **Residual diagnostics** use standardized residuals with the state-space burn-in removed.
- **Fair comparison**: 1-step forecasts (that consume the actual previous week) are labelled separately and never compared with multi-step forecasts.
- Every model reports **RMSE, MAE and MAPE**.

---

## 3. Results (weekly RMSE, 104-week hold-out)

| Model | RMSE (MW) | Forecast type |
|-------|----------:|---------------|
| **Seasonal Naive** | **3006.8** | multi-step (best) |
| Random Forest (recursive) | 3049.8 | multi-step (conditional) |
| SARIMAX (Temp + Holiday) | 3418.0 | multi-step (conditional) |
| SARIMA | 3835.7 | multi-step |
| Mean | 4397.3 | multi-step |
| Naive | 4459.1 | multi-step |
| Drift | 5118.0 | multi-step |
| LSTM (open-loop) | 22564.2 | multi-step |
| Random Forest (1-step) | 2551.5 | 1-step (uses actual lag-1) |
| LSTM (rolling) | 318.7 | 1-step (uses actual lag-1) |

Selected SARIMA model: **SARIMA(1,1,6)×(0,1,1)₅₂** (the seasonal search dropped the insignificant seasonal AR term).

### Key findings
- **No model beats the Seasonal Naive benchmark on multi-step accuracy.** German weekly demand is dominated by a stable annual cycle, so "repeat last year" is a very strong 2-year baseline; the recursive Random Forest essentially matches it.
- The **2020 COVID-19 demand dip** falls in the test window — an exogenous shock none of the models anticipate, which penalises model-based extrapolation.
- **1-step** RF / rolling LSTM have low RMSE only because they see the actual previous value; they are not comparable to multi-step forecasts.
- **Recommended for operational use: SARIMAX** — not for top accuracy, but for native confidence intervals, interpretable temperature/holiday coefficients, exogenous-driver support, and low maintenance.
- SARIMA/SARIMAX residuals are **not perfect white noise** (significant Ljung-Box, non-normal per Shapiro-Wilk), so the Gaussian confidence intervals are approximate.

---

## 4. Repository structure

```
.
├── version1_fixed.ipynb            # primary notebook (clean, runnable)
├── version-1-output-results.ipynb  # saved run with outputs/figures
└── README.md
```

---

## 5. How to run

**Environment:** Python 3.10+, with `numpy`, `pandas`, `matplotlib`, `statsmodels`, `scikit-learn`,
`tensorflow`, `holidays`, `requests`, `scipy`, `joblib`.

**Prerequisites**
- The OPSD CSV available at the path referenced in the first code cell (edit if needed).
- **Internet enabled** (installs `holidays`, and calls the Open-Meteo temperature API).
- **GPU recommended** for the LSTM.

**Steps**
1. Open `version1_fixed.ipynb` (Kaggle / Colab / Jupyter).
2. Ensure the dataset path and GPU/internet settings are correct.
3. **Run all cells** top to bottom.

**Runtime:** roughly 30–60 minutes, dominated by the SARIMA grid search and the LSTM open-loop
recursive forecast (17,472 sequential steps).

---

## 6. References

- Open Power System Data — Time series (Germany, `DE`).
- Open-Meteo Historical Weather API.
- Hyndman, R.J. & Athanasopoulos, G. *Forecasting: Principles and Practice*.
- Burnham, K.P. & Anderson, D.R. *Model Selection and Multimodel Inference* (AIC / parsimony).
- Kong et al. (2017), "Short-Term Residential Load Forecasting based on LSTM Recurrent Neural Network," *IEEE Transactions on Smart Grid*.

---

## 7. Notes & limitations

- SARIMAX/RF-recursive use **observed** future temperature → **conditional (explanatory) forecasts**, not fully operational (a real deployment needs a weather forecast, adding uncertainty). Holidays are deterministic and known in advance.
- The open-loop LSTM is shown in a separate figure because its recursive drift over 2 years reaches very large values and would otherwise distort the comparison plot.
