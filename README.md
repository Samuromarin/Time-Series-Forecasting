# Time Series Forecasting — Retail Sales

**Prophet · SARIMAX · XGBoost**

End-to-end time series forecasting project applied to **TodoVentas S.A.**, an online retail company operating across 10 European countries. The goal is to generate a sales forecast for December 2023 to support a capital increase decision.

---

## Business Context

The finance team needs a December 2023 sales estimate broken down by country to present to shareholders.

**United Kingdom** accounts for 93% of total revenue, showing clear seasonality around Black Friday and Christmas. International markets show a more irregular pattern with lower volume.

---

## Dataset

Daily sales data from December 2022 to December 2023, with transactions across 10 European countries. After filtering out returns and zero-sales days, data is aggregated to weekly frequency.

> The dataset is not included in this repository.

---

## Notebook

| | |
|---|---|
| retail_sales_forecasting.ipynb | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Samuromarin/Time-Series-Forecasting/blob/main/retail_sales_forecasting.ipynb) |

---

## Methodology

The analysis focuses on the UK market (93% of sales) and applies the selected model to 9 international markets.

**Pipeline:**
```
Daily data → EDA + descriptive analysis → Stationarity tests (ADF) + ACF/PACF
→ Train/test split (last 4 weeks as holdout) → Three models trained and evaluated
→ Best model selected → Final forecast for December 2023
```

---

## Models

| Model | Description |
|---|---|
| **Prophet** | Meta's forecasting library for time series with trend and seasonality |
| **SARIMAX** | Classical statistical model with orders selected via `auto_arima` |
| **XGBoost** | Gradient boosting adapted to time series via `sktime` with recursive strategy |

---

## Results

| Model | RMSE | MAPE |
|---|---|---|
| Prophet | 118,111 | 37.72% |
| SARIMAX | 49,995 | 14.37% |
| XGBoost | 62,046 | 16.55% |

> Metrics evaluated on the test period (November 2023). SARIMAX baseline produces a flat line — adding exogenous variables removes this but MAPE rises to 41.32%, as one year of data is insufficient to calibrate the Black Friday effect.

**XGBoost** was selected as the final model for generating more realistic week-by-week predictions.

**Total estimated sales for December 2023: £1,257,821** (UK: 91%, international markets: 9%)

---

## How to Run

1. Clone the repository
2. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn plotly statsmodels pmdarima prophet xgboost sktime scikit-learn
```
3. Place `retail_todo_ventas.csv` and `prod_dict.csv` in the project root
4. Run `retail_sales_forecasting.ipynb` top to bottom

---

## Tech Stack

`Python` · `Pandas` · `Prophet` · `Statsmodels` · `SARIMAX` · `XGBoost` · `sktime` · `Plotly`
